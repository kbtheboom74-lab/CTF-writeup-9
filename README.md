# CTF-writeup-9



CTF Writeup: Nice netcat...
This is one of those challenges where you connect to a server and it just... doesn't speak English at you. No prompt, no instructions on the wire, just noise until you figure out what the noise actually is.

How I Approached It
Connected with nc <host> <port> exactly like the challenge description tells you to, and instead of a normal greeting or menu I got hammered with a long, continuous wall of numbers separated by spaces — hundreds of them, scrolling past in one connection. No labels, no line breaks that meant anything, just digits.

What Was Actually Going On
Instead of panicking at the wall of numbers, I looked at the actual range they fell in — mostly two- and three-digit values sitting somewhere between roughly 30 and 120. That range is a dead giveaway for ASCII codes, since standard printable ASCII characters (letters, digits, punctuation, spaces) all live in the 32–126 decimal range. So this wasn't encryption at all — the server was just sending the flag one character at a time as its decimal ASCII value instead of as literal text, which is a cheap but common way challenges dress up plain output to look scarier than it is.

How I Solved It
I copied the full run of numbers out of the terminal, then wrote a short Python script that split the string on whitespace, ran chr() on each individual number, and joined all the resulting characters back together into one string. Ran it once and the flag printed out cleanly. You could just as easily skip the script entirely and paste the number list into an online decimal-to-ASCII converter — either way gets you the same readable output in seconds.

What I Took Away From It
Whenever a CTF throws a wall of numbers at you and they're clustered in that roughly 32–126 range, your first instinct should be "ASCII," not "encryption." It's one of the most common, laziest, and most effective ways challenges disguise perfectly plain text — no math to break, just a representation to translate back.
