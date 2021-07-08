![HackerRank](https://hrcdn.net/community-frontend/assets/brand/hr-logo-new-black-green-2f615594d2.svg)

#### Objective
Today, we are building on our knowledge of arrays by adding another dimension. Check out the Tutorial tab for learning materials and an instructional video.

#### Context
Given a ***6 x 6*** 2D Array, ***A*** :

```
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
```

We define an hourglass in ***A*** to be a subset of values with indices falling in this pattern in ***A***'s graphical representation:

```
a b c
  d
e f g
```

There are **16** hourglasses in ***A***, and an hourglass sum is the sum of an hourglass' values.

#### Task
Calculate the hourglass sum for every hourglass in ***A***, then print the maximum hourglass sum.

#### Example

In the array shown above, the maximum hourglass sum is **7** for the hourglass in the top left corner.

#### Input Format

There are **6** lines of input, where each line contains **6** space-separated integers that describe the 2D Array ***A***.

#### Constraints

+ ***-9 <= A[i][j] <= 9*** 
+ ***0 <= i,j <= 5***
#### Output Format

Print the maximum hourglass sum in .

#### Sample Input

```
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 2 4 4 0
0 0 0 2 0 0
0 0 1 2 4 0
```

#### Sample Output

```
19
```

#### Explanation

 contains the following hourglasses:

```
1 1 1   1 1 0   1 0 0   0 0 0
  1       0       0       0
1 1 1   1 1 0   1 0 0   0 0 0

0 1 0   1 0 0   0 0 0   0 0 0
  1       1       0       0
0 0 2   0 2 4   2 4 4   4 4 0

1 1 1   1 1 0   1 0 0   0 0 0
  0       2       4       4
0 0 0   0 0 2   0 2 0   2 0 0

0 0 2   0 2 4   2 4 4   4 4 0
  0       0       2       0
0 0 1   0 1 2   1 2 4   2 4 0
```

The hourglass with the maximum sum () is:
```
2 4 4
  2
1 2 4
```

#### Solution:

```golang

package main

import (
    "bufio"
    "fmt"
    "io"
    "os"
    "strconv"
    "strings"
)

func main() {
    reader := bufio.NewReaderSize(os.Stdin, 1024*1024)

    var array [][]int32
    for i := 0; i < 6; i++ {
        arrRowTemp := strings.Split(readLine(reader), " ")

        var arrRow []int32
        for _, arrRowItem := range arrRowTemp {
            arrItemTemp, err := strconv.ParseInt(arrRowItem, 10, 64)
            checkError(err)
            arrItem := int32(arrItemTemp)
            arrRow = append(arrRow, arrItem)
        }

        if len(arrRow) != int(6) {
            panic("Bad input")
        }

        array = append(array, arrRow)
    }
    
    var zz []int

    for i := 0; i < int(len(array)-2); i++ {
        v := array[i]
        for j := 0; j < int(len(v)-2); j++ {

            z := array[i][j] + array[i][j+1] + array[i][j+2] + array[i+1][j+1] + array[i+2][j] + array[i+2][j+1] + array[i+2][j+2]
            zz = append(zz, int(z))
        }
    }
    
    const mininput int = -9

    var max int
    max = mininput * 7
    for k := 0; k < len(zz); k++ {
        if zz[k] > max {
            max = zz[k]
        }
    }
    fmt.Println(max)
}

func readLine(reader *bufio.Reader) string {
    str, _, err := reader.ReadLine()
    if err == io.EOF {
        return ""
    }

    return strings.TrimRight(string(str), "\r\n")
}

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

```
