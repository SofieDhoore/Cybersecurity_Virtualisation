# WIFI Captures

First we have to crack a zip-file with John the Ripper. Open a terminal where the zip-file is located and use the following commands:

`sudo zip2john pass.zip > password.txt`

`ls` to see the new text-file.

`sudo john password.txt`
