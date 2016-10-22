###DOL.MD

----------

1.改完之后的.dot图：
- example1：
![example1](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/assignment/dot1.png?raw=true)

- example2：
![example2](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/assignment/dot2.png?raw=true)

2.改完之后的输出图：
- example1：
![example1](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/assignment/example1.JPG?raw=true)
- example2:
![example2](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/assignment/example2.JPG?raw=true)

3.如何修改的：
- example1: 使其输出3次方
将原来的square.c文件里的i = i * i改成 i = i * i * i;
```
if (p->local->index < p->local->len) {
        DOL_read((void*)PORT_IN, &i, sizeof(float), p);
        i = i*i*i;
        DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
        p->local->index++;
    }
```

- example2:
将example2.xml里面的迭代次数由3次改成2次：
``` <variable value="2" name="N"/>  ```