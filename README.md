It is a null modem / loop back kernel mode driver providing full duplex communication and handshaking signals.

It creates virtual serial ports pair that appears same as the real once to the application software.

##Use cases
- Fully automate Junit testing and continuous integration
- Custom protocols development and debugging
- Serial port based application's scalability and performance testing
- Can be used as a medium for inter/intra-process communication
- Serial port communication sniffer or test sniffer application itself
- GPS coordinates and robotics emulator/simulator
- Application development when hardware is still not available
- Test/debug different serial port device emulators like modem and faxes etc
- Testing high level user space drivers
- Segregate hardware issues from software bugs quickly during product development
- Multiple producers/consumers sharing same channel application design development/testing
- Development cost reduction across team
- Add new functionality to existing application by inserting plugin between serial hardware and existing application   
  [hw device]--[hw comport]--[plugin software (process data)]--[virtual comport]--[Existing application]
- Write user space drivers for ex; multiplex several virtual connections on single physical GSM Modem line
- Protocol converter engine software
- Capture the output of Guest OS on virtual machine and re-direct it to a terminal program

##Features
- Create standard, loopback or custom pinout connected serial devices
- Software, hardware and no flow controls emulation
- Parity, frame, overrun and line break events emulation
- Control signals (RTS,DTR,CTS,DCD,RI,LOOP,DSR) and all serial port settings
- Ring indicator line signal emulation
- Create/destroy virtual serial ports dynamically directly from your application without reboot
- Operating system specific serial port APIs and IOCTL supported
- Serial ports can be deleted even when opened by an application (useful in automated testing)
- Plug and play device emulated
- Ports can be created automatically at system boots
- Create large number of serial ports
- Speed is directly proportional to your software/hardware configuration
- Virtual box and VMware virtual machine supported
- Multithreaded environment supported
- Mismatched line settings causes garbled data as in real life and appropriate error event generation
- API to control virtual ports directly from your application

##Demo application


##Build and Run
See instructions in operating system specific directory for build scripts, udev rules, steps to install etc.

##Pins mapping

There are three connection configurations supported by this driver.

####Standard nulll modem
```
 tty2com0            tty2com1
     RXD -------------- TXD
     TXD -------------- RXD
     DTR -------------- DSR,DCD
 DSR,DCD -------------- DTR
     CTS -------------- RTS
     RTS -------------- CTS
     GND -------------- GND
```
- TX of local port is connected to RX of remote port and vice-versa
- DTR of the local port is connected to DSR and DCD of the remote port
- RTS of the local port is connected to CTS of the remote port

####Standard loop back
```
   tty2com0            
     RXD -----]
     TXD -----]
     
     DTR -----]
 DSR,DCD -----]
 
     RTS -----]
     CTS -----]
```
- TX of local port is connected to RX of local port and vice-versa
- DTR of the local port is connected to DSR and DCD of the local port
- RTS of the local port is connected to CTS of the local port

####Custom

The local pins RTS, DTR, DCD, DSR and RI can be connected to local/remote pins as desired.

*Custom null modem :*   
```
 tty2com0            tty2com1
     RXD -------------- TXD
     TXD -------------- RXD
     RTS -------------- DSR,DCD
 DSR,DCD -------------- DTR
     CTS -------------- RTS
     GND -------------- GND
```

*Custom loop back :*   
```
   tty2com0            
     RXD -----]
     TXD -----]
     
     RTS -----]
 DSR,DCD -----]
 
     DTR -----]
     CTS -----]
```

You can create all the configurations as per the application requirements.

