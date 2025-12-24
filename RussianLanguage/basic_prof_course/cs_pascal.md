# Pascal

pascal 对于 变量名 和 关键字 均大小写不敏感。
```pascal
program nameProgram
var
	{define var type}
begin
	{function}
end.
```

```pascal
:= { pascal 赋值}
=  { pascal 判定相等}
   {pascal 无自增、自减符号}
```
## 数据类型

`shortInt`(16), `integer`(32), `longInt`(64)

`real`, `doubleReal`, `Extended`

`singleChar`, `char`

`boolean`

```pascal
flag := (5 > 3);
```

`enumeratedType` 枚举

`setType` 集合

```pascal
var
    number : setType;
    i : integer;
begin
    numbers := {1, 2, 3, 4, 5, 6};
    for i in numbers do
    begin
        // ...
    end;
end;
```

`record` 记录类型

```pascal
RECORD
    Name : string;
    Age : integer;
    Gender : char;
END;
```

## 循环

### `FOR ... DO`

```PASCAL
for {condition = true} do
begin
	{function, line end as ';'}
end;
```
### `WHILE ... DO`

```PASCAL
while {condition = true} do
begin
	{function, line end as ';'}
end;
```

## 文件读写

核心函数说明：
- **`AssignFile`**: 将文件变量与外部磁盘文件关联。
>  **`AssignFile(f, filename)`**: Связывает файловую переменную `f` с именем файла на диске (**filename**). Это первый шаг перед выполнением любой операции.

- **`Rewrite`**: 创建并打开一个新文件以供写入。
> **`Rewrite(f)`**: Создает новый файл и открывает его для записи. Если файл с таким именем уже существует, он будет полностью **перезаписан** (старое содержимое удалится).

- **`Reset`**: 打开一个现有文件以供读取。
>**`Reset(f)`**: Открывает существующий файл только для **чтения**. Если файл не найден, программа выдаст ошибку.

- **`Writeln(tf, ...)`**: 向文件写入一行并换行。
> **`Writeln(f, string)`**: Записывает строку текста в файл и переводит курсор на новую строку.

- **`Readln(tf, s)`**: 从文件读取一行并存入字符串变量。
> **`Readln(f, s)`**: Считывает одну строку из файла в переменную `s` и переходит к следующей строке.

- **`CloseFile`**: 操作完成后必须关闭文件以释放系统资源。
> **`CloseFile(f)`**: Закрывает файл и сохраняет все изменения. Это **обязательный** шаг для освобождения ресурсов системы.

> **`Append(f)`**: Открывает существующий текстовый файл для **добавления** данных в конец (не удаляя текущее содержимое).

> **`Eof(f)`**: (End Of File) Логическая функция, которая возвращает `True`, если достигнут **конец файла**. Обычно используется в циклах `while`.

```pascal
program WriteToFile {此代码将创建或覆写一个文件并写入两行文本}
var
	tfOut : TextFile;
begin
	{指定文件路径}
	AssignFile(tfOut, 'example.txt');
	
	try
		{创建新文件，如果文件已存在则覆盖}
		Rewrite(tfOut);
		{写入数据}
		WriteLn(tfOut, 'this is the 1st line.');
		WriteLn(tfOut, 'this is the 2nd line.');
		{关闭文件}
		CloseFile(tfOut);
	except
		on E: Extension do
			WriteLn('write file error: ', E.message);
	end;
end.
```

```pascal
program ReadFromFile;
var
	tfIn: TextFile;
	s: string;
begin
	{指定文件路径}
	AssignFile(tfIn, 'example.txt');
  
	try
		{以只读模式打开文件}
	    Reset(tfIn);
	    {循环读取直到文件末尾}
	    while not Eof(tfIn) do
		    begin
				Readln(tfIn, s);
			    Writeln(s);
		    end;
	    {关闭文件}
	    CloseFile(tfIn);
	except
	    on E: Exception do
	      Writeln('read file error: ', E.Message);
	end;
	
	{保持窗口开启S}
	Readln;
end.
```
> 在 Delphi 环境下，可以使用 `LoadFromFile` 和 `SaveToFile` 实现更简便的读写（[TStringList 官方文档](http://www.delphibasics.ru/)）。