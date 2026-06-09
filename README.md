# CSE-B-MINI-PROJECT
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
#define WIDTH 50
#define HEIGHT 20
#define MAX_OBJECTS 100

typedef enum {
    CIRCLE,
    RECTANGLE,
    LINE,
    TRIANGLE
} ShapeType;

typedef struct {
    int x, y;
} Point;

typedef struct {
    ShapeType type;
    Point center;
    int width, height;
    int radius;
    Point p1, p2, p3;
    char color;
} Shape;

typedef struct {
    Shape objects[MAX_OBJECTS];
    int count;
    char canvas[HEIGHT][WIDTH];
} Picture;

void init_picture(Picture *pic) {
    pic->count = 0;
    for (int i = 0; i < HEIGHT; i++) {
        for (int j = 0; j < WIDTH; j++) {
            pic->canvas[i][j] = ' ';
        }
    }
}

void draw_point(Picture *pic, int x, int y, char c) {
    if (x >= 0 && x < WIDTH && y >= 0 && y < HEIGHT) {
        pic->canvas[y][x] = c;
    }
}

void draw_line(Picture *pic, int x1, int y1, int x2, int y2, char c) {
    int dx = abs(x2 - x1);
    int dy = abs(y2 - y1);
    int sx = (x1 < x2) ? 1 : -1;
    int sy = (y1 < y2) ? 1 : -1;
    int err = dx - dy;
    int x = x1, y = y1;
