#include <stdio.h>
#include <string.h>

#define PI 3.14f

/* Compute and display the centroid of a right-angled triangle. */
static void right_angle_triangle(void) {
    float base, height, area, centroid_x, centroid_y;

    printf("Enter the base: ");
    scanf("%f", &base);
    printf("Enter the height: ");
    scanf("%f", &height);

    area = (height * base) / 2.0f;
    centroid_x = base / 3.0f;
    centroid_y = height / 3.0f;

    printf("The area of the triangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", centroid_x, centroid_y);
    printf("Thank you\n");
    printf("Made by Yug Shah.\n");
}

/* Compute and display the centroid of a non-right-angled triangle. */
static void non_right_angle_triangle(void) {
    float base, height, area, centroid_x, centroid_y;

    printf("Enter the base: ");
    scanf("%f", &base);
    printf("Enter the height: ");
    scanf("%f", &height);

    area = (height * base) / 2.0f;
    centroid_x = base / 2.0f;
    centroid_y = height / 3.0f;

    printf("The area of the triangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", centroid_x, centroid_y);
    printf("Thank you\n");
    printf("Made by Yug Shah.\n");
}

/* Compute and display the centroid of a rectangle. */
static void rectangle(void) {
    float base, height, area, centroid_x, centroid_y;

    printf("Enter the base: ");
    scanf("%f", &base);
    printf("Enter the height: ");
    scanf("%f", &height);

    area = height * base;
    centroid_x = base / 2.0f;
    centroid_y = height / 2.0f;

    printf("The area of the rectangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", centroid_x, centroid_y);
    printf("Thank you\nMade by Yug Shah\n");
}

/* Compute and display the centroid of a circle. */
static void circle(void) {
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

/* Compute and display the centroid of a semicircle. */
static void semicircle(void) {
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

/* Compute and display the centroid of a quarter circle. */
static void quartercircle(void) {
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

/* Prompt for a triangle type and dispatch to the appropriate handler. */
static void triangle(void) {
    char angle[4];

    while (1) {
        printf("Is the triangle right angle (yes) or not (no)? ");
        scanf("%3s", angle);

        if (strcmp(angle, "yes") == 0) {
            right_angle_triangle();
            break;
        } else if (strcmp(angle, "no") == 0) {
            non_right_angle_triangle();
            break;
        } else {
            printf("Invalid input\nTry again\n");
        }
    }
}

/* Prompt for a shape and dispatch to the appropriate centroid calculator. */
static void centroid(void) {
    char shape[3];

    while (1) {
        printf("Enter the shape\nFor rectangle: (r)\nFor circle: (c)\nFor triangle: (t)\nFor semicircle: (sc)\nFor quartercircle: (qc)\n");
        scanf("%2s", shape);

        if (strcmp(shape, "c") == 0) {
            circle();
            break;
        } else if (strcmp(shape, "r") == 0) {
            rectangle();
            break;
        } else if (strcmp(shape, "t") == 0) {
            triangle();
            break;
        } else if (strcmp(shape, "sc") == 0) {
            semicircle();
            break;
        } else if (strcmp(shape, "qc") == 0) {
            quartercircle();
            break;
        } else {
            printf("Invalid value\nError!\nTry again.\n");
        }
    }
}

int main(void) {
    int choice;

    printf("Enter the number of figure: ");
    scanf("%d", &choice);

    if (choice == 0) {
        printf("Thank you.\n");
        printf("Made by Yug Shah.\n");
    } else if (choice == 1) {
        centroid();
    } else {
        printf("Coming soon\n");
        printf("Made by Yug Shah.\n");
    }

    return 0;
}

# centroid.c