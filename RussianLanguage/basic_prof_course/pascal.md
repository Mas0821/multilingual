# Pascal

## 数据类型

shortInt(16), integer(32), longInt(64)

real, doubleReal, Extended

singleChar, char

boolean

```pascal
flag := (5 > 3);
```

enumeratedType 枚举

setType 集合

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

record 记录类型

```pascal
RECORD
    Name : string;
    Age : integer;
    Gender : char;
END;
```