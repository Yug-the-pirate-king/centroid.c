#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>

#ifndef M_PI
#define M_PI 3.14159265358979323846
#endif

static void print_signature(void) {
    printf("Thank you\n");
    printf("Made by Yug Shah.\n");
}

static int read_line(char *buffer, size_t size) {
    if (fgets(buffer, (int)size, stdin) == NULL) {
        return 0;
    }

    size_t len = strlen(buffer);
    if (len > 0 && buffer[len - 1] == '\n') {
        buffer[len - 1] = '\0';
    }

    return 1;
}

static int read_int(const char *prompt, int *value) {
    char line[64];
    char *endptr;

    printf("%s", prompt);
    if (!read_line(line, sizeof(line))) {
        return 0;
    }

    long tmp = strtol(line, &endptr, 10);
    if (endptr == line || *endptr != '\0') {
        return 0;
    }

    *value = (int)tmp;
    return 1;
}

static int read_double(const char *prompt, double *value) {
    char line[64];
    char *endptr;

    printf("%s", prompt);
    if (!read_line(line, sizeof(line))) {
        return 0;
    }

    double tmp = strtod(line, &endptr);
    if (endptr == line || *endptr != '\0') {
        return 0;
    }

    *value = tmp;
    return 1;
}

static void right_angled_triangle(void) {
    double base, height, area, x, y;

    while (!read_double("Enter the base: ", &base)) {
        printf("Invalid input. Please enter a valid number.\n");
    }
    while (!read_double("Enter the height: ", &height)) {
        printf("Invalid input. Please enter a valid number.\n");
    }

    area = (height * base) / 2.0;
    x = base / 3.0;
    y = height / 3.0;

    printf("The area of the triangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    print_signature();
}

static void non_right_angled_triangle(void) {
    double base, height, area, x, y;

    while (!read_double("Enter the base: ", &base)) {
        printf("Invalid input. Please enter a valid number.\n");
    }
    while (!read_double("Enter the height: ", &height)) {
        printf("Invalid input. Please enter a valid number.\n");
    }

    area = (height * base) / 2.0;
    x = base / 2.0;
    y = height / 3.0;

    printf("The area of the triangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    print_signature();
}

static void handle_triangle(void) {
    char angle[8];

    for (;;) {
        printf("Is the triangle right angle (yes) or not (no)? ");
        if (!read_line(angle, sizeof(angle))) {
            printf("Invalid input\nTry again\n");
            continue;
        }

        if (strcmp(angle, "yes") == 0) {
            right_angled_triangle();
            return;
        } else if (strcmp(angle, "no") == 0) {
            non_right_angled_triangle();
            return;
        } else {
            printf("Invalid input\nTry again\n");
        }
    }
}

static void rectangle(void) {
    double base, height, area, x, y;

    while (!read_double("Enter the base: ", &base)) {
        printf("Invalid input. Please enter a valid number.\n");
    }
    while (!read_double("Enter the height: ", &height)) {
        printf("Invalid input. Please enter a valid number.\n");
    }

    area = height * base;
    x = base / 2.0;
    y = height / 2.0;

    printf("The area of the rectangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    printf("Thank you\nMade by Yug Shah\n");
}

static void semicircle(void) {
    double radius, area, x, y;

    while (!read_double("Enter the radius: ", &radius)) {
        printf("Invalid input. Please enter a valid number.\n");
    }

    area = (M_PI * radius * radius) / 2.0;
    x = radius;
    y = (4.0 * radius) / (3.0 * M_PI);

    printf("The area of the semicircle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    printf("Thank you\nMade by Yug Shah\n");
}

static void quartercircle(void) {
    double radius, area, x, y;

    while (!read_double("Enter the radius: ", &radius)) {
        printf("Invalid input. Please enter a valid number.\n");
    }

    area = (M_PI * radius * radius) / 4.0;
    x = (4.0 * radius) / (3.0 * M_PI);
    y = (4.0 * radius) / (3.0 * M_PI);

    printf("The area of the quarter circle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    printf("Thank you\nMade by Yug Shah\n");
}

static void circle(void) {
    double radius, area, x, y;

    while (!read_double("Enter the radius: ", &radius)) {
        printf("Invalid input. Please enter a valid number.\n");
    }

    area = M_PI * radius * radius;
    x = radius;
    y = radius;

    printf("The area of the circle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    printf("Thank you\nMade by Yug Shah\n");
}

static void select_shape(void) {
    char shape[8];

    for (;;) {
        printf("Enter the shape\n");
        printf("For rectangle: (r)\n");
        printf("For circle: (c)\n");
        printf("For triangle: (t)\n");
        printf("For semicircle: (sc)\n");
        printf("For quartercircle: (qc)\n");

        if (!read_line(shape, sizeof(shape))) {
            printf("Invalid value\nError!\nTry again.\n");
            continue;
        }

        if (strcmp(shape, "c") == 0) {
            circle();
            return;
        } else if (strcmp(shape, "r") == 0) {
            rectangle();
            return;
        } else if (strcmp(shape, "t") == 0) {
            handle_triangle();
            return;
        } else if (strcmp(shape, "sc") == 0) {
            semicircle();
            return;
        } else if (strcmp(shape, "qc") == 0) {
            quartercircle();
            return;
        } else {
            printf("Invalid value\nError!\nTry again.\n");
        }
    }
}

int main(void) {
    int choice;

    if (!read_int("Enter the number of figure: ", &choice)) {
        return EXIT_FAILURE;
    }

    if (choice == 0) {
        print_signature();
    } else if (choice == 1) {
        select_shape();
    } else {
        printf("Coming soon\n");
        printf("Made by Yug Shah.\n");
    }

    return EXIT_SUCCESS;
}