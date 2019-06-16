---
title: My Second Post :)
date: 2019-06-13T01:01:43.000+00:00

---
Hello Second!!

{{< highlight go "linenos=table">}}
package main

import (
    "fmt"
    "math/rand"
    "time"
)

type Moo struct {
    Cow   int
    Sound string
    Tube  chan bool
}

// A cow will moo until it is being milked
func cow(num int, mootube chan Moo) {
    tube := make(chan bool)
    for {
        select {
        case mootube <- Moo{num, "moo", tube}:
            fmt.Println("Cow number", num, "mooed through the mootube")
            <-tube
            fmt.Println("Cow number", num, "is being milked and stops mooing")
            mootube <- Moo{num, "mooh", nil}
            fmt.Println("Cow number", num, "moos one last time in relief")
            return
        default:
            fmt.Println("Cow number", num, "mooed through the mootube and was ignored")
            time.Sleep(time.Duration(rand.Int31n(1000)) * time.Millisecond)
        }
    }
}

// The farmer wants to turn on all the milktubes to stop the mooing
func farmer(numcows int, mootube chan Moo, farmertube chan string) {
    fmt.Println("Farmer starts listening to the mootube")
    for unrelievedCows := numcows; unrelievedCows > 0; {
        moo := <-mootube
        if moo.Sound == "mooh" {
            fmt.Println("Farmer heard a moo of relief from cow number", moo.Cow)
            unrelievedCows--
        } else {
            fmt.Println("Farmer heard a", moo.Sound, "from cow number", moo.Cow)
            time.Sleep(2e9)
            fmt.Println("Farmer starts the milking machine on cow number", moo.Cow)
            moo.Tube <- true
        }
    }
    fmt.Println("Farmer doesn't hear a single moo anymore. All done!")
    farmertube <- "yey!"
}

// The farm starts out with mooing cows that wants to be milked
func runFarm(numcows int) {
    farmertube := make(chan string)
    mootube := make(chan Moo)
    for cownum := 0; cownum < numcows; cownum++ {
        go cow(cownum, mootube)
    }
    go farmer(numcows, mootube, farmertube)
    farmerSaid := <-farmertube
    if farmerSaid == "yey!" {
        fmt.Println("All cows are happy.")
    }
}

func main() {
    runFarm(4)
    fmt.Println("done")
}
{{< / highlight >}}

{{< highlight dart "linenos=table">}}
print('Hello world!');
abstract class Person {
    String _name;
  
    void greet();
  
    void walk();
  
    void eat() {
      print('人得吃饭');
    }
  }

  class Teacher implements Person {
    @override
    void greet() {
        print('gren');
    }
  
    @override
    void walk() {}
  
    @override
    void eat() {}
  
    @override
    get _name => '';
  
    @override
    set _name(String __name) {
      _name = __name;
    }
  }
void main(){
    Teacher ter = Teacher();
    
    
}
{{< / highlight >}}


{{< highlight go-html-template >}}
<section id="main">
<div>
<h1 id="title">{{ .Title }}</h1>
{{ range .Pages }}
{{ .Render "summary"}}
{{ end }}
</div>
</section>
{{< /highlight >}}


