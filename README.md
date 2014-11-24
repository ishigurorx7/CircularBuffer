CircularBuffer
==============

1 Introduction
==============

This repository provides simple circular buffer routines and their test program for mbed LPC1768 board.
The circular buffer and their utility routines are defined in cirucluarBuffer.h header, and their initialization routine is defined in circularBuffer.cpp file. This program supports en-queue and de-queue features only, and these routine returns un-success value when queue is full detected by the en-queue routine or queue is empty by the de-queue routine. Those routine are no secure when it's accessed by the multiple tasks such as ISR, but there are wrapper functions of en-queue and de-queue defined in main.cpp named 'myBufferEnque() and myBufferDeque(), those routine, uses mutex operation (mutual exclusive operation) to protect critical regions before calling en-queue and de-queue functions defined on the 'circularBuffer.h'.

2 Test method (three tickers)
=============================

  The test program consists of following three tickers (interrupt driven tasks that are periodically called by timer tick):

* myBufferEnque:  En-queueing single element from buffer every 10 ms
* myBufferDeque:  De-queueing single element from buffer every 15 ms
* bufUsageMeter:   Display LED(s) to shows usage amount of the buffer 85 ms

3 Test sequence
===============

Here is the sequence of circular buffer test:

* Diagnostics mbed (LPC1768)'s mounted 4 LEDs by displaying few different patterns. It takes 2-4 seconds.
* Kick off 3 tickers mentioned above, and operator can see the state by seeing 4 LED's and console output if you setup the USB-console setups.
* Whenever en-queue or de-queue encounters their non-programmable conditions; buffer full or empty, their ticker's interval time amount is switched between myBufferEnque and myBufferDeque so that program can continue be executed.
 
4 Notes
=======

This program was tested on LPC1768 using binary created by the mbed online compiler, and not tested with binary from GNU GCC tool chain yet.
The en-queue and de-queue core routines should be organized as library so that other application can use it.
