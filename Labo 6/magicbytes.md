# Magic bytes & headers of files (file formats)

Download an image and rename it while downloading:

`wget -c https://upload.wikimedia.org/wikipedia/commons/1/18/Superman_logo.jpg -O superman.jpg`

Change LEAD to AAAA:

00000010: 0060 0000 fffe 001f 4c45 4144 2054 6563  .`........LEAD Tec
00000010: 0060 0000 fffe 001f 4141 4141 2054 6563  .`........AAAA Tec

First save the jpg to a new file:

`xxd superman.jpg > supes.hex`

Open a vim: `vim supes.hex`

Make the changes, press escape and `:wq` to save the file.

Save it again as a jpg:

`xxd -r supes.hex > supes.jpg`
