# SmiTrigger
C++ SMI trigger

test

#include <sys/io.h>
#include <stdio.h>
#include <stdlib.h>

int main() {
    // Request permission to access port 0xB2
    if (ioperm(0xB2, 1, 1)) {
        perror("ioperm");
        return 1;
    }

    // Write to port 0xB2 to trigger SMI
    printf("Triggering Software SMI...\n");
    outb(0x00, 0xB2); // 0x00 is a sample command, depends on BIOS
    
    // Release permission
    ioperm(0xB2, 1, 0);
    return 0;
}
