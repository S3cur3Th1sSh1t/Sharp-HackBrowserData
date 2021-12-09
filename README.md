# Sharp-HackBrowserData
C# Wrapper of HackBrowserData from https://github.com/moonD4rk/HackBrowserData 

I did this mainly to experiment for myself with embedding golang binaries in C#.

The HackBrowserData main.go file was changed the following before compilation:

This technique has one main disadvantage. It writes the dll into appdata on runtime to load it. Therefore it's easy to spot for defenders. 

```
package main
import "C"
import "fmt"
import "strings"

import (
	"hack-browser-data/cmd"
)
	
//maindel :
//export maindel
func maindel(charargs *C.char) {
    var stringargs string
	stringargs = C.GoString(charargs)
	arrayargs := strings.Fields(stringargs)
    fmt.Println(arrayargs)
    cmd.Execute()
}

func main() {
}

``` 

Credit to [shantanu561993](https://github.com/shantanu561993) for writing the following blog post:
* https://medium.com/@shantanukhande/red-team-how-to-embed-golang-tools-in-c-e269bf33876a
