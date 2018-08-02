
---?image=assets/cognizant-log-small.png&position=left 25px top 25px&size=17%


# Establishing Patient Identification

---

## Key Points

@ul

* Correct patient identification is vital for patient safety and the maintenance of patient confidentiality.
* States have been implementing two methods of establishing patient identification.

@ulend

---


## Protected Health Information
@fa[info] The **HIPAA Privacy Rule** protects most individually identifiable health information held or transmitted by a covered entity or its business associate, in any form or medium, whether electronic, on paper, or oral. The Privacy Rule calls this information protected health information (PHI)2. Protected health information is information, including demographic information, which relates to:  

---

@ul

* the individual’s past, present, or future physical or mental health or condition,
* the provision of health care to the individual, or
* the past, present, or future payment for the provision of health care to the individual, and that identifies the individual or for which there is a reasonable basis to believe can be used to identify the individual. Protected health information includes many common identifiers (e.g., name, address, birth date, Social Security Number) when they can be associated with the health information listed above.


@ulend

 ---

## Sources 
There are several sources for identifying a patient in HL7 messaging standards.

@ul

* IHE (Integrating the Healthcare Enterprise) 
* Standards of Practice for Patient Identification - Association of Surgical Technologists
* HL7 Version 2.x messages
* HL7 Version 3 - CCD messages
* HL7 FHIR 
* DICOM 

@ulend

---

### IHE (Integrating the Healthcare Enterprise)
IHE is a profiling organization. IHE provides Integration Profiles and Technical Frameworks that can be used for guidance in identifying Patient Identification.

---

### IHE IT Infrastructure Domain Profiles

