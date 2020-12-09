- 太空船操作符`<=>`
  - 例如：当`$a`小于，等于，大于`$b`时，分别返回-1，0，1

- 类型声明
  - 修改`strict_types`开启严格模式
  - `declare(strict_types=1)`，strict_types=1表示开启严格模式

- null合并操作符，`??`
  
- 常量数组
  - `defined('ANIMAL', ['dog','cat']);`

- `namespace`批量导入 
  - `use Space\{ClassA,ClassB,ClassC};`

- `throwable`接口
  - 7里面可以通过try...catch捕获异常
  - `set_exception_handler`捕获

- `Closure::call()`
    ```php
        class Test{
            private $num = 1;
        }

        $f = function () {
            return $this->num + 1;
        }

        echo $f->call(new Test);
    ```

- `intdiv`函数
  - 例如`10/3`,`intdiv(10,3)`，返回3
  
- `list`方括号写法
  - `$arr = [1,2,3];list($a,$b,$c) = $arr;` =》 `$arr = [1,2,3];[$a,$b,$c] = $arr;`

- 抽象语法树（AST）

