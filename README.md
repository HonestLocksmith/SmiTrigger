# SmiTrigger
C++ SMI trigger Linux (root)

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


windows user mode (python)

# Using inpoutx64.dll (place in same folder or system32)
from ctypes import windll, c_ubyte

inpout = windll.LoadLibrary("inpoutx64.dll")
inpout.Out32(0xB2, 0x00)  # Triggers SMI with code 0x00
