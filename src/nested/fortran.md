# Fortran base

# 变量

5 种内置数据类型

- integer —— 表示整数的数据，正数或负数

- real —— 用于浮点数据（不是整数）

- complex —— 由实部和虚部组成的对

- character —— 用于文本数据

- logical —— 用于表示布尔值（真或假）值的数据

# 声明变量

Fortran 代码不区分大小写

```fortran
program variables
  implicit none

  integer :: amount
  real :: pi
  complex :: frequency
  character :: initial
  logical :: isOkay

end program variables
```

一旦我们声明了一个变量，我们就可以使用赋值运算符 `=` 对其进行赋值和重新赋值。

```fortran
amount = 10
pi = 3.1415927
frequency = (1.0, -0.5)
initial = 'A'
isOkay = .false.
```

字符由单引号 (') 或双引号 (") 包围。

逻辑或布尔值可以是 `.true.` 或 `.false.`。

注意 “content=” 声明时的赋值：`integer :: amount = 1`。 这不是正常的初始化； 它暗示了 `save` 属性，这意味着变量在过程调用之间保留其值。好的做法是将变量分别初始化为它们的声明。

> 当使用"::"运算符来声明一个变量时，Fortran 编译器会在编译时为这个变量分配内存，并将其初始化为 0。如果在声明变量时为它赋予一个初始值，如所示的 1，那么在分配内存后，变量将被初始化为这个值。
>
> 在这种情况下，声明"fortran integer :: amount = 1"意味着你正在定义一个整数类型的变量"amount"，并将其初始化为 1。这个变量可以在后续的代码中使用，其值可以改变。如果你在声明时不给变量赋值，那么它的值将被初始化为 0。

## 一些例子

1. `real*8 AL(3,3),Etotp`: 这是两个变量的声明，一个是`AL`，另一个是`Etotp`。 `real*8`指定了变量的数据类型为 8 字节的浮点数，也称为双精度实数。`AL`是一个二维数组，其维度为 3x3，意味着它包含 9 个浮点数。`Etotp`是一个单独的浮点数变量，类型为`real*8`。

示例代码：

```fortran
AL(1,1) = 1.0d0
AL(1,2) = 2.0d0
AL(1,3) = 3.0d0
AL(2,1) = 4.0d0
AL(2,2) = 5.0d0
AL(2,3) = 6.0d0
AL(3,1) = 7.0d0
AL(3,2) = 8.0d0
AL(3,3) = 9.0d0

Etotp = 10.0d0
```

2. `real*8,allocatable,dimension (:,:) :: xatom,fatom`:这是两个可分配的（allocatable）二维数组变量`xatom`和`fatom`的声明。 `real*8`指定了这些变量的数据类型为 8 字节的浮点数，也称为双精度实数。`dimension(:,:)`说明它们是二维数组，且维度在运行时指定。`allocatable`指定这些数组是可分配的，这意味着它们的大小可以在程序运行时动态分配，并且可以根据需要重新分配大小。

示例代码：

```fortran
allocate(xatom(3,3))
allocate(fatom(3,3))

xatom(1,:) = [1.0d0, 2.0d0, 3.0d0]
xatom(2,:) = [4.0d0, 5.0d0, 6.0d0]
xatom(3,:) = [7.0d0, 8.0d0, 9.0d0]

fatom = xatom**2
```

这将分配 3x3 大小的 xatom 和 fatom 数组，并将 xatom 数组的第一行分配为 1,2,3。然后，使用逐元素平方运算符将 xatom 数组的平方分配给 fatom 数组，从而将 fatom 数组设置为[1.0d0, 4.0d0, 9.0d0]的第一行，[16.0d0, 25.0d0, 36.0d0]的第二行和[49.0d0, 64.0d0, 81.0d0]的第三行。

3. `character(len=50) char_tmp(20)`:这是一个有 20 个元素的字符数组，每个元素都是 50 个字符长。

示例代码：

```fortran
character(len=50) char_tmp(20)
char_tmp(1) = 'Hello, '
char_tmp(2) = 'how are you?'
print *, char_tmp(1) // char_tmp(2)
```

这将输出“Hello, how are you?”，其中 // 是 Fortran 中的字符串连接运算符。

4. `CHARACTER(LEN=200), OPTIONAL :: title_line`:这是一个可选的字符变量声明，它的长度为 200。使用 `OPTIONAL` 关键字声明的变量意味着变量是可选的，即在调用程序中可以选择性地传递它的值。

示例代码：

```fortran
SUBROUTINE read_data_file(filename)
    CHARACTER(LEN=200), OPTIONAL :: title_line
    CHARACTER(LEN=200) :: filename

    OPEN(10, FILE=filename)

    IF (PRESENT(title_line)) THEN
        READ(10, '(A)') title_line
    END IF

    ! read the data from the file

    CLOSE(10)
END SUBROUTINE
```

这个子程序打开一个名为 filename 的文件，并读取它的标题行（如果存在）。如果 title_line 变量在调用程序中被传递，则使用 PRESENT()函数检查它是否存在。如果存在，读取文件中的第一行数据到 title_line 变量中。

5. `CHARACTER(LEN=*) :: title `:这是一个长度不固定的字符变量声明，它的长度可以根据存储的字符串内容进行自动调整。

示例代码：

```fortran
CHARACTER(LEN=*) :: title

title = 'My simulation results'

WRITE(*, '(A)') title
```

这将创建一个长度为 15 的字符变量 title，并将“ My simulation results ”字符串存储在其中。最后，它使用 WRITE 语句将 title 变量的值输出到控制台。因为 CHARACTER(LEN=\*) 声明的变量长度是可变的，所以可以存储不同长度的字符串。

# 表达式

常用的算术运算符集可用，按优先顺序列出：

| 操作符 | 描述 |
| ------ | ---- |
| \*\*   | 指数 |
| \*     | 乘法 |
| /      | 除法 |
| +      | 加法 |
| -      | 减法 |

# 组织代码结构

Fortran 有两种形式的过程：

- **子例程**：由 `call` 语句调用

- **函数**：在返回值的表达式或赋值中调用

子程序和函数都可以通过 argument association 访问父范围内的变量；除非指定了 `value` 属性，否则这类似于按引用调用。

## 子程序

子程序输入参数，称为 dummy arguments，在子程序名称后面的括号中指定；虚拟参数类型和属性在子例程的主体中声明，就像局部变量一样。

使用示例：

```fortran
! Print matrix A to screen
subroutine print_matrix(n,m,A)
  implicit none
  integer, intent(in) :: n
  integer, intent(in) :: m
  real, intent(in) :: A(n, m)

  integer :: i

  do i = 1, n
    print *, A(i, 1:m)
  end do

end subroutine print_matrix
```

注意声明虚拟参数时附加的 `intent` 属性；这个可选属性向编译器表示参数是“只读”（`intent(in)`）“只写”（`intent(out)`）还是“读写”（`intent(inout)`) 在过程中。在这个例子中，子程序不会修改它的参数，因此所有的参数都是 `intent(in)`。

