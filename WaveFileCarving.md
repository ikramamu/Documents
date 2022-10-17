
## Pre-Req:
    - A file that converts the hexa decimal to decimal
### Steps to create convert.sh file
    1. vi convert.sh
    2. #! /bin/bash   echo $(( 16#$1 ))
    3. save and exit :wq
    4. make the file executable 'chmod +x convert.sh'

## Steps for file carving wav file
1. Run xxd on file from where we need to carve wave file and grep RIFF to find the line number
    `xxd practicewav.bin| grep RIFF -A3 -B2` 
2. now convert the start line number hex to decimal
    `./convert.sh 00001e00` --> 7380
3. RIFF hexadecimal is `5249 4646`
    - Add 4 to the decimal value of line number --> 7380 + 4 = 7384
    - `00001e00: 67f7 4386 5249 4646 427f 0400 5741 5645`
4. search above RIFF hexadecimal on above line number and note next 4 bytes example
    - `00001e00: 67f7 4386 5249 4646 427f 0400 5741 5645`
    - from above, 427f 0400 si what we got.
   
5. Then, write the mirror image and convert that to decimal
    - `./convert.sh 00047f42` --> 294722
6. Now add number of bytes to reach the above value
    - `00001e00: 67f7 4386 5249 4646 427f 0400 5741 5645`
    - in this case, we add 8 to 294722 = 294730
7. finally, use dd command to create a file
    - `dd if=practicewav.bin of=carvedwav.wav skip=7684 count=294730 bs=1`
8. To compare, check md5sum of original file and carved file
    - `md5sum carvwav.wav`
    
