---
category: LLM workspace
---

```TypeScript {'title':'hallo2.ts'}
import { Component } from '@angular/core';  
import { LanguageManagerService } from '../../services/language/language-manager.service';  
import { ApplicationReloaderService } from '../../services/application/application-reloader.service';  
import { Language } from '../../models/base/language.enum';  
  
@Component({  
    selector: 'app-home-container',  
    templateUrl: './home-container.component.html',  
    styleUrls: ['./home-container.component.scss']  
})  
export class HomeComponent {  
  
    // Public properties  
  
    public languages = Language.getAllForUI();  
  
    // Calculated properties  
  
    public get activeLanguage(): Language {  
        return this._languageManager.language;  
    }  
  
    // Enum properties  
  
    public languageEnum = Language;  
  
    // Lifecycle  
  
    constructor(  
        private _applicationReloaderManager: ApplicationReloaderService,  
        private _languageManager: LanguageManagerService  
    ) {}  
  
    // Interface  
  
    public setActiveLanguage(language: Language) {  
        this._languageManager.saveLanguage(language);  
        this._applicationReloaderManager.reloadApp();  
    }  
}
```

```dataview {'title':"Top-10"}
table lang
from "halloworld"
sort lang asc
limit 10
```

```Python {'title':'hallo.py'}
print("Hello World")
```

```Java {'title':'hallo.java'}
import java.io.*;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World");
    }
}
```

```Go {'title':'hallo.go'}
println('Hello World");
```
```Cpp {'title':'hallo.cpp'}
#include <iostream>
 
int main() {
    std::cout << "Hello World";
    return 0;
}
```
```JavaScript {'title':'hallo.js'}
console.log("Hello World");
```
```TypeScript {'title':'hallo.ts'}
console.log 'Hello World'
```
```C {'title':'hallo.c'}
#include <stdio.h>
int main() {
    printf("Hello World");
    return 0;
}
```
```Rust {'title':'hallo.rs'}
fn main() {
    println!("Hello, world!");
}
```
```Swift {'title':'hallo.swift'}
println('Hello World');
```
```HTML {'title':'hallo.html'}
<!DOCTYPE html>
<html>
    <head>
    </head>
    <body>
        <h1>Hello World<h1>
    </body>
</html>
```