始终为虚拟参数指定 `intent` 属性是一种很好的做法；这允许编译器检查意外错误并提供自文档。

我们可以使用 `call` 语句从程序中调用此子例程：

```fortran
program call_sub
  implicit none

  real :: mat(10, 20)

  mat(:,:) = 0.0

  call print_matrix(10, 20, mat)

end program call_sub
```

## 函数

## 模块

## Interface

`INTERFACE` 是用于定义子程序和函数接口的语句块。它用于在主程序中声明子程序或函数的名称、参数、返回值类型和其他属性。这可以让编译器在编译时检查调用程序与被调用程序之间的数据类型、参数数目和参数顺序是否匹配，从而减少错误和调试时间。

在调用子程序时，使用 `CALL` 语句可以让程序执行特定的子程序。但在调用子程序时，必须确保传递的参数与子程序声明中的参数匹配，否则可能会出现编译错误或运行时错误。使用 `INTERFACE` 可以在编译时检查这些参数匹配错误，提高代码的可靠性和稳定性。

```fortran
INTERFACE
    SUBROUTINE scan_title (io_file, title, title_line, if_find)
        CHARACTER(LEN=200), OPTIONAL :: title_line
        LOGICAL, OPTIONAL :: if_find
        INTEGER :: io_file
        CHARACTER(LEN=*) :: title
    END SUBROUTINE scan_title
END INTERFACE
```

# 文件输入/输出

在 Fortran 中，文件由单元标识符管理。与文件系统的交互主要通过 `open` 和 `inquire` 内置程序进行。通常，工作流程是打开一个文件到一个单元标识符，读取和/或写入它，然后再次关闭它。

```fortran
integer :: io
open(newunit=io, file="log.txt")
! ...
close(io)
```

默认情况下，如果文件不存在，则将创建该文件并打开以供读取和写入。写入现有文件将从第一条记录（行）开始，因此默认情况下会覆盖该文件。

