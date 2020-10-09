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
import { MatDialog, MatDialogConfig,  MAT_DIALOG_DATA } from '@angular/material/dialog';
import { CommonPopupDialogComponent } from 'src/app/utils/common-popup-dialog/common-popup-dialog.component';


 constructor(
              @Inject(MAT_DIALOG_DATA) public data: any ,
              public dialog: MatDialog ,
              )
  
  
  openSuccessDialog() :void{
     const dialogConfig = new MatDialogConfig();
      dialogConfig.disableClose = true;
      dialogConfig.autoFocus = true;
      dialogConfig.panelClass = 'custom-dialog-container';
      dialogConfig.data = {
      mobileNumber: this.profileForm.value.mobileNumber,
      Id: this.Id
};
  dialogConfig.width =  '40%';
  const dialogRef  = this.dialog.open(OtpMessageComponent , dialogConfig);

    dialogRef.afterClosed().subscribe(
        data => console.log("Dialog output:", data)
    );    
  }
```
## style.scss
```
.custom-dialog-container .mat-dialog-container {
    padding: 0px !important;
    border-radius: 5px;
    border-color: $base-color;
    border-style: groove;
}
```


[resource] (https://blog.angular-university.io/angular-material-dialog/)
