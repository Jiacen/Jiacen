---
title: Delphi Script Programming under integra phase 6
date: 2019-02-24 18:27:02
tags: [integra6,iDPro,Delphi script]
---
### 1. Data Elements Creation and Load to SIS Database

- 1.1. Create new global DB *(NO Optimized access)* with different data type elements as a user data block according to the associated function group, and load it into CPU;
	![](/images/integra001_01.jpg)    
- 2.2. If u want to use the symbolic addressing to program scripts under integraDesignerPro, all the symbol operands have to be generated in SIS database. For user data block, only operands that have been defined in a template are entered can be rebuild to SIS database. So, create a function group template to use all the elements defined in the user DB;
      
	  //Create newtab name==FLEXTAB01;title==Flex(line1)/TAB1(line2)  
	  !TAB_01;FLEXTAB01;NNNNN;Flex;;  
	  !TAB_02;FLEXTAB01;NNNNN;TAB1;;
      
	  //AddT displayed and operated under FlexTAB1
      @AddOn@AddT.bypassBZ3;FLEXTAB01;0001N;;;
	  @AddOn@AddT.bypassBZ4;FLEXTAB01;0001N;;;
      
	  //Binary values from userdata, displayed under FlexTAB1
	  "FGDB_010VE_001@userdata".Test1_Bool;FLEXTAB01;0001N;;;
	  "FGDB_010VE_001@userdata".Test2_Bool;FLEXTAB01;0001N;;;

	  //Integer value form userdata, add to Process Valuse tab w/o min&max
	  TYPE;PW;Prozesswert;;; 
      "FGDB_010VE_001@userdata".Test3_INT;Soll;0001N;Motor Speed (rpm);#;
	  "FGDB_010VE_001@userdata".Test3_INT;IST;NNNNN;;#;
	  END_TYPE 

	  //Word value from userdata, displayed under FlexTAB1
	  TYPE;FLEXTAB01;Prozesswert;;; 
	  "FGDB_010VE_001@userdata".Test4_WORD;IST;0001N;;%X;
	  END_TYPE 

	  //String values from userdata, displayed under FlexTAB1,not be operated
	  TYPE;FLEXTAB01;String;;;
	  "FGDB_010VE_001@userdata".Test5_STRING;FLEXTAB01;NNNNN;;;
	  END_TYPE
***
### 2. Change the properties of graphic object via script programming under *BitButton* **OnClick** event

- 2.1. Background Color Changing *(Task 11.1.1)* ;
 
 	  // BitBtn1.OnClick
      procedure BitBtn1Click(Sender: TObject);
	  begin
	  if Rectangle1.Brush.StartColor = clWhite then      
  	  Rectangle1.Brush.StartColor := clGreen
  	  else
  	  Rectangle1.Brush.StartColor := clWhite; 
      end;   //click to invert the backgroud color of rectangle
      
- 2.2. Object Position Changing *(Task 11.1.2)* ;
 
      // BitBtn1.OnClick
      procedure BitBtn1Click(Sender: TObject);
      begin
	  if  Rectangle1.Top <=400 then                   
 	  Rectangle1.Top :=  Rectangle1.Top +50
 	  else
 	  Rectangle1.Top :=100; 
      end;	 //click to move the rectangle top to bottom
***     
### 3. Create Global Actions to change the object properties via script programming under *SISEvents* **OnFlashingCycle** event *(Task 11.2)*

		  // SISEvents1.OnFlashingCycle
		  procedure SISEvents1FlashingCycle(Sender: TObject; TriggerOn: Boolean);
		  Begin	
      		//"mouthe" open & close
		  	if Pie1.Sweepangle = 315 then             
		  	Pie1.Sweepangle:=355
		  	else
		  	Pie1.Sweepangle:=315;    
      		//movement form left to right
		  	if Pie1.Left <= 1000 then               
		  	Pie1.Left := Pie1.Left + 100
		  	else
		  	Pie1.Left := 100;
		  End;
	  
***
### 4. Application of *TagItemList* with ISI DataAccess *PLCLED* & *PLCLabel* that have **TagItem** properties *(Task 11.3)*
- 4.1. Create a TagItemList and add tag items to it;
	![](/images/integra001_02.jpg)
- 4.2. TagItemList activation via script programming with the **OnCreate** event of the Form;    

	  // FormS001.OnCreate
	  procedure isi_FormCreate(Sender: TObject);
	  begin
      ActivateTagItemList(TagItemList1, DEFAULTCONNECTION, DEFAULTPLANT, DEFAULTFGNAME,false);    
      end;
***
### 5. The using of Simple DataAccess *LED* & *Label* connect to *TagItemList* w/o **TagItem** properties     *(Task 11.4)*
- Select the TagItem from TL, and add scripts under it **OnValueChange** event;

	  // TagItem_flashfreq.OnValueChange
	  procedure TagItem_flashfreqValueChange(Sender: TObject; AValue: Variant; AValueValid: Boolean);
	  begin
      if not AValueValid then exit;  //Error routine
      LED1.LedState := AValue;
	  end;
      // TagItem_Sec.OnValueChange
	  procedure TagItem_SecValueChange(Sender: TObject; AValue: Variant; AValueValid: Boolean);
	  begin
      if not AValueValid then exit;  //Error routine
      Label1.Caption := IntToStr(AValue) + 'sec';
	  end;
***
### 6. Value Input from VISU system to PLC via ISI DataAccess *PLCLabel* *(Task 11.5)*
- 6.1. Add a new TagItem in the TL;
	![](/images/integra001_03.jpg)
- 6.2. Add a *PLCLabel* and connect the TagItem as before, then create scripts under **OnClick** event of this *PLCLabel* ;
  
  	  // PLCLabel1.OnClick
	  procedure PLCLabel1Click(Sender: TObject);
   	  var
 	  	AIntVal   : integer;                //variable declaration
 
	  Begin                              
      		//reload operand into local variable
      		AIntVal := TagItem_Write_Test.value;  
            
    		//Call input box
      		if SIS.InputInt(AIntVal, TagItem_Write_Test.TagComment,false) then
      		Begin
      		TagItem_Write_Test.Write(AIntVal);
      		Showmessage (INTtoSTR(AIntVal) + tr' was written in the PLC');
      		End;          
      End     
***
### 7. The script programming for user access level
- 7.1. Value can only be wirtten to PLC with sufficient user level from VISU 
*(Task 11.6)* ;

	  // PLCLabel1.OnClick
      procedure PLCLabel1Click(Sender: TObject);
      var
 	  AIntVal   : integer;                //variable declaration
      
	  Begin
   	  // Level check
	  if TagItem_Write_Test.IsTagAccessLevelValid then
      //scripts for value input
      Begin
      ....
      ...
      ...
      End
      //pop-up messagebox
 	  Else
	  Showmessage('No Authority to write');
      End;
- 7.2. Make *user access level* to change the properties of object via script programming under *SISEvents* **OnUserChanged** event *（Task 11.7）* ;

		// SISEvents1.OnUserChanged
		procedure SISEvents1UserChanged(Sender: TObject);
		Begin
        
		if TagItem_Write_Test.IsTagAccessLevelValid then
        
 		begin 
        	PLCLabel1.Color:=clWhite;
        	PLCLabel1.Font.Color:=clBlue;
 		end    
        
   		else
        
   		begin 
        	PLCLabel1.Color:=clBtnFace;
        	PLCLabel1.Font.Color:=clBlack;
   		end 
        End;