# Bubble Sort

This project is a gentle introduction to the use of `vector`. You will implement a Bubble Sort and use it to sort of `vector` of randomly assigned integers.

## Other new material

In this project you'll also make some minimal use of `<iomanip>`. You can find `<iomanip>` in zybooks chapter 9.3. You will need to write a `Print()` function that prints 8 integers per row. It must look like this:

```text
   37398    7356   47732    9029   51360   38333   44473   27337
   59125    2404   46053   42854   17711    4781   17852   21023
   35270   24283   40907   54434    6270   63609    2087   17972
   11757    9577    6988    9611   54823   46488   18479    5355
   28272   43790   16677   62841    4703   18368   45685   15313
   21659   40974     287   42367   15895   37544   30366   40176
   23500   56459   11594   25471   22452    2606   25956   41839
    3058   18652   39085   36935   17253   49838   21578   63671
```

rather than this:

```text
 37398 7356 47732 9029 51360 38333 44473 27337
 59125 2404 46053 42854 17711 4781 17852 21023
 35270 24283 40907 54434 6270 63609 2087 17972
 11757 9577 6988 9611 54823 46488 18479 5355
 28272 43790 16677 62841 4703 18368 45685 15313
 21659 40974 287 42367 15895 37544 30366 40176
 23500 56459 11594 25471 22452 2606 25956 41839
 3058 18652 39085 36935 17253 49838 21578 63671
```

The features afforded by `<iomanip>` make this possible.

## Starter code

I [provide starter code](./starter_code.zip) which indicates precisely where you are to write code. Use the link just given to download the zip file. Below is a copy of the starter code (which may or may not be current) for discussion purposes.

```c++
/*	Write the comment listing authors and program summary
*/

#include <iostream>
#include <iomanip>
#include <vector>
#include <ctime>

using namespace std;

/*	Initialize() - this function... write big picture comment here.

	Parameters:
	vector<int> &		A reference to the vector of int to create
	const int			How many ints to add to the vector
	const int			The largest random value to include i.e.
						use this value along with '%' to limit the
						range of random numbers.

	Returns:
	void				No return value
*/

void Initialize(vector<int> & values, const int vector_size, const int max_value) {
	// You write this
}

/*	Write function comment in style of above.
*/

void Print(string title, vector<int> & values) {
	// You write this
}

/*	Write function comment in style of above.
*/

void BubbleSort(vector<int> & values) {
	// You write this
}

int main() {
	const size_t vector_size = 64;
	const int max_value = 65536;
	vector<int> values;

	srand((unsigned int) time(nullptr));
	Initialize(values, vector_size, max_value);
	Print("Before", values);
	BubbleSort(values);
	Print("After", values);

	return 0;
}
```

### Ampersands `&` are critical

While the `&` are not explained yet, they are critical. **Ensure that you do not remove them.**

### Commenting is graded

I have modeled a partial function comment and you are to complete it as well as to write others as indicated.

A function comment's text should provide the *big picture*. In terms of strategy versus tactics, the function comment describes strategy. Comments mixed in which code describes tactics.

### `main()` is to be used as-is

Your job is to write only what is indicated. `main()` isn't be to modified.

## Bubble sort

A bubble sort is an **inefficient** method of sorting whereby the collection is iterated over repeatedly, stopping when a complete iteration finds no new work to do.

In each iteration, the current value is compared to the next value. If the current value is larger than the next value, the two are exchanged. That is, if `index` is the loop variable, then `values[index]` is compared to `values[index + 1]`. This gives rise to a small complication which is left to you to ponder (think *Index out of Range* error).

You are to count (and print), the number of iterations as well as the number of exchanges.

## Sample output

Note that due to random values, your output will be different.

```text
Vector of size: 64 created.
Before
   37398    7356   47732    9029   51360   38333   44473   27337
   59125    2404   46053   42854   17711    4781   17852   21023
   35270   24283   40907   54434    6270   63609    2087   17972
   11757    9577    6988    9611   54823   46488   18479    5355
   28272   43790   16677   62841    4703   18368   45685   15313
   21659   40974     287   42367   15895   37544   30366   40176
   23500   56459   11594   25471   22452    2606   25956   41839
    3058   18652   39085   36935   17253   49838   21578   63671
Bubble sort complete:
Iterations: 53
Exchanges:  1007
After
     287    2087    2404    2606    3058    4703    4781    5355
    6270    6988    7356    9029    9577    9611   11594   11757
   15313   15895   16677   17253   17711   17852   17972   18368
   18479   18652   21023   21578   21659   22452   23500   24283
   25471   25956   27337   28272   30366   35270   36935   37398
   37544   38333   39085   40176   40907   40974   41839   42367
   42854   43790   44473   45685   46053   46488   47732   49838
   51360   54434   54823   56459   59125   62841   63609   63671
```

In the above execution, the entire vector had to be passed over 53 times. During these passes, two elements were exchanged 1007 times.

## Functions to be implemented by you

### `Initialize()`

This function builds the vector, selecting random integers in the range of 0 to `max_value`.

### `Print()`

This function prints the vector and must do so obeying the rules that:

1. Only 8 numbers are printed per line.
2. Each number is printed in a cell that is 8 characters wide.

### `BubbleSort()`

This function implements the bubble sort algorithm producing a sorted vector in ascending order.

## iomanip

See Zybooks chapter 9.2 **Text-alignment manipulators** to learn about `setw`. Use `setw` to specify that each number is to be printed within a cell of 8 characters.

## Partner rules

This work is to be done **SOLO**. All students are to hand in their own work.
