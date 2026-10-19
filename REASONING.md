# Reasoning Before Execution

Write the rule behind each case before you commit your predictions. Replace
every placeholder line below with one to three sentences that name the rule
producing that case's value, type, length, and dimensions. One rule is enough.
After you run and find a miss, add a short correction entry under that case in a
later commit.

## P01
It climbs a coercion ladder from logical -> integer -> double -> character, and whichever is the highest type among the values that the atomic vector contains will be the type. In this case, `c(TRUE, 2L, 3.5)`, `TRUE` is logical, `2L` is integer, and `3.5` is double. Hence, the type is double and coerces the values into double, resulting in `[1,2,3.5]`, since `TRUE` in double is `1`, `2L` in double is plainly `2`, and `3.5` is left as is, with length three and no dimensions.

## P02
The coercion ladder runs from logical -> integer -> double -> character. The highest type among these values is character, `"2"`, making the atomic vector convert the other two values into characters where `1L` becomes `"1"`, `"2"` is as is, and `TRUE` becomes `"TRUE"`. The value is `["1","2","TRUE"]` with length three and no dimensions.

## P03
The arithmetic requires recycling because one operand is shorter than the other so R repeats it, making `c(1L, 2L)` repeatedly added to `c(10L, 20L, 30L, 40L)`, resulting in `c(10L+1L,20L+2L,30L+1L,40L+2L)`. The type is integer since no coercion happened. The value is `[11,22,31,42]` with length of four, and no dimensions.

## P04
Indexing by position selects elements of `c(first = 8L, second = 5L, third = 9L)` with the selector `[c(3L, 1L)]`, which chooses the third and the first element, same in the order of the selector. No coercion happened since all of the types are integers. This results to the value of `[third=9,first=8]` with length two and no dimensions.

## P05
A negative index in the selector `c(4L, 7L, 9L)[-2L]` means the value includes every element except the one stored in the index of the selector, `[-2L]` drops the second element,`7L`. Selecting does not coerce, so the type is still integer. The value is `[4,9]` with length two and no dimensions.

## P06
`c(5L, NA_integer_, 12L, 3L)` is assigned to `x`, and `x` has a selector of a logical index `[is.na(x) | x > 10L]` which makes `TRUE | NA` `TRUE` because the operand already determines the result. The type is integer since no coercion happened. The value is `[NA,12]` with length two and no dimensions.

## P07
`factor` stores categorical data as integer vectors with attribute `levels` that defines the set of allowed values in `factor`, making the type an integer. It stores the value without the quotes. The value is `factor[low,high,low];levels=[low,high]` with length three, based of the number of elements in factor, and no dimensions.

## P08
List can store different type of elements and keeps them as it is instead of running the coercion ladder, resulting in a `list` type. The length counts the number of elements in the list, in this case are the `scores` and `label`. Hence, the value is `list{scores=[3,5],label=["A"]}` with length 2 and no dimensions.

## P09
data.frame is a list with class of data.frame, with vectors as its components and the length of each vector must be the same. The value is data.frame[2x2]{id=[1,2],passed=[TRUE,FALSE]} and its type is list with length 2 as length counts the vectors. Rows counts the items inside a vector, columns is per vector which is why it's 2x2.

## P10
The `c(10L, 20L)` is recycled in matrix with 2 rows and 3 columns, `matrix(1:6, nrow = 2L)`. It's 3 columns because columns are determined by the number of items(6) and the defined nrow(2). R fills the matrix down the columns, resulting in `1L+10L,2L+20L,3L+10L,4L+20L,5L+10L,6L+20L` with the type integer since both are integers. They get mapped by order, when the last value of the vector is reached but the matrix  still hasnt reached the end yet, the value to be added from the vector now goes back to the start. So the value is `matrix[2x3](11,22,13,24,15,26)` with length six and 2x3 dimensions.

## P11
Arithmetic with a missing value as one of the operand results in `NA` value. The value for `mean(c(8, NA_real_, 10))` is `[NA]` with the type double since the highest type is double, length of one, and no dimensions.

## P12
Arithmetic with a missing value as one of the operand results in `NA` value but `na.rm` drops the missing value to complete the operation in the remaining operands. `mean(c(8, NA_real_, 10), na.rm = TRUE)` drops the `NA` and calculates the mean of `8` and `10` which is `9`, with double as its type since no coercion happened. The value is `[9]` with length one and no dimensions.

## P13
Values from 1 to 3 is assigned to x, `[1,2,3]`, then the next line has a selector `[2]` and replaces the value at that index with `2.5`, resulting in `[1,2.5,3]` as the value and double as its type. It should be double because a vector should only hold 1 type of value from the value with the highest type precedence. This is a mixed-mode assignment. The length is three and there are no dimensions.

## P14
Value `[7,NA,12,4]` is assigned to `scores` with double as its type. `ifelse(is.na(scores), 0, scores * 2)` assigns the elements from scores to adjusted, and if the element is a missing value, it automatically replaces it as `0`, otherwise, multiplies the element by 2, then the selector `[adjusted > 15]` finds as value greater than 15, replacing it with `15`. The value is `[14,0,15,8]` with length four and no dimensions.

## P15
The array stores the values from 1 to 8 as integers and its dimension is set to be 2x2x2. The value is `array[2x2x2](1,2,3,4,5,6,7,8)` with length eight.

## P16
Indexing in R starts at 1, so the selector `[0L]` selects nothing returning an empty vector. The atomic vector contains integer type without coercion. The value is `[]` with length 0 and no dimensions.