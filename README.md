#include <stdio.h>
#include <string.h>

/* Centroid calculator: computes the area and centroid for common 2-D shapes.
   The original program used 3.14 as the value of pi, so that value is kept
   here to preserve the existing numeric behaviour. */
static const float PI = 3.14f;

/* Function prototypes */
void show_centroid_menu(void);
void process_circle(void);
void process_rectangle(void);
void process_semicircle(void);
void process_quartercircle(void);
void process_triangle(void);
void process_right_angled_triangle(void);
void process_non_right_angled_triangle(void);

/* Right-angled triangle: base and height are the two perpendicular sides.
   Area = (base * height) / 2.
   The centroid of a right triangle is at (base/3, height/3). */
void process_right_angled_triangle(void) {
    float base, height, area, centroid_x, centroid_y;

    printf("Enter the base: ");
    scanf("%f", &base);
    printf("Enter the height: ");
    scanf("%f", &height);

    area = (base * height) / 2.0f;
    centroid_x = base / 3.0f;
    centroid_y = height / 3.0f;

    printf("The area of the triangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", centroid_x, centroid_y);
    printf("Thank you\n");
    printf("Made by Yug Shah.\n");
}

/* Non-right-angled triangle: treated as a generic triangle with the base on the x-axis.
   Area = (base * height) / 2.
   Centroid x-coordinate is the midpoint of the base (base/2);
   y-coordinate is one-third of the height (height/3). */
void process_non_right_angled_triangle(void) {
    float base, height, area, centroid_x, centroid_y;

    printf("Enter the base: ");
    scanf("%f", &base);
    printf("Enter the height: ");
    scanf("%f", &height);

    area = (base * height) / 2.0f;
    centroid_x = base / 2.0f;
    centroid_y = height / 3.0f;

    printf("The area of the triangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", centroid_x, centroid_y);
    printf("Thank you\n");
    printf("Made by Yug Shah.\n");
}

/* Program entry point: choose a figure type.
   0 exits, 1 starts the centroid calculator, any other value shows "Coming soon". */
int main(void) {
    int choice;

    printf("Enter the number of figure: ");
    scanf("%d", &choice);

    if (choice == 0) {
        printf("Thank you.\n");
        printf("Made by Yug Shah.\n");
    } else if (choice == 1) {
        show_centroid_menu();
    } else {
        printf("Coming soon\n");
        printf("Made by Yug Shah.\n");
    }

    return 0;
}

/* Display the shape selection menu and keep asking until a valid shape is entered. */
void show_centroid_menu(void) {
    char shape[3];
    int choice_is_valid = 0;

    while (!choice_is_valid) {
        printf("Enter the shape\n"
               "For rectangle: (r)\n"
               "For circle: (c)\n"
               "For triangle: (t)\n"
               "For semicircle: (sc)\n"
               "For quartercircle: (qc)\n");
        scanf("%2s", shape);

        if (strcmp(shape, "c") == 0) {
            process_circle();
            choice_is_valid = 1;
        } else if (strcmp(shape, "r") == 0) {
            process_rectangle();
            choice_is_valid = 1;
        } else if (strcmp(shape, "t") == 0) {
            process_triangle();
            choice_is_valid = 1;
        } else if (strcmp(shape, "sc") == 0) {
            process_semicircle();
            choice_is_valid = 1;
        } else if (strcmp(shape, "qc") == 0) {
            process_quartercircle();
            choice_is_valid = 1;
        } else {
            printf("Invalid value\nError!\nTry again.\n");
        }
    }
}

/* Ask whether the triangle is right-angled and dispatch to the correct handler. */
void process_triangle(void) {
    char answer[4];
    int answer_is_valid = 0;

    while (!answer_is_valid) {
        printf("Is the triangle right angle (yes) or not (no)? ");
        scanf("%3s", answer);

        if (strcmp(answer, "yes") == 0) {
            process_right_angled_triangle();
            answer_is_valid = 1;
        } else if (strcmp(answer, "no") == 0) {
            process_non_right_angled_triangle();
            answer_is_valid = 1;
        } else {
            printf("Invalid input\nTry again\n");
        }
    }
}

/* Rectangle: area = base * height; centroid is at the geometric centre. */
void process_rectangle(void) {
    float base, height, area, centroid_x, centroid_y;

    printf("Enter the base: ");
    scanf("%f", &base);
    printf("Enter the height: ");
    scanf("%f", &height);

    area = base * height;
    centroid_x = base / 2.0f;
    centroid_y = height / 2.0f;

    printf("The area of the rectangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", centroid_x, centroid_y);
    printf("Thank you\nMade by Yug Shah\n");
}

/* Semicircle: area = (pi * r^2) / 2.
   Centroid coordinates: (r, 4r / (3*pi)). */
void process_semicircle(void) {
    float radius, area, centroid_x, centroid_y;

    printf("Enter the radius: ");
    scanf("%f", &radius);

    area = (PI * radius * radius) / 2.0f;
    centroid_x = radius;
    centroid_y = (4.0f * radius) / (3.0f * PI);

    printf("The area of the semicircle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", centroid_x, centroid_y);
    printf("Thank you\nMade by Yug Shah\n");
}

/* Quarter circle: area = (pi * r^2) / 4.
   Centroid is equidistant along both axes at (4r / (3*pi), 4r / (3*pi)). */
void process_quartercircle(void) {
    float radius, area, centroid_x, centroid_y;

    printf("Enter the radius: ");
    scanf("%f", &radius);

    area = (PI * radius * radius) / 4.0f;
    centroid_x = (4.0f * radius) / (3.0f * PI);
    centroid_y = (4.0f * radius) / (3.0f * PI);

    printf("The area of the quarter circle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", centroid_x, centroid_y);
    printf("Thank you\nMade by Yug Shah\n");
}

/* Circle: area = pi * r^2; centroid is at the centre of the circle. */
void process_circle(void) {
    float radius, area, centroid_x, centroid_y;

    printf("Enter the radius: ");
    scanf("%f", &radius);

    area = PI * radius * radius;
    centroid_x = radius;
    centroid_y = radius;

    printf("The area of the circle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", centroid_x, centroid_y);
    printf("Thank you\nMade by Yug Shah\n");
}

# centroid.c