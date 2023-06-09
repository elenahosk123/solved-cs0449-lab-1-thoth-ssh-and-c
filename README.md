Download Link: https://assignmentchef.com/product/solved-cs0449-lab-1-thoth-ssh-and-c
<br>
<a href="https://en.wikipedia.org/wiki/Thoth">thoth</a> is a computer in the CS building. It’s hooked up to Pitt’s network, but the CS department manages it and puts software on it useful for this and other courses.

By logging into thoth remotely, you don’t have to worry about setting up a C compiler on your own computer.

<strong>ssh</strong> is a way of running commands on a remote machine. It’s like your command line, but the console is connected across the internet instead of to your own computer.

Later projects will also use features only available on thoth. <strong>So please don’t try to compile your projects on your local machine.</strong>

<h2>1. Getting connected and set up</h2>

Nothing will show up when you type your password. That’s normal.

When you log in, don’t worry about the “unauthorized access” message. You <em>are</em> supposed to be logging in. <em>You’re authorized &#x1f609;</em>

<h3>Windows users</h3>

You need to get an ssh client, <a href="https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html">like PuTTY</a> (use the 64-bit installer). Run it, and use thoth.cs.pitt.edu as the address.

Say “Yes” to the certificate, give your username (lowercase) and password, and you’re in!

<h3>Mac users</h3>

Open up Terminal (⌘+Space, type “terminal”, hit enter). Then run:

$ ssh <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="9ce5f3e9eee9eff9eef2fdf1f9dce8f4f3e8f4b2ffefb2ecf5e8e8b2f9f8e9">[email protected]</a>

Say “Yes” to the certificate, give your username (lowercase) and password, and you’re in!

If you can’t log in, please ask the TA for help. If you are sure you’re putting in your username in lowercase, and the right password, please email me and CC Dr. Khattab (<a href="/cdn-cgi/l/email-protection#44372f2c25303025260427376a342d30306a212031"><span class="__cf_email__" data-cfemail="4d3e26252c39392c2f0d2e3e633d24393963282938">[email protected]</span></a>). He’s the thoth administrator.

<h2>2. Common UNIX commands</h2>

Here’s a quick reference guide to refer back to.

<ul>

 <li>pwd – display the current directory</li>

 <li>cd dirname – change current directory to dirname

  <ul>

   <li>cd .. moves up one directory</li>

   <li>cd ~ goes to your home directory</li>

   <li>cd – toggles back and forth between the last two directories you were in</li>

  </ul></li>

 <li>ls – list all files/folders in current directory

  <ul>

   <li>ls dirname will list files/folders in the directory dirname</li>

  </ul></li>

 <li>mv source dest – move or rename a file

  <ul>

   <li>source is the file you want to move/rename</li>

   <li>dest is the new place/name</li>

  </ul></li>

 <li>cp source dest – copy a file from source to dest</li>

 <li>mkdir name – make a new directory named name</li>

 <li>touch filename – make an empty file named filename</li>

 <li>cat filename – display contents of text file filename</li>

 <li>less filename – view contents of text file filename – good for longer files

  <ul>

   <li>press q to exit!</li>

  </ul></li>

 <li>rm filename – delete (“remove”) filename</li>

 <li>rmdir dirname – delete an EMPTY directory named dirname</li>

</ul>

<h2>Where are we?</h2>

When you log in, you are placed in your <strong>home directory.</strong>

<ol>

 <li>Try using pwd; it’ll show you the full path of your home directory.

  <ul>

   <li>Your home directory can be referred to as ~ in many commands as a typing shortcut.</li>

  </ul></li>

 <li>Try using ls. It will list the files and directories.

  <ul>

   <li>Your private directory is what you want to do your work in. No one else can see it.</li>

  </ul></li>

 <li>Do cd private and you’ll move into that directory.

  <ul>

   <li>pwd again, and you’ll see that your directory changed.</li>

   <li>You can use cd .. to move up one directory.</li>

   <li>You can use cd ~ to go to your home directory.</li>

  </ul></li>

</ol>

<h2>3. Setting up your ~/.bash_profile a little bit</h2>

bash is what you’re using right now – the thing you type commands into. .bash_profile is the configuration file for bash.

<ol>

 <li>Do cd ~.

  <ul>

   <li>This goes back to your home directory.</li>

  </ul></li>

 <li>Do chmod u+rw .bash_profile</li>

 <li>Now let’s edit it: nano .bash_profile

  <ul>

   <li>nano is a very simplistic text editor that runs inside the terminal. The controls are at the bottom of the screen – something like ^X means press Ctrl+X. (Mac users, use the actual control key.)</li>

  </ul></li>

 <li>Scroll down to the bottom of the file. There, you’ll see:</li>

</ol>

5.   # Define your own private shell functions and other commands here

<ol>

 <li>Use the arrow keys to put your cursor after that line. Now, copy and paste this <strong>exactly:</strong>

  <ul>

   <li>In putty, you can right click and paste</li>

   <li>In Terminal on a mac, ⌘V will paste</li>

  </ul></li>

</ol>

7.   if [ “$HOSTNAME” = “thoth.cs.pitt.edu” ]; then8.       source /opt/set_specific_profile.sh;9.   fi

<ol>

 <li>If you want a nice-looking terminal prompt like I have, find the line that starts with export PS1, and replace it with this:</li>

</ol>

11. export PS1=”[[ 33[1;32m]h[ 33[0m] [ 33[1;34m]w[ 33[0m]]: “;

<ol>

 <li><strong>Now hit </strong><strong>Ctrl+O</strong> and hit enter to save. Then hit Ctrl+X to exit.</li>

 <li>Do source .bash_profile</li>

</ol>

<ol start="14">

 <li>Try doing man open. If you see this, yay! Hit q to exit.</li>

</ol>

If you see No manual entry for open then you messed up somewhere. <strong>Ask for help!</strong>

<h2>4. Making a “hello world” program</h2>

Organization is good. Don’t just do all your work in private. Make a directory for your 449 work!

<ol>

 <li>Make sure you are in your private directory. Then do mkdir cs449.</li>

 <li>Do ls, and you should now see cs449 listed. cd into cs449.</li>

 <li>Now make a lab1 directory inside your cs449 directory, and cd into <em>that.</em></li>

 <li>Let’s make a C file. Do nano lab1.c. This will create a new file and open it in nano.</li>

 <li>Now <strong>type the following into the editor.</strong></li>

</ol>

6.   // Your Name (username)7.   #include &lt;stdio.h&gt;8.   9.   int main() {10.     printf(“Hello World!
”);11.     return 0;12. }

<ol>

 <li>Save the file and exit nano.</li>

 <li>Now, compile it like so:</li>

</ol>

15. gcc –std=c99 -Wall -Werror -o lab1 lab1.c

If you did it right, it should print nothing. With UNIX, “no news is good news.” Successful commands will usually be quiet. But if you ls, you should now see a new file, lab1. This is your executable!

<ol>

 <li>Type ./lab1 to run your program. It should say “Hello, World!”</li>

</ol>