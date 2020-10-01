# angularSnippet-


# angular material dialog 

In order to use angular meterial dialog , first need to import bellow modules to module.ts
CommonPopupDialogComponent will be a name of our custom dialog box component.

## module.ts

```
import {MatDialogModule, MatDialogRef, MAT_DIALOG_DATA} from '@angular/material/dialog';
import { CommonPopupDialogComponent } from 'src/app/utils/common-popup-dialog/common-popup-dialog.component';


@NgModule({
  declarations: [ CommonPopupDialogComponent],
  imports: [
    MatDialogModule
  ],
  
  providers: [
    PocService,
    { provide: MAT_DIALOG_DATA , useValue: {}},
    { provide: MatDialogRef , useValue: {}},

  ],
  entryComponents: [CommonPopupDialogComponent],
  exports: [ CommonPopupDialogComponent],
 
})
export class PocModule { }
```
Here is the implementation of CommonPopupDialogComponent
## CommonPopupDialogComponent.ts
```
import { Component, Inject, OnInit } from '@angular/core';
import { MatDialogRef, MAT_DIALOG_DATA } from '@angular/material/dialog';

@Component({
})
export class CommonPopupDialogComponent implements OnInit {
  val: any;

 
  constructor(
             public dialogRef: MatDialogRef<OtpModelComponent>,
              @Inject(MAT_DIALOG_DATA) public message: string ) {}

  closeDialog(){
    this.dialogRef.close(val);
  }
}
```

#### Here is the usage of our dialog box component 

## ParentComponent.ts
```
import { Component, Inject, OnInit } from '@angular/core';
import { MatDialogRef , MAT_DIALOG_DATA , MatDialog } from '@angular/material/dialog'
import { ActivatedRoute, Router } from '@angular/router';
import { CommonPopupDialogComponent } from 'src/app/utils/common-popup-dialog/common-popup-dialog.component';


 constructor(
              @Inject(MAT_DIALOG_DATA) public data: any ,
              private dialogRef: MatDialogRef<CommonPopupDialogComponent> ,
              public dialog: MatDialog ,
              private route: ActivatedRoute , 
              private router: Router)
  
  
  openSuccessDialog() :void{
    const dialogRef  = this.dialog.open(CommonPopupDialogComponent , {
      width: '40%',
      data: 'otp'
    });

    dialogRef.afterClosed().subscribe(
        data => console.log("Dialog output:", data)
    );    
  }
```

[resource] (https://blog.angular-university.io/angular-material-dialog/)