要创建对文件的只读访问权限，必须使用指定的 `status` 和 `action`

```fortran
integer :: io
open(newunit=io, file="log.txt", status="old", action="read")
read(io, *) a, b
close(io)
```

如果文件不存在，则会发生运行时错误。要在打开文件之前检查文件是否存在，可以使用 `inquire` 函数

```fortran
logical :: exists
inquire(file="log.txt", exist=exists)
if (exists) then
  ! ...
end if
```

或者，`open` 过程可以返回可选的 iostat 和 iomsg：

```fortran
integer :: io, stat
character(len=512) :: msg
open(newunit=io, file="log.txt", status="old", action="read", &
  iostat=stat, iomsg=msg)
if (stat /= 0) then
  print *, trim(msg)
end if
```

请注意，iomsg 需要一个具有足够存储大小的固定长度字符变量来保存错误消息。

同样，通过使用 status 和 action 关键字写入文件。

要创建一个新文件，请使用

```fortran
integer :: io
open(newunit=io, file="log.txt", status="new", action="write")
write(io, *) a, b
close(io)
```

或者，`status="replace"` 可用于覆盖现有文件。强烈建议在决定要使用的*status* 之前先检查文件是否存在。要附加到输出文件，可以使用显式指定 position 关键字

```fortran
integer :: io
open(newunit=io, file="log.txt", position="append", &
  & status="old", action="write")
write(io, *) size(v)
write(io, *) v(:)
close(io)
```

要重置文件中的位置，可以使用内置程序`rewind`和`backspace`。 `rewind` 将文件指针重置为文件的开头，以便读取文件的第一行，而 `backspace` 将文件指针向后移动一个记录，也就是向后移动一个记录的长度。

最后，要删除文件，必须打开文件，并且可以在关闭后删除

```fortran
logical :: exists
integer :: io, stat
inquire(file="log.txt", exist=exists)
if (exists) then
  open(file="log.txt", newunit=io, iostat=stat)
  if (stat == 0) close(io, status="delete", iostat=stat)
end if
```

一个有用的 IO 功能是暂存文件，可以使用 `status="scratch" `打开。它们在关闭单元标识符后自动删除。

# 其他使用

1. 编译：`ifort -o file_exe file1.f90 file2.f90 ...`

2. `read(10,*) Rc_M,m_neigh`:_ 符号用于指示一个读取/写入列表项应使用的格式。在这个例子中，_ 符号表示使用默认格式，读取从文件 10 中得到的下一个数据值，并将其分配给变量 Rc_M 和 m_neigh。

    默认格式是指定读取或写入操作中不需要显式格式指令的方式，这在某些情况下可以方便地读取或写入简单的数据类型。但是，在某些情况下，可能需要使用显式格式控制，以确保数据被正确读取或写入。如果省略了 \* 符号，则编译器将假定您提供了一个格式字符串，这可能会导致读取或写入错误。

3. `read(13,'(a200)') trainSetDir`:这行代码是一个读取输入的语句。具体来说，它使用 `read` 命令从文件号为 13 的文件中读取一个长度为 200 个字符的字符串，并将其存储在 `trainSetDir` 变量中。

    `'(a200)'` 是一个格式说明符，用于告诉 `read` 命令应该如何解释从文件中读取的内容。在这个例子中，`(a200)` 表示读取一个长度为 200 的字符串（`a` 是字符串类型的格式符）。这意味着 `read` 命令将从文件中读取一个长度为 200 的字符串，并将其存储在 `trainSetDir` 变量中。

    注意，如果输入字符串的长度超过了 200 个字符，则会被截断。如果输入字符串的长度小于 200 个字符，则其余的字符将被填充为零。

4. `MOVEMENTDir=trim(trainSetFileDir(sys))` 函数用于删除字符串两端的空格。

5. `write(1314, "(3(E17.10, 1x), i4)") dR_neigh(1, i, j, k), dR_neigh(2, i, j, k), dR_neigh(3, i, j, k), list_neigh(i,j,k)`:"(3(E17.10, 1x), i4)" 是一个格式字符串，用来指定输出的数据格式，包括了以下几个部分：
    `3`：指示这个格式字符串将会输出三个值；
    `E17.10`：指示每个浮点数的宽度为 17，其中包括小数点和 10 位小数，即总共 17 个字符；
    `1x`：指示每个浮点数和整数之间都有一个空格分隔符，以便于阅读；
    `i4`：指示输出一个整数，宽度为 4，即总共 4 个字符。
