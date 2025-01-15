//Gisa
#include <GL/glut.h> 
#include <iostream>
#include <cmath>

// Variables for transformations
float cloudY = 5.0f;
float cloudScale = 1.0f; // Scale factor for the cloud
float sunX = 6.0f;
float sunY = 6.0f;
float rotationAngle = 0.0f;
float sunRotationAngle = 0.0f;
bool showAxes = true; // Toggle for Cartesian axes
float TreeX = 5.0f; // X position of the tree
float TreeZ = 0.0f; // Z position of the tree

// Camera position
struct CameraPosition {
    float camPosX = 0.0f;
    float camPosY = 10.0f;
    float camPosZ = 20.0f;
    float targetX = 0.0f;
    float targetY = 0.0f;
    float targetZ = 0.0f;
    float radius = 20.0f; // Camera distance from the target
    float angle = 0.0f; // Camera rotation angle
    bool rotate = false; // Status of camera rotation
} pos;

// Initialize lighting
void initLighting() {
    GLfloat ambientLight[] = {0.2f, 0.2f, 0.2f, 1.0f};
    GLfloat diffuseLight[] = {0.8f, 0.8f, 0.8f, 1.0f};
    GLfloat lightPosition[] = {10, 4, 0.0f, 1.0f};

    glEnable(GL_LIGHTING);
    glEnable(GL_LIGHT0);
    glLightfv(GL_LIGHT0, GL_AMBIENT, ambientLight);
    glLightfv(GL_LIGHT0, GL_DIFFUSE, diffuseLight);
    glLightfv(GL_LIGHT0, GL_POSITION, lightPosition);

    glEnable(GL_COLOR_MATERIAL);
    glColorMaterial(GL_FRONT, GL_AMBIENT_AND_DIFFUSE);
}

// Draw Cartesian axes
void drawAxes() {
    if (!showAxes) return; // Skip drawing if axes are hidden

    glDisable(GL_LIGHTING); // Disable lighting for axes
    glBegin(GL_LINES);
        // X-axis (red)
        glColor3f(1.0f, 1.0f, 1.0f);
        glVertex3f(-10.0f, 0.0f, 0.0f);
        glVertex3f(10.0f, 0.0f, 0.0f);

        // Y-axis (green)
        glColor3f(1.0f, 1.0f, 1.0f);
        glVertex3f(0.0f, -10.0f, 0.0f);
        glVertex3f(0.0f, 10.0f, 0.0f);

        // Z-axis (blue)
        glColor3f(1.0f, 1.0f, 1.0f);
        glVertex3f(0.0f, 0.0f, -10.0f);
        glVertex3f(0.0f, 0.0f, 10.0f);
    glEnd();
    glEnable(GL_LIGHTING); // Re-enable lighting
}

// Draw octahedron
void drawOctahedron() {
    glPushMatrix();
    glScalef(3.2f, 3.2f, 3.2f); // Increase the size of the octahedron
    glColor3f(1.0f, 0.8f, 0.0f);
    glutSolidOctahedron();
    glPopMatrix();
}

// Draw solid cube as the floor
void drawFloor() {
    glPushMatrix();
    glScalef(100.0f, 3.5f, 100.0f); // Scale cube to make it a floor
    glTranslated(0,-0.5,0);
    glColor3ub(246,215,176); 
    glutSolidCube(1.0f);
    glPopMatrix();
}
//wanda
// Draw tree (coconut tree)
void drawTree(float x, float z) {
    glPushMatrix();
    glTranslatef(x, 0.55f, z); // Adjust position above the floor

    // Draw trunk
    glColor3f(0.55f, 0.27f, 0.07f);
    glPushMatrix();
    glScalef(0.2f, 1.5f, 0.2f);
    glutSolidCube(1.0f);
    glPopMatrix();

    // Draw leaves
    glColor3f(0.0f, 0.8f, 0.0f);
    for (int i = 0; i < 4; i++) {
        glPushMatrix();
        glTranslatef(0.0f, 0.75f, 0.0f);
        glRotatef(i * 90, 0.0f, 1.0f, 0.0f);
        glScalef(1.5f, 0.1f, 0.3f);
        glutSolidCube(1.0f);
        glPopMatrix();
    }

    // Draw coconuts
    glColor3f(0.5f, 0.35f, 0.05f);
    glPushMatrix();
    glTranslatef(0.25, 0.6f, 0);
    glutSolidSphere(0.1f, 20, 20);
    glPopMatrix();

    glPopMatrix();
}

// Draw cloud with specific design
void drawCloud() {
    glPushMatrix();
    glTranslatef(0.0f, cloudY, 0.0f);
    glScalef(cloudScale, cloudScale, cloudScale); // Apply scale

    // Center sphere
    glColor3f(0.8f, 0.8f, 0.8f);
    glutSolidSphere(1.0f, 20, 20);

    // Left sphere
    glPushMatrix();
    glTranslatef(-1.2f, 0.0f, 0.0f);
    glutSolidSphere(0.8f, 20, 20);
    glPopMatrix();

    // Right sphere
    glPushMatrix();
    glTranslatef(1.2f, 0.0f, 0.0f);
    glutSolidSphere(0.8f, 20, 20);
    glPopMatrix();

    // Upper left sphere
    glPushMatrix();
    glTranslatef(-0.8f, 0.6f, 0.0f);
    glutSolidSphere(0.6f, 20, 20);
    glPopMatrix();

    // Upper right sphere
    glPushMatrix();
    glTranslatef(0.8f, 0.6f, 0.0f);
    glutSolidSphere(0.6f, 20, 20);
    glPopMatrix();

    glPopMatrix();
}

// Draw sun
void drawSun() {
    glPushMatrix();
    glTranslatef(sunX, sunY, 0.0f);
    glRotatef(sunRotationAngle, 0.0f, 0.0f, 1.0f); // Rotate around its own center
    glColor3ub(220,220,220);
    glutSolidSphere(1.5f, 20, 20);
    glPopMatrix();
}
//bubu
// Display callback
void display() {
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glLoadIdentity();

    // Update camera position based on rotation status
    pos.camPosX = pos.radius * sin(pos.angle); // X position
    pos.camPosZ = pos.radius * cos(pos.angle); // Z position

    gluLookAt(
        pos.camPosX,
        pos.camPosY,
        pos.camPosZ,
        pos.targetX, pos.targetY, pos.targetZ,
        0.0, 1.0, 0.0
    );

    drawAxes();
    drawFloor();

    glPushMatrix();
    glRotatef(rotationAngle, 0.0f, 1.0f, 0.0f);
    drawOctahedron();
    glPopMatrix();

    drawCloud();
    drawSun();

    // Draw main tree
    drawTree(TreeX, TreeZ);

    // Draw additional trees
    drawTree(-3.0f, -3.0f);
    drawTree(3.0f, -3.0f);
    drawTree(-3.0f, 3.0f);
    drawTree(3.0f, 3.0f);

    glutSwapBuffers();
}

// Keyboard callback
void keyboard(unsigned char key, int x, int y) {
    switch (key) {
        case 'w': cloudY += 0.5f; break;
        case 's': cloudY -= 0.5f; break;
        case 'r': rotationAngle += 5.0f; break;
        case 'x': showAxes = !showAxes; break; // Toggle axes visibility
        case 'a': TreeX -= 0.5f; break; // Move tree left
        case 'd': TreeX += 0.5f; break; // Move tree right
        case 'z': TreeZ -= 0.5f; break; // Move tree forward
        case 'c': TreeZ += 0.5f; break; // Move tree backward
        case '+': pos.radius += 1.0f; break; // Increase camera radius
        case '-': pos.radius -= 1.0f; break; // Decrease camera radius
        case 'q': cloudScale += 0.1f; break; // Increase cloud scale
        case 'e': cloudScale -= 0.1f; break; // Decrease cloud scale
        case 't': pos.angle += 0.1f; break; // Rotate camera to the right
        case 'g': pos.angle -= 0.1f; break; // Rotate camera to the left
    }
    glutPostRedisplay();
}

// Timer callback for animations
void timer(int value) {
    sunRotationAngle += 1.0f; // Rotate the sun
    if (sunRotationAngle >= 360.0f) sunRotationAngle -= 360.0f;

    glutPostRedisplay();
    glutTimerFunc(16, timer, 0); // Approximately 60 FPS
}

// Reshape callback
void reshape(int w, int h) {
    glViewport(0, 0, w, h); // Set the viewport to the new window dimensions
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    gluPerspective(45.0, (float)w / (float)h, 1.0, 100.0); // Set perspective projection
    glMatrixMode(GL_MODELVIEW); // Switch back to model view matrix
}

// Main function
int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH);
    glutInitWindowSize(800, 600);
    glutCreateWindow("Kelompok 6 Piramida Mesir Malam Hari");

    glEnable(GL_DEPTH_TEST);
    initLighting();

    glutDisplayFunc(display);
    glutReshapeFunc(reshape);
    glutKeyboardFunc(keyboard); // Register keyboard callback
    glutTimerFunc(0, timer, 0); // Start timer for animations

    glutMainLoop();
    return 0;
}.
