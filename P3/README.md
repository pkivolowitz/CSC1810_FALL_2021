# File based Mad Libs

In this program you will use:

* files to read data using `ifstream` (zybooks 9.1, for example)
* vectors to hold a number of strings (zybooks 5.2)
* `substr()` (zybooks 5.12)

## Three vectors

Declare three vectors of `string` as *global variables*. A global variable is a variable declared outside any function. The vectors will hold, respectively, verbs, subjects and adverbs.

## The data file

You will read a data file to populate vectors holding verbs, subjects and adverbs.

For example:

```text
sBob
sMary
sShe
sHe
veats
vdrinks
vthinks
vsnores
vgroans
vwalks
aloudly
aquickly
anoisily
aslowly
aquietly
```

Notice each line begins with an:

* 's' for subjects
* 'v' for verbs
* 'a' for adverbs

As you read each line (using `getline()`), test the first character to determine to which vector the remainder of the string should be appended.

## Opening a file

To read from a file, it must be opened. File operations use *streams* just like `cin` and `cout`.

Include `fstream` to get access to file streams.

Input file streams can be accessed using variables of type `ifstream`.

An `ifstream` can be opened in one of two ways:

```c++
ifstream fin("nameoffile");
```

or on two lines like:

```c++
ifstream fin;
fin.open("nameoffile");
```

## Ensuring a file stream is open

Stuff happens. Your stream might not actually open. Maybe the file is missing, for example.

Remember this: **NEVER ASSUME A FILE OPEN SUCCEEDED - ALWAYS CHECK**

Example:

```c++
ifstream fin("nameoffile");
if (fin.is_open()) {
	// all is well
	// do stuff
	// then close the file when done
	fin.close();
} else {
	// ERROR!
	// do something.
}
```

## Closing a stream

Use `close()` on the stream variable. See above for example.

## Reading a line at a time

Use `getline()` to read a whole line at a time. `getline()` returns a boolean value of `true` if all goes well. So the following is common:

```c++
while (getline(cin, s)) {
	// Read a line into string variable s from cin.
}
// There is no more to read.
```

or with an `ifstream`:

```c++
while (getline(fin, s)) {
	// Read a line into string variable s from cin.
}
// There is no more to read.
fin.close();
```

## Getting the tail of a string

The first letter of each line in the data file tells you which of the three vectors to add the rest of the string to. Use `substr()` to get access to the characters beyond a certain position.

`substr()` is found in zybooks 5.12. Note that you are allowed to leave off the second parameter to `substr()` which means "take the rest of the string."

Example:

```c++
string s("xJones");
cout << s.at(0) << " " << s.substr(1) << endl;
```

will print:

```text
x Jones
```

## Appending something to a `vector`

Use `push_back()` as described in zybooks 5.7.

Example:

```c++
vector<int> numbers;
numbers.push_back(18);
```

## Getting the size of a `vector`

Use `size()` just like with strings. `string` is kind of like a `vector<char>`.

The size of the vector is vital in choosing an entry within the vector at random.

## Choosing a member of a `vector` at random

Use `rand()` along with the `%` operator to choose an integer at random which runs from 0 to the length of the vector minus 1.

## Remember to use `srand()` just once

As in:

```c++
#include <ctime>
```

and 

```c++
srand((unsigned int) time(nullptr));
```

## MAC USERS

Ordinarily, `xcode` hides your executable program deep within the bowels of your Mac. Why? Who knows. It's Apple. I guess hiding stuff where you cannot find it is an Apple innovation. This makes using data files *very hard*.

Fortunately, you can change where `xcode` thinks it is when it debugs your programs. Follow:
`Product > Scheme > Edit Scheme`. Select `Run`. Find `Working Directory`. Check the box and then click in the custom directory text box and enter:

```text
$(PROJECT_DIR)/NAMEOFYOURPROJECT
```

If your project name is `test`, then enter:

```text
$(PROJECT_DIR)/test
```

## Placing the data file

Put the data file in the directory that holds your source code.

## Example output

```text
She eats noisily.
```

## Remember to ensure the file successfully opened

Remember to use `is_open()`.

## Remember to close the file only if opened

Remember that closing the file is important and only works if the file is truly open.

## Remember to print an error if the file cannot be opened

Include the name of the file that failed to open.

## What to turn in

Just the cpp file.
