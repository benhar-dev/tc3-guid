# Example GUID Creation in TwinCAT

## Disclaimer
This is a personal guide not a peer reviewed journal or a sponsored publication. We make
no representations as to accuracy, completeness, correctness, suitability, or validity of any
information and will not be liable for any errors, omissions, or delays in this information or any
losses injuries, or damages arising from its display or use. All information is provided on an as
is basis. It is the reader’s responsibility to verify their own facts.

The views and opinions expressed in this guide are those of the authors and do not
necessarily reflect the official policy or position of any other agency, organization, employer or
company. Assumptions made in the analysis are not reflective of the position of any entity
other than the author(s) and, since we are critically thinking human beings, these views are
always subject to change, revision, and rethinking at any time. Please do not hold us to them
in perpetuity.

## Overview 
Simple demo of the inbuilt GUID generation of TwinCAT.

### Code of interest
```
// Declaration ------------------------------------------------------

PROGRAM MAIN
VAR
	trigger : BOOL := TRUE;
	createGuid : FB_CreateGuid;
	guid : GUID;
	guidAsString : STRING;
END_VAR

// Program ----------------------------------------------------------

IF NOT createGuid.bBusy AND trigger THEN	
	
	trigger := FALSE;
	createGuid(bExecute := FALSE);	
	createGuid(
			bExecute := TRUE,
			pGuidBuffer := ADR(guid),
			nGuidBufferSize := SIZEOF(guid));
			
ELSIF createGuid.bBusy THEN
	
	createGuid();	
	
END_IF

// The code abover this point does not require any further libraries.  
// ------------------------------------------------------------------
// The code below requires Tc2_Utilites

guidAsString := GUID_TO_STRING(guid);

```

## Install 
Not required.  Simply open the project.

## TwinCAT
This project uses TcXaeShell 3.1.4024.11

## Getting started
This is not a guide for TcXaeShell, please visit http://beckhoff.com/ for further guides
* Open the included TwinCAT project and activate on your local machine
* Login and set the PLC running
* The first cycle will activate the creation of a GUID.  For further generation set the trigger to TRUE.

