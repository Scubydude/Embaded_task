#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>

#define GPIO_EXPORT "/sys/class/gpio/export"
#define GPIO_UNEXPORT "/sys/class/gpio/unexport"
#define GPIO_DIR "/sys/class/gpio/gpio%d/direction"
#define GPIO_VAL "/sys/class/gpio/gpio%d/value"

void writeToFile(const char *path, const char *value) {
    int fd = open(path, O_WRONLY);
    if (fd < 0) {
        perror("Error opening file");
        exit(EXIT_FAILURE);
    }
    write(fd, value, strlen(value));
    close(fd);
}

int main() {
    int gpio = 17; // GPIO pin number
    char path[50];

    // Export the GPIO
    writeToFile(GPIO_EXPORT, "17");

    // Set the GPIO direction to "out"
    sprintf(path, GPIO_DIR, gpio);
    writeToFile(path, "out");

    // Blink the LED
    for (int i = 0; i < 10; i++) {
        sprintf(path, GPIO_VAL, gpio);
        writeToFile(path, "1");
        sleep(1);
        writeToFile(path, "0");
        sleep(1);
    }

    // Unexport the GPIO
    writeToFile(GPIO_UNEXPORT, "17");
    return 0;
}
