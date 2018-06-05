# ETag code revisions
ETag and code originally developed by [Eli Bridge](https://github.com/Eli-S-Bridge) and [Jay Wilhelm](https://github.com/jaywilhelm).
Revisions by [Ben Duggan](https://github.com/BenSDuggan).  You can email with questions at [bendugga@iu.edu](mailto:bendugga@iu.edu).  BSD_ETag_Revisions is the folder with the most up to date code.  The other folders are ones that I use to test new code or hold original versions I work on.

## **_Status: BSD_ETag_Revisions working_**

* [Original code with instillation help](https://github.com/Eli-S-Bridge/ETAG_4095_Apr2018)

## List of changes:
* Sleep function: To save battery life the board can go to sleep.  In the constants and logging parameters section slpH and slpM are hour and minute (seconds are not supported) to put the board to sleep, respectively.  wakH, wakM and wakS are the hour, minute and second to wake up, respectively.  Both of these are in 24-hour format.  Some notes on this feature:
    * The sleep function works for almost any time.  To be clear, the sleep function won't work if the main loop() takes longer than 1 minute.  So as a rule of thumb, (pollTime1 + pollTime2 + readInterval + pauseTime) <= 55 seconds.  Additionally, the sleep time and wake time should differ by more than 3 minutes.  ~~This feature only works for sleeping at night and waking up in the morning.  By this I mean that the following must hold: 0 <= wakH:wakM:wakS <= slpH:slpM:slpS <= 23:59:59 ~~
    * When the board goes to sleep the communication through the USB is terminated.  So, if the board is scheduled to sleep and you try to upload code it won't work.  To fix this the board will terminate scanning and write to the log file when the board is scheduled to sleep, but the board won't go into its deep sleep for 2 minutes after a sleep is scheduled.
   * I didn't write the actual sleep function.  I am using the [RTCZero library](https://www.arduino.cc/en/Reference/RTC).
* Reader ID: In the constants and logging parameters section you can set readerID which is prepended to the data and log file.  This is similar to file name scheme of the Gen. 2 boards.  The string can contain alphanumeric characters.
* Log file: There is a log file added to the board.  This is like the one from the Gen. 2.  The file saves when logging is started and stopped.
* Create data and log file at initial startup:  The data and log files are created immediately when the board is turned on, even if nothing is in them.
* Change file name to readerID + data/log: The file name scheme changed from just one that says datalog.txt to (readerID + "data.txt") for the data file and (readerID + "log.txt") for the log file.
