Current Events - 150 Points
===========================
This challenge uses local file inclusion (LFI) and a little bit of php knowledge. One thing you should realize is that when you click any links on reader.php page, it updates the GET parameter article to have a <article-name>.php. If you visit /<article-name>.php you'll see that page shows up. So reader.php just seems to be including whatever file you tell it.

The next step is to check the URL but without any files, just /, or the root of the URL. This will show a file listing and flag.php looks like it would be where the answer is! But when viewing that page it gives a taunting message instead of the flag. So if you go back to the file listing, there is a file called flag.php.txt which is the source of flag.php. There is still no flag here, but we see it opens a file in one directory up called flag.txt and prints that if two conditions are true. One is that a GET parameter 'winning' is set to 'yes'. The other is that $val is set, or exists as a variable. But we don't see $val anywhere else in flag.php so it would seem that this must be initialized in a file somewhere else. So this should lead you to try going to /reader.php?article=flag.php&winning=yes. This will print out the flag.txt that flag.php was reading in and printing out. This is because $val is declared in reader.php, so it is a variable that exists and also the GET parameter of winning is set to 'yes' so all checks pass and flag.php is nice this time and gives us the flag.

There is also a potential for directory traversal by making article=../flag.txt. However, the script reader.php disallows periods at the beginning and slashes anywhere in the filename. But it does not URL decode the given parameters, so it may be possible to get the flag by URL encoding ../flag.txt, however this was not tested. It was really intended to get the flag the other way, but this might be another possible way to get the flag.

Flag: **RC3-PHPISFUN-1016397**