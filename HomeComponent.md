```typescript
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