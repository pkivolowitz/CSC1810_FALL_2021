# Simple Vending Machine

The point of this project is to practice defining and implementing your own objects.

You will:

* use `argv` and `argc` to get a file name (zybooks 15.15 and 15.16)

* read lines from the given file to stock the vending machine (practice with `ifstream` and `stringstream`):

    `fail()`

* print a nicely formatted menu and ask the user for a selection. From `iomanip`:

    `left`

	`right`

	`setw`

    `setprecision`

	`fixed`

	and also `boolalpha`.

* based on the user's selection, vend and item or tell them the item is not available. If an item is vended, deduct one of the inventory.

## The Data

Here is a sample:

```text
Snickers	A1	3	2.00	yes
Apples		A2	5	1.00	no
Chips		B1	2	1.50	no
badline
Peanuts		B2	3	1.50	yes
Liver		B3	1	5.00	no
Brains		B4	0	5.00	no
```

Each **good** line contains a name, position, count, cost and whether or not it contains nuts.

Notice there is one bad line thrown in. Bad lines are skipped after printing a message.

Notice only whitespace separates the fields. Therefore, if you make your own data, you **cannot** have spaces in any field as it will throw off conversion from text into your object. That is: `Chips` is OK but `Potato Chips` would break the program.

Remember to ensure the data file actually opened. If it did not open successfully, print a message **and quit**.

Remember to close the file if it is opened successfully.

## The Object

You are to implement this:

```c++
struct Item {
private:
	string name;
	string position;
	int count;
	double price;
	bool contains_nuts;

public:
	string to_string();
	bool InStock();
	void Vend();
	string GetPosition();
	string GetName();
	bool Parse(string line);
};
```

Notice that the data members are marked `private`. This means that code outside the implementation of the object cannot reach the data members. Instead, code outside the implementation of the object must go through "getters" such as `GetPosition()`.

Data members are often made private so that the programmer can tightly control how the members are accessed. In this case, for example, because the data members are private code outside the implementation cannot change the value of the data members because the programmer of `Item` prevented them from doing so.

### GetPosition()

Simply returns the `position`.

### GetName()

Simply returns the ``name`.

### InStock()

Returns true if `count` is greater than 0.

### Vend()

Reduces `count` by one. Note that you must already have ensured `count` is greater than zero before calling this method.

### to_string()

Formats the data nicely putting the results into a string that is returned.

`position` is printed first followed by the name which is left justified in a field of 10 spaces.

Next comes the `count` which is right justified and put in a field of 4 spaces.

Then comes the `price` which must be printed with exactly two decimal places even if the values are zero.

Lastly, `contains_nuts` is printed using `true` or `false` not 1 or 0.

Use a `stringstream` to get access to all the nice formatting features of a `stream` then turn the `stringstream` into a `string` for the `return`. See zybooks 9.4.

Here is a sample of what `to_string()` should produce:

```text
B2 Peanuts      3 1.50 true
```

Notice the name is left justified. Notice the price shows two decimal places including a trailing zero.

### Parse()

This method takes an entire line from the data file and parses it into the distinct data members or returns `false` if it cannot. Note that this implies you're to use `getline` to get whole lines of input. You've done this before.

To get the extraction operator (`>>`) you must convert the `string` to a `stringstream` like so:

```c++
string s("This is a lovely string");
stringstream ss(s); // ss is a stringstream initialized with the lovely string.
string w;
ss >> w;
cout << w;         // This
```

You should chain together all the extractions on one line like:

```c++
ss >> foo >> bar >> fum >> foe >> fi;
```

Then, quiz the `stringstream` to see if the extractions caused any errors.

```c++
if (ss.fail()) {
	// print an error message and return false from Parse()
}
```

The `stringstream` should be a local variable inside `Parse()` so you get a fresh `stringstream` each time `Parse()` is called.

One final note... you must turn "true" and "false" in the data into a boolean yourself. The extraction operator doesn't know how to deal with "true" and "false" when asked to extract to a `bool`. You must extract to a `string` first.

## Printing bool With True and False

Apparently not in the zybook, you can easily print bools as `true` or `false` using `boolalpha`.

```c++
cout << false << " " << boolalpha << false << endl;
```

prints:

```text
0 false
```

## Reading the Data

If no command line argument is present, print an error message and quit the program.

You are encouraged to encapsulate reading the data file into a function. After reading the data file, print the number of items read. If the number of items read is zero, print an error message and quit the program.

Each `Item` successfully read should be added to a `vector` representing your inventory.

## Quitting a Program

When quitting a program you can either call `exit()` or `return` from `main()`.

With each of these, there is a returned value. By convention, if anything went wrong in your program you should return or exit with a non-zero value. If all is well, exit or return with 0.

## Main Loop

Print the current inventory.

Print a prompt.

Get user input. Make all user input upper case.

If the user input is Q, quit the program.

Otherwise, search your inventory and if you match a `position`, check to see if there are any of that
item in stock. If not, print an error. If the item is in stock, `Vend()` that item and print a nice message.

### There Is No `toupper()` For `string`

Write this yourself.

## Sample Runs

### Good Run

```text
% ./a.out stock.txt                      
Failed extraction on line containing: badline
Items read: 6
Current Inventory:
A1 Snickers     3 2.00 true
A2 Apples       5 1.00 false
B1 Chips        2 1.50 false
B2 Peanuts      3 1.50 true
B3 Liver        1 5.00 false
B4 Brains       0 5.00 false
Selection (or "Q"): B3
Enjoy your Liver

Current Inventory:
A1 Snickers     3 2.00 true
A2 Apples       5 1.00 false
B1 Chips        2 1.50 false
B2 Peanuts      3 1.50 true
B3 Liver        0 5.00 false
B4 Brains       0 5.00 false
Selection (or "Q"): B3
Sorry! There is no stock at position: B3

Current Inventory:
A1 Snickers     3 2.00 true
A2 Apples       5 1.00 false
B1 Chips        2 1.50 false
B2 Peanuts      3 1.50 true
B3 Liver        0 5.00 false
B4 Brains       0 5.00 false
Selection (or "Q"): q
% 
```

This sample run shows how the quantity of *B3* was reduced from 1 to 0 and then when the user asked for *B3* again, they were told there was no more stock. Also, note that *q* worked for *Q*.

Notice also the error message indicating one of the lines of the data file was no good.

### No Command Line Argument

```text
% ./a.out
Must specify inventory file.
%
```

### Bad Command Line Argument

```text
% ./a.out badfilename    
Failed to open file: badfilename
% 
```

## Work Rules

Work is to be done solo.

## What To Hand In

Just one .cpp file.

## Setting Expectations

Without comments, my implementation is 131 lines long. This isn't a contest. I provide this information only to set your expectations. If you have written 132,451 lines, for example, you've written too much.

