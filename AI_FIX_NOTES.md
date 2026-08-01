# AI Fix — Issue #2: Code Quality: Refactor repeated logic across modules

**Issue body:**

This is an automated issue created by the AI agent to track planned code quality improvements. The AI will fix this in a subsequent run.

---

**AI-proposed fix:**

### Root-cause analysis

The codebase repeatedly implements the same low-level geometry “plumbing” in several modules—most likely:

* Validating a `point_t` array (`pts != NULL && n > 0`).
* Iterating over points to sum `x` / `y`.
* Allocating / freeing point arrays.

When the same loop/validation logic is copy-pasted across modules, fixes and behavior changes have to be applied in multiple places, which is error-prone and inflates the code size.

---

### Exact code changes needed

> **Note:** I do not have the live repo contents, so the paths below follow the `centroid.c` naming convention. Adjust the directory names if your layout differs. The duplicated logic to replace is wherever you see the same `for` loop summing points or the same `if (!pts || n == 0)` guard.

#### 1. Create a shared utility module

**File:** `src/geometry_utils.h`

```c
#ifndef GEOMETRY_UTILS_H
#define GEOMETRY_UTILS_H

#include <stddef.h>

typedef struct {
    double x;
    double y;
} point_t;

/* Validate a point array. Returns 0 on success, -1 on error (errno = EINVAL). */
int validate_points(const point_t *pts, size_t n);

/* Sum all x and y coordinates into *sx and *sy. */
void sum_coordinates(const point_t *pts, size_t n, double *sx, double *sy);

/* Allocate / free a point array. */
point_t *alloc_points(size_t n);
void free_points(point_t *pts);

#endif /* GEOMETRY_UTILS_H */
```

**File:** `src/geometry_utils.c`

```c
#include "geometry_utils.h"
#include <stdlib.h>
#include <errno.h>

int validate_points(const point_t *pts, size_t n)
{
    if (pts == NULL || n == 0) {
        errno = EINVAL;
        return -1;
    }
    return 0;
}

void sum_coordinates(const point_t *pts, size_t n, double *sx, double *sy)
{
    double x = 0.0;
    double y = 0.0;

    for (size_t i = 0; i < n; ++i) {
        x += pts[i].x;
        y += pts[i].y;
    }

    *sx = x;
    *sy = y;
}

point_t *alloc_points(size_t n)
{
    if (n == 0) {
        errno = EINVAL;
        return NULL;
    }
    return malloc(n * sizeof(point_t));
}

void free_points(point_t *pts)
{
    free(pts);
}
```

#### 2. Replace the duplicated logic in `centroid.c`

**File:** `src/centroid.c`

```c
#include "centroid.h"
#include "geometry_utils.h"

point_t compute_centroid(const point_t *pts, size_t n)
{
    if (validate_points(pts, n) != 0) {
        /* Caller should check errno. */
        return (point_t){0.0, 0.0};
    }

    double sx, sy;
    sum_coordinates(pts, n, &sx, &sy);

    return (point_t){
        .x = sx / (double)n,
        .y = sy / (double)n
    };
}
```

Remove any inline `if (!pts || n == 0)` checks and any `for` loops that sum `x`/`y` inside this file.

#### 3. Replace the same repeated patterns in other modules

In every other module that currently repeats the validation or summation logic (for example, `src/input.c`, `src/output.c`, `src/polygon.c`, or test files), replace the duplicated blocks with:

```c
#include "geometry_utils.h"

/* Replace this: */
/* if (!pts || n == 0) { ... } */
/* with this: */
if (validate_points(pts, n) != 0) { ... }

/* Replace this: */
/* double sx=0, sy=0; for (...) { sx += ...; sy += ...; } */
/* with this: */
double sx, sy;
sum_coordinates(pts, n, &sx, &sy);
```

#### 4. Update the build system

**File:** `Makefile` (or `CMakeLists.txt`)

Add `src/geometry_utils.c` to the source list, for example:

```make
SRCS = src/main.c src/centroid.c src/geometry_utils.c
```

or in CMake:

```cmake
add_executable(centroid
    src/main.c
    src/centroid.c
    src/geometry_utils.c
)
```

---

### Follow-up actions

1. **Audit for more duplication** – search the repo for patterns like `pts == NULL`, `n == 0`, `for.*x +=`, and `malloc.*sizeof(point_t)` to make sure all repeated logic is routed through `geometry_utils`.
2. **Add unit tests** for the new helpers, e.g.:
   * `validate_points(NULL, 5)` returns `-1`.
   * `sum_coordinates` on `{(1,2),(3,4)}` returns `(4,6)`.
   * `alloc_points(0)` returns `NULL` and sets `errno`.
3. **Static analysis / CI** – run `clang -Wall -Wextra`, `clang-tidy`, or `cppcheck` to confirm no dead duplicated code remains.
4. **Code review** – have a second reviewer check that all previous call sites now use the shared helpers and that error handling is consistent.

If you paste the specific duplicated snippets from the repo, I can turn this template into an exact, line-numbered patch for your files.
