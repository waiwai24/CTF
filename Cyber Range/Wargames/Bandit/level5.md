# Goal

The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:

- human-readable
- 1033 bytes（字节） in size
- not executable



# Ideas

use `ls` we find there have 20 directory, but the file size is 1033bytes.

use `find . -size 1033c`:

./maybehere07/.file2

use `cat ./maybehere07/.file2`:

P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU