#include <stdio.h>
void centroid();
void circle();
void rectangle();
void semicircle();
void quartercircle();
void triangle();
void ra();
void na();


void ra() {
    float base, height, area, x, y;
    printf("Enter the base: ");
    scanf("%f", &base);
    printf("Enter the height: ");
    scanf("%f", &height);
    area = (height * base) / 2;
    x = base / 3;
    y = height / 3;
    printf("The area of the triangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    printf("Thank you\n");
    printf("Made by Yug Shah.\n");
}

void na() {
    float base, height, area, x, y;
    printf("Enter the base: ");
    scanf("%f", &base);
    printf("Enter the height: ");
    scanf("%f", &height);
    area = (height * base) / 2;
    x = base / 2;
    y = height / 3;
    printf("The area of the triangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    printf("Thank you\n");
    printf("Made by Yug Shah.\n");
}

int main() {
    int a;
    printf("Enter the number of figure: ");
    scanf("%d", &a);
    if (a == 0) {
        printf("Thank you.\n");
        printf("Made by Yug Shah.\n");
    } else if (a == 1) {
        centroid();
    } else {
        printf("Coming soon\n");
        printf("Made by Yug Shah.\n"); // work later
    }
    return 0;
}

void centroid() {
    char c[3];
    printf("Enter the shape\nFor rectangle: (r)\nFor circle: (c)\nFor triangle: (t)\nFor semicircle: (sc)\nFor quartercircle: (qc)\n");
    scanf("%2s", c);
    if (c[0] == 'c' && c[1] == '\0') {
        circle();
    } else if (c[0] == 'r' && c[1] == '\0') {
        rectangle();
    } else if (c[0] == 't' && c[1] == '\0') {
        triangle();
    } else if (c[0] == 's' && c[1] == 'c' && c[2] == '\0') {
        semicircle();
    } else if (c[0] == 'q' && c[1] == 'c' && c[2] == '\0') {
        quartercircle();
    } else {
        printf("Invalid value\nError!\nTry again.\n");
        centroid();
    }
}

void triangle() {
    char angle[4];
    printf("Is the triangle right angle (yes) or not (no)? ");
    scanf("%3s", angle);
    if (angle[0] == 'y' && angle[1] == 'e' && angle[2] == 's' && angle[3] == '\0') {
        ra();
    } else if (angle[0] == 'n' && angle[1] == 'o' && angle[2] == '\0') {
        na();
    } else {
        printf("Invalid input\nTry again\n");
        triangle();
    }
}

void rectangle() {
    float base, height, area, x, y;
    printf("Enter the base: ");
    scanf("%f", &base);
    printf("Enter the height: ");
    scanf("%f", &height);
    area = height * base;
    x = base / 2;
    y = height / 2;
    printf("The area of the rectangle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    printf("Thank you\nMade by Yug Shah\n");
}

void semicircle() {
    float radius, area, x, y;
    printf("Enter the radius: ");
    scanf("%f", &radius);
    area = (3.14 * radius * radius) / 2;
    x = radius;
    y = (4 * radius) / (3 * 3.14);
    printf("The area of the semicircle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    printf("Thank you\nMade by Yug Shah\n");
}

void quartercircle() {
    float radius, area, x, y;
    printf("Enter the radius: ");
    scanf("%f", &radius);
    area = (3.14 * radius * radius) / 4;
    x = (4 * radius) / (3 * 3.14);
    y = (4 * radius) / (3 * 3.14);
    printf("The area of the quarter circle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    printf("Thank you\nMade by Yug Shah\n");
}

void circle() {
    float radius, area, x, y;
    printf("Enter the radius: ");
    scanf("%f", &radius);
    area = 3.14 * radius * radius;
    x = radius;
    y = radius;
    printf("The area of the circle: %f\n", area);
    printf("The centroid is (x, y) = (%f, %f)\n", x, y);
    printf("Thank you\nMade by Yug Shah\n");
}# centroid.c
