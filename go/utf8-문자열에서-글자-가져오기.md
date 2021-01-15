# UTF8 문자열에서 글자 가져오기

`utf8.DecodeRuneInString` 함수를 사용하는 방법과 `range` 키워드를 사용하는 방법이 있다.

```go
package main

import (
    "fmt"
    "unicode/utf8"
)

func main() {
    var s string = "안녕하세요"

    for i, w := 0, 0; i < len(s); i += w {
        runeValue, width := utf8.DecodeRuneInString(s[i:])
        fmt.Printf("%#U\n", runeValue)
        w = width
    }

    for _, runeValue := range s {
        fmt.Printf("%#U\n", runeValue)
    }
}
```
