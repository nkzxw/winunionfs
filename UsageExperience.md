# Introduction #

I have tested this project in the context of building a medium size project. It appears that merging 2 paths with WinUnionFS is rather resource intensive. The bottle neck seems to be in the Dokan library, particularly slow paths are listing of directories containing numerous files.


# Details #

I have created an empty partition, formated NTFS (drive E:) and made an empty directory on it (\build) to avoid merging the Win XP root directory system files.

I merged it with my pristine environment: C:\Build\_C\pristine (also NTFS).

NOTE: Currently WinUnionFS does not work correctly if the underlying filesystems do not return filenames in case insensitive alphabetical order (such as FAT).

I mounted the result as drive P:
WinUnionFS.exe /r C:\Build\_C\pristine /w E:\build /l P

Started the build and watched using Windows Task Manager and Very Sleepy.

Windows Task Manager showed that WinUnionFS was taking 3 times as much CPU as the compiler. Very Sleepy was showing that WinUnionFS threads are mostly in DokanMain if not in some synchronization function (such RtlCriticalSection).

In debug mode I log all calls to callbacks. When looking at my logs in real time, I noticed that the log would pause for many seconds in the directory list function while the Windows Task Manager would show WinUnionFS to use 1 CPU 100%. This is why I suspect that there is a problem with the Dokan Library in this case since my code was logging nothing and the program was still very busy.
I know that this study is not flawless and I'll review a little more data such as check out the behavior of mirror.c under the same circumstances.