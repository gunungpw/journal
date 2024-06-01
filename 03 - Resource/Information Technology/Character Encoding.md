# Character Encoding

By the end of this video, you'll learn how we can represent the words, numbers, emojis, and more we see on our screens from only these 256 possible values. It's all thanks to character encoding. Character encoding is used to assign our binary values to characters so that we as humans can read them. We definitely wouldn't want to see all the texts in our emails in webpages rendered in complex sequences of zeros and ones. This is where character encodings come in handy. You can think of character encoding as a dictionary. It's a way for your computers to look up which human character should be represented by a given binary value. The oldest character encoding standard used is ASCII. It represents the English alphabet, digits, and punctuation marks. The first character in the ASCII to binary table, a lowercase a, maps to 01100001 in binary. This is done for all the characters you can find in the English alphabet, as well as numbers and some special symbols. The great thing with ASCII was that we only needed to use 127 values out of our possible 256. It lasted for a very long time, but eventually, it wasn't enough. Other character encoding standards were created to represent different languages, different amounts of characters, and more. Eventually, they would require more than 256 values we are allowed to have. Then came UTF-8, the most prevalent encoding standard used today. Along with having the same ASCII table, it also lets us use a variable number of bytes. What do I mean by that? Think of any emoji. It's not possible to make emojis with a single byte since we can only store one character in a byte. Instead, UTF-8 allows us to store a character in more than one byte, which means endless emoji fun. UTF-8 is built off the Unicode Standard. We won't go into much detail, but the Unicode Standard helps us represent character encoding in a consistent manner. Now that we've been able to represent letters, numbers, punctuation marks, and even emojis, how do we represent color? Well, there are all kinds of color models. For now, let's stick to a basic one that's used in a lot of computers, RGB or red, green, and blue model. Just like the actual colors, if you mix a combination of any of these, you'll be able to get the full range of colors. In computer land, we use three characters for the RGB model. Each character represents a shade of the color, and that then changes the color of the pixel you see on your screen. With just eight combinations of zeros and ones, we're able to represent everything that you see on your computer from a simple letter a to the very video that you're watching right now. Very cool.