![](https://i.imgur.com/hK55SpO.png)


---

IHE defines the  Patient Identifier Domain as a single system or a set of interconnected systems that all share a common identification scheme (an identifier and an assignment process to a patient) and issuing authority for patient identifiers. 

---

##  HL7 Profiles

There are three IHE profiles that support Patient Identification.

@ul

* Patient Identifier Cross Referencing (PIX)
* Cross-Community Patient Discovery (XCPD) 
* Patient Identifier Cross Referencing for HL7v3 (PIXv3)

@ulend

---

### Patient Identifier Cross Referencing (PIX)
The **Patient Identifier Cross Referencing (PIX)** profile supports the cross-referencing of patient identifiers from multiple Patient Identifier Domains.  HL7 V2.x is the message format.  Supports determination of matching patient identifiers (ADT^A01, A04, A05, A08, A31, A40; Q23)

+++

| Process Flow                         |
|:--------------------------------------|
| ![](https://i.imgur.com/H55QXWc.png) |
| *Source*: IHE                    |

---

### Cross-Community Patient Discovery (XCPD)
The **Cross-Community Patient Discovery (XCPD)** profile supports the means to locate communities which hold patient relevant health data.  



---

### Patient Identifier Cross Referencing for HL7v3 (PIXv3)
The **Patient Identifier Cross Referencing for HL7v3 (PIXv3)** profile provides cross-referencing of patient identifiers from multiple Patient Identifier Domains. HL7 V3 is the message format. 


+++

#### Actor and Transactions

![](https://i.imgur.com/YZhNcm2.jpg)    



---


## Dicom Profiles

### Patient Information Reconciliation (PIR)
This profile coordinates reconciliation of the patient record when images are acquired for unidentified (e.g. trauma), or misidentified patients. 

---

### Nuclear Medicine Image (NMI)
This profile specifies how Nuclear Medicine images and result screens are created, exchanged, used and displayed. 

---

## Workflows
### Scheduled Workflow (SWF) 
This workflow integrates the ordering, scheduling, imaging acquisition, storage and viewing activities associated with radiology exams.

---

Scheduled Workflow establishes a seamless flow of information that supports efficient patient care workflow in a typical imaging encounter. It specifies transactions that maintain the consistency of patient information from registration through ordering, scheduling, imaging acquisition, storage and viewing as shown in the following figure.

---

| Scheduled Workflow                   |
|:--------------------------------------|
| ![](https://i.imgur.com/TLKLCGd.jpg) |
| *Source*: IHE                      |



---

## Anatomy of a Dicom file
As we already know a DICOM file storing one image contain the image data and data belonging to the patient and data (name, age, etc.) belonging to the examination (date of acquisition, manufacturer, etc.) and identifiers: the study UID, the series’ UID’s, and the image UID’s.  

---

The software that interprets the image will have to be able to find, first of all, the part of the DICOM file containing the image; also all of the identifiers and the other data contained in the DICOM file. The DICOM standard has a special pair of characters, the parentheses and the comma: ’(’ and ’)’ and ’,’. Now, numbers of 2x4 hexadecimal digits enclosed by the these parentheses and separated by the comma uniquely identify a specific DICOM field or data. For instance this tag:

---

`(0010,0010)` is the identifier of the patient’s name - „ten-ten is the patient name” as DICOM experts would say. The last thing that we have to learn is that the data, in this case the patient name is enclosed by a pair of the tag shown above:

---



### Dicom-File-Format for Patient Identification

Here is a decoded segment of the DICOM information found in a DICOM file:

The following table defines the attributes relevant to identifying a patient

+++

| Attribute Name                    | Tag         | Attribute Description                    |
|:-----------------------------------|-------------|------------------------------------------|
| Patient's Name                    | (0010,0010) | Patient's full name                      |
| Patient ID                        | (0010,0020) | Primary identifier for the patient.      |
| Other Patient IDs                 | (0010,1000) | Other identification numbers or codes used to identify the patient. |
| Other Patient IDs Sequence        | (0010,1002) | A sequence of identification numbers or codes used to identify the patient, which may or may not be human readable, and may or may not have been obtained from an implanted or attached device such as an RFID or barcode. |
| Type of Patient ID                | (0010,0020) | The type of identifier in this item.<br>Enumerated Values: <br>TEXT <br><br>RFID <br><br>BARCODE |
| Other Patient Names               | (0010,1001) | Other names used to identify the patient. |
| Patient's Birth Name              | (0010,1005) | Patient's birth name.                    |
| Patient's Mother's Birth Name     | (0010,1060) | Birth name of patient's mother.          |
| Medical Record Locator            | (0010,1090) | An identifier used to find the patient's existing medical record (e.g., film jacket). |
| Referenced Patient Photo Sequence | (0010,1100) | A photo to confirm the identity of a patient.<br>Only a single Item is permitted in this Sequence. |



---


## Standards of Practice for Patient Identification - Association of Surgical Technologists

### Standard of Practice I
The use of two patient identifiers improves the reliability of the patient
identification process and decreases the chance of performing the wrong
procedure on the wrong patient. Additionally, the use of two patient identifiers is
necessary in the instances of a name patient alert because two (or more patients)
have the same name that can be spelled the same, close to being spelled the same
and/or pronounced the same.

---

>![](https://i.imgur.com/DiPYycK.png) NOTE: The patient’s room number should not be used as a patient identifier; room numbers are not person-specific identifiers, since patients can be moved from room to room

---

### Standard of Practice II
All patients undergoing a surgical procedure should wear an identifying marker.


---

## HL7 Version 2.x messages

### HL7 PID Segment
The HL7 PID segment is found in every type of ADT message (i.e. ADT-A01, ADT-A08, etc.) and contains 30 different fields with values ranging from patient ID number, to patient sex, to address, to marital status, to citizenship. The PID segment provides important identification information about the patient and, in fact, is used as the primary means of communicating the identifying and demographic information about a patient between systems. 

+++

The HL7 standard allows for several different types of patient identification numbers in the first four fields of the PID segment. 

| Sequence |           Element Name                               |
|----------|:------------------------------------------|
| PID-1:   | Set ID – Patient ID – a number to identify the transaction |
| PID-2:   | Patient ID (External ID) – the patient identifier number used by one or more outside institutions (i.e. a physician’s office that is referring the patient) |
| PID-3:   | Patient ID (Internal ID) – the primary, unique patient identifier number used by the facility |
| PID-4:   |  Alternate Patient ID – an alternate, additional, temporary or pending patient identification number |

---

#### Example
The PID segment is shown in red.

![](https://i.imgur.com/gSfnUe3.png)

---


## HL7 Version 3 - CCD
The Continuity of Care Document (CCD) is built using HL7 Clinical Document Architecture (CDA) elements and contains data that is defined by the ASTM Continuity of Care Record (CCR). It is used to share summary information about the patient within the broader context of the personal health record.


---


| CDA Template Types                   |
|:--------------------------------------|
| ![](https://i.imgur.com/92VwsBW.png) |
| *Source*:  HL7 Organization                                |


---




### Record Target Section
The recordTarget element of the header identifies the patient associated with the document and contains no narrative component.

+++

Example


 ```xml
    <recordTarget>
      <patientRole>

      <!-- CONF 5268-->
      <!-- Patient SSN recorded as an ID -->
      <id extension="123-456-7890" root="2.16.840.1.113883.4.1"/>

      <!-- CONF 5271 -->
      <addr use="HP">
         <!-- HP is "primary home" from codeSystem 2.16.840.1.113883.5.1119 -->
         <streetAddressLine>999 Huckleberry Ave, Apt #3</streetAddressLine>
         <city>Springfield</city>
         <state>PA</state>
         <postalCode>19064</postalCode>
         <country>US</country>
         <!-- US is "United States" from ISO 3166-1 Country Codes: 1.0.3166.1 -->
      </addr>

      <!-- CONF 5280 -->
      <telecom value="tel:+1(610)555-0000" use="HP"/>
      <!-- HP is "primary home" from HL7 AddressUse 2.16.840.1.113883.5.1119 -->

      <telecom value="tel:+1(610)555-1111" use="MC"/>
      <!-- MC is "mobile contact" from HL7 AddressUse 2.16.840.1.113883.5.1119 -->

      <!-- CONF 5283 -->
      <patient>

         <!-- CONF 5284 -->
         <name use="L">
            <!-- L is "Legal" from HL7 EntityNameUse 2.16.840.1.113883.5.45 -->
            <given>Jane</given>
            <family>Appleseed-Monroe</family>
         </name>
         <administrativeGenderCode code="F" codeSystem="2.16.840.1.113883.5.1"
            displayName="Female"/>
         <birthTime value="19770330"/>
         <maritalStatusCode code="M" codeSystem="2.16.840.1.113883.5.2"
            codeSystemName="MaritalStatus"/>

         <raceCode code="2076-8" displayName="Native Hawaiian or Other Pacific Islander"
            codeSystem="2.16.840.1.113883.6.238"
            codeSystemName="OMB Standards for Race and Ethnicity"/>
         <sdtc:raceCode code="2054-5" displayName="Black or African American"
            codeSystem="2.16.840.1.113883.6.238"
            codeSystemName="OMB Standards for Race and Ethnicity"/>
         <ethnicGroupCode code="2186-5" displayName="Not Hispanic or Latino"
            codeSystem="2.16.840.1.113883.6.238"
            codeSystemName="OMB Standards for Race and Ethnicity"/>

         <languageCommunication>
            <!-- CONF 5407: LanguageCode Code System 2.16.840.1.113883.1.11.11526 -->
            <languageCode code="en"/>
            <modeCode code="ESP" displayName="Expressed spoken"
               codeSystem="2.16.840.1.113883.5.60" codeSystemName="LanguageAbilityMode"/>
            <preferenceInd value="true"/>
         </languageCommunication>
      </patient>
   </patientRole>
</recordTarget>
```




---

## HIE Sources

---

### Record Locator Service  

**Record Locator Service (RLS)** — The Record Locator Service is the only new piece of infrastructure required by the Health Information Environment. A RLS is subject to privacy and security requirements, and is based on open standards set by the Standards and Policy Entity. 
The RLS holds information authorized by the patient about where authorized information can be found, but not the actual information the records may contain. It thus enables a separation, for reasons of security, privacy, and the preservation of the autonomy of the participating entities, of the function of locating authorized records from the function of transferring them to authorized users.  

+++

> ![](https://i.imgur.com/DiPYycK.png) INFO: Release of information from one entity to another is  subject to authorization requirements between those parties; in certain sensitive treatment situations patients or providers may choose not to share information. 
> * RLSs are operated by multi-stakeholder collaboratives at each sub-network and are built on the current use of Master Patient Indices.  
> * The Record Locator Service needs to enable a care professional looking for a specific piece of information (PCP visit or ER record) to find it rapidly. An open design question is how and where in the model this capability can best be accomplished.

---

## Message Processing



| Message Processing Workflow          |
|:------------------------------------|
| ![](https://i.imgur.com/laeKK2Y.png) |


---


The Message Processor provides all the capibilites of extracting Patient data from all HL7 Message Types.  The following are examples from a Message processor application.

---

### Processing HL7 ADT Message Types


| Processing HL7 ADT Message Types example |
|------------------------------------------|
| ![](https://i.imgur.com/y2QBfJq.png)     |


---




### Extracting Patient information from ADT Message Types


| Extracting Patient information from ADT Message Types example |
|:------------------------------------------|
| ![](https://i.imgur.com/GI6xHPQ.png)      |



---



### Extracting Patient information from FHIR resources


+++

| Extracting Patient information from FHIR Resources example |
|:------------------------------------------|
| ![](https://i.imgur.com/41aWKZ7.png)     |
| ![](https://i.imgur.com/CSHQPWi.png)     |





---

## Devices

### Device auto-provisioning



| Device auto-provisioning                 |
|:------------------------------------------|
| ![](https://i.imgur.com/KHScHE2.png)     |
| *source*: <a href="https://docs.microsoft.com/en-us/azure/iot-dps/concepts-auto-provisioning" target="_blank">Auto-provisioning concepts</a> |

### Device Configuration


---

| Configuration |
|:----------|
| ![](https://i.imgur.com/YLucNK8.png) |
| *source*: <a href="https://docs.microsoft.com/en-us/azure/iot-hub/tutorial-device-twins" target="_blank">Configure your devices from a back-end service </a>|



---

| Device Twins |
|:--------------|
| ![](https://i.imgur.com/DUwwlOg.png)    |
| *source*:   <a href="https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-device-twins" target="_blank">Understand and use device twins in IoT Hub</a>      |


---

+++

#### Device Twin example

```
{
    "deviceId": "devA",
    "etag": "AAAAAAAAAAc=", 
    "status": "enabled",
    "statusReason": "provisioned",
    "statusUpdateTime": "0001-01-01T00:00:00",
    "connectionState": "connected",
    "lastActivityTime": "2015-02-30T16:24:48.789Z",
    "cloudToDeviceMessageCount": 0, 
    "authenticationType": "sas",
    "x509Thumbprint": {     
        "primaryThumbprint": null, 
        "secondaryThumbprint": null 
    }, 
    "version": 2, 
    "tags": {
        "$etag": "123",
        "deploymentLocation": {
            "room": "OR234",
            "floor": "1"
        },
        "$etag": "124",
        "patient": {
            "id": "233x3dd3frr",
            'id2': "medddddd"
        
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            "$metadata" : {...},
            "$version": 1
        },
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            "batteryLevel": 55,
            "$metadata" : {...},
            "$version": 4
        }
    }
}
```

---


## Extended Patient Identification  

---

#### Facial Recognition 

@ol

1. When a patient is admitted, a front facing photo is taken.
2. The photo is stored either locally or in Azure Blob Storage.
3. The uri for the image is inserted into a HL7 Version 2.x OBX-5 message.
4. Once the Processor Service receives the message it is added to the HL7 FHIR Patient Resource.
5. When the patient is brought into  the Operating Room, a facial scan is performed. 
6. It is verified using the [Azure Cogitative Face API Service](https://docs.microsoft.com/en-us/azure/cognitive-services/face/overview).

@olend

---

The following figure shows the mapping between the HL7 Version 2.x and FHIR Patent Resource.

| Mapping |
|:--------------|
|![](https://i.imgur.com/hrWXZZO.png)   |
| *source*:   HL7 FHIR      |


---



## Post Surgury Reporting
The HL7 FHIR **Procedure Resource** is used to record the details of procedures performed on a patient.  

This resource provides summary information about the occurrence of the procedure and is not intended to provide real-time snapshots of a procedure as it unfolds.

---

The following is the resource template

```
{


  "resourceType" : "Procedure",
  // from Resource: id, meta, implicitRules, and language
  // from DomainResource: text, contained, extension, and modifierExtension
  "identifier" : [{ Identifier }], // External Identifiers for this procedure
  "definition" : [{ Reference(PlanDefinition|ActivityDefinition|
   HealthcareService) }], // Instantiates protocol or definition
  "basedOn" : [{ Reference(CarePlan|ProcedureRequest|ReferralRequest) }], // A request for this procedure
  "partOf" : [{ Reference(Procedure|Observation|MedicationAdministration) }], // Part of referenced event
  "status" : "<code>", // R!  preparation | in-progress | suspended | aborted | completed | entered-in-error | unknown
  "notDone" : <boolean>, // True if procedure was not performed as scheduled
  "notDoneReason" : { CodeableConcept }, // C? Reason procedure was not performed
  "category" : { CodeableConcept }, // Classification of the procedure
  "code" : { CodeableConcept }, // Identification of the procedure
  "subject" : { Reference(Patient|Group) }, // R!  Who the procedure was performed on
  "context" : { Reference(Encounter|EpisodeOfCare) }, // Encounter or episode associated with the procedure
  // performed[x]: Date/Period the procedure was performed. One of these 2:
  "performedDateTime" : "<dateTime>",
  "performedPeriod" : { Period },
  "performer" : [{ // The people who performed the procedure
    "role" : { CodeableConcept }, // The role the actor was in
    "actor" : { Reference(Practitioner|Organization|Patient|RelatedPerson|
    Device) }, // R!  The reference to the practitioner
    "onBehalfOf" : { Reference(Organization) } // Organization the device or practitioner was acting for
  }],
  "location" : { Reference(Location) }, // Where the procedure happened
  "reasonCode" : [{ CodeableConcept }], // Coded reason procedure performed
  "reasonReference" : [{ Reference(Condition|Observation) }], // Condition that is the reason the procedure performed
  "bodySite" : [{ CodeableConcept }], // Target body sites
  "outcome" : { CodeableConcept }, // The result of procedure
  "report" : [{ Reference(DiagnosticReport) }], // Any report resulting from the procedure
  "complication" : [{ CodeableConcept }], // Complication following the procedure
  "complicationDetail" : [{ Reference(Condition) }], // A condition that is a result of the procedure
  "followUp" : [{ CodeableConcept }], // Instructions for follow up
  "note" : [{ Annotation }], // Additional information about the procedure
  "focalDevice" : [{ // Device changed in procedure
    "action" : { CodeableConcept }, // Kind of change to device
    "manipulated" : { Reference(Device) } // R!  Device that was changed
  }],
  "usedReference" : [{ Reference(Device|Medication|Substance) }], // Items used during procedure
  "usedCode" : [{ CodeableConcept }] // Coded items used during the procedure
}
```

---

## References
<a href="http://library.ahima.org/PdfView?oid=302331" target="_blank">AHIMA STANDARDS FACT SHEET</a>  

<a href="http://bok.ahima.org/doc?oid=79237#.W0Tj-_ZFxTc" target="_blank">Patient Identification in Three Acts </a>  

<a href="https://www.ihe.net/" target="_blank">Integrating the Healthcare Enterprise (IHE)</a>  

<a href="https://www.himss.org/" target="_blank">Healthcare Information and Management Systems Society (HIMSS)</a>  

<a href="http://www.ast.org/" target="_blank">Association of Surgical Technologists</a>  

<a href="https://www.dicomstandard.org/" target="_blank">DICOM</a>  

<a href="http://www.hl7.org/" target="_blank">Health Level Seven International (HL7)</a>  

<a href="http://hl7.org/fhir/" target="_blank">FHIR® – Fast Healthcare Interoperability Resources</a>  

<a href="https://docs.microsoft.com/en-us/azure/iot-fundamentals/" target="_blank">Azure IoT Fundamentals</a>

---

---?image=assets/cognizant-log-small.png&position=center&size=25%
