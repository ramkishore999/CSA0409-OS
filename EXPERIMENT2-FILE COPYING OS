#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>

#define SIZE 1024  // buffer size

int main() {
    int source, dest;
    char buffer[SIZE];
    ssize_t bytesRead;

    // Open source file (read-only)
    source = open("source.txt", O_RDONLY);
    if (source < 0) {
        perror("Error opening source file");
        exit(1);
    }

    // Open/Create destination file (write-only, create if not exists, truncate if exists)
    dest = open("destination.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644);
    if (dest < 0) {
        perror("Error opening/creating destination file");
        close(source);
        exit(1);
    }

    // Read from source and write to destination
    while ((bytesRead = read(source, buffer, SIZE)) > 0) {
        if (write(dest, buffer, bytesRead) != bytesRead) {
            perror("Error writing to destination file");
            close(source);
            close(dest);
            exit(1);
        }
    }

    if (bytesRead < 0) {
        perror("Error reading from source file");
    }

    // Close both files
    close(source);
    close(dest);

    printf("File copied successfully!\n");
    return 0;
}
