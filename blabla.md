```typescript
import { Component, OnInit } from '@angular/core';  
import { UntilDestroy, untilDestroyed } from '@ngneat/until-destroy';  
import { finalize } from 'rxjs';  
import { ApplicationInitializerService } from '../services/application/application-initializer.service';  
import { LoaderManagerService } from '../services/loader/loader-manager.service';  
import { InjectChangeDetectorService } from '../services/change-detector/inject-change-detector.service';  
  
@UntilDestroy()  
@Component({  
    selector: 'app-root',  
    templateUrl: './app.component.html',  
    styleUrls: ['./app.component.scss'],  
    providers: [  
        InjectChangeDetectorService  
    ]  
})  
export class AppComponent implements OnInit {  
  
    // Public properties  
  
    public shouldDisplayLoader = false;  
  
    // Calculated properties  
  
    public get isApplicationInitialized(): boolean {  
        return this._applicationInitializer.isApplicationInitialized;  
    }  
  
    // Lifecycle  
  
    constructor(  
        private _applicationInitializer: ApplicationInitializerService,  
        private _loaderManager: LoaderManagerService,  
    ) {}  
  
    ngOnInit() {  
        this.initializeApplication();  
        this.setupGeneralListeners();  
    }  
  
    private initializeApplication() {  
        this._loaderManager.startLoading();  
        this._applicationInitializer.initializeApplication()  
            .pipe(  
                finalize(() => {  
                    this._loaderManager.stopLoading();  
                })  
            )  
            .subscribe({  
                error: (err) => {  
                    console.log(err);  
                }  
            });  
    }  
  
    // Inner work  
  
    private setupGeneralListeners() {  
        this.setupLoadingActivatedListener();  
    }  
  
    private setupLoadingActivatedListener() {  
        this._loaderManager.isLoading$.pipe(  
            untilDestroyed(this)  
        ).subscribe(isLoading => {  
            this.shouldDisplayLoader = isLoading;  
        });  
    }  
}
```