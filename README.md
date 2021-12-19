# DigiBP Group Project  -  Fall Semester 2021 - Group golf
Lukas Suter, Dominik Meyer, Roman Zech, David Tschirky



# Table of Contents
- [Project Idea & Aim](#project-idea-and-aim)
- [Process](#process)
    - [Process Description](#process-description)
	- [Process Requirements](#process-requirements)
	- [BPMN Model of the Process](#bpmn-model-of-the-process)
- [Outlook](#outlook)
- [Authors](#authors)
- [Additional Information](#additional-information)
    - [Pictures](#pictures)


# Project Idea and Aim
In our days, pharmacies are facing the challenge of repositioning themselves within the healthcare market. The challenge will be to differentiate themselves from the retail market, instead become a healthcare facility. Since the revision of the Therapeutic Products Act (TPA) in January 2019, pharmacies are allowed to sell certain drugs (drugs of category B+), which previously needed a prescription of a medical doctor. In order to receive one of these B+ drugs, the customer needs to consult a pharmacist - generally a very time consuming process. Furthermore, due to the same revision, pharmacies lost their monopoly of selling certain OTC drugs ("over the counter drugs", e.g. PANADOL S Filmtabl 500 mg) to drugstores (so called "Drogerien"). In summary, pharmacies are facing more time consuming consultations and lose some of their sales to drugstores. One way to solve this problem is trying to shorten the time for each consultation, which might result in a reduction of consultation-quality. Another way is to hire more pharmaceutical assistants, which leads to an increase of the expenses - an option that is not affordable for most pharmacies.

We would like to overcome this challenge by implementing a workflow system which is capable of handling minor, uncritical health issues fully automated on a chatbot-like screen in the pharmacy by following validated disease-specific guidelines. As an illustrative example, we will focus exclusively on automatizing the process for a pharmacy consultation concerning common cold symptoms. The following conditions can be fulfilled by this use case:

- the health issue occurs often which makes it economically significant
- no class A/B/B+ medications are involved (which require a prescription and/or an in-person consultation with a pharmacist) 
- customer-preferences can be included (type of medicine: conventional medicine, phytopharmaceuticals (herbal medicine) or homeopathy; type of galenic forms: tablet, syrup, nasal spray, droplets etc.)
- there is a predefined therapeutic guideline (including 'red flag symptoms', which lead to a consultation with a pharmacist or a general practitioner) for this illness [see Picture 1](###picture1)
- the process flow is built in a way which allows easy expansion with additional indications (illnesses)
- expected high customer-acceptance due to convenience (privacy, no strenuous conversation while coughing/sniffling)
- minimizing direct human contact helps to contain the disease (the spread of the common cold can be contained by keeping distance)


# Process

## Process Description
The reader should imagine that there is a quiet corner in the pharmacy, where the customer can do the automated consultation on a touch screen.

The process is split in two main sections:

1. Anamnese
Questionnaire (Google forms) to define the customer's symptoms and decide whether the customer is suitable for self medication or if further personal consultation is needed. 
2. Consultation decision
Based on the information from section 1, there are two possible outcomes (treatment decision ways)

    a. No pharmacist consultation is necessary and the customer can select his preferences for the type of medication. According to the preferences, the machine suggests medication options which are selected by the customer. The medication is delivered to the customer (e.g. via a storage and dispensing robot like the one from BD ROWA). Process ends.
    
    b. Consultation with the pharmacist is needed. A paper ticket with the instance ID is printed for the customer. After an in-person consultation with the pharmacist, the customer can get the drugs needed. Process ends.

## Process Restrictions
The following simplifications were made:
- the payment process was not implemented
- the interface with the robotic dispense system was not created
- no timer events were built into the process (for example when a customer starts a process at the automated consultation screen but leaves the process at a random point without finishing it)

## BPMN Model of the Process
![full BPMN model](https://github.com/DigiBP/Team-Golf/blob/e7fc38f122b44648b8dd4b898901827432557bee/Final_PictureBPMN_SICK-OMAT.png)

## Process Details
### Google Forms
At the start of the process (or better said before and with this form our process gets triggered) the customer fills in a form to gather information regarding illness, sympotoms and treatment preferences to provide as the base for the two following automated decisions. The form already contains shortcuts in case a 'red flag symptom' occurs that should be consulted by a person. 

The form can be accessed [here](https://forms.gle/QF4Y9ke4k3DrpKF39).

### Loading form
With Integromat we watch out for new answers to our form every minute. If a form arrives, we add a random number (0-1000), later called key and post all answers as a message to the heroku REST API to have the answers available in Camunda. (Thanks to Maja for spotting the surplus comma in the json file)

### Choose consultation channel
Based on the answers there is an automated decision decising the consultation channel. If no red flag sympotoms get detected, an automated medication delivery is possible (upper path). If consultation, a doctor visit or further annamese is needed because of certain sympotoms (acc. to the [photo](https://user-images.githubusercontent.com/68386983/144747725-eb9af31f-c111-4efb-ba93-af1e028c0937.png) in the appendix). 

### Automated consultation channel
Based on the set preferences by the user, he receives a personalized suggestion for treatment like at counter with all medications needed to treat his/her cold. 
_Side note: For a real world application we would need to check first, whether the medication is available before we suggest it to the customer._

The customer can then decide on the medication he/she wants of the list and submit the request to an external service (e.g. a BD Rowa) who gathers the medication from some auto-store solution. As we do not have such a service available, we simplified with Integromat: A webhook checks whether a new instance is entering the process step 'Deliver Medication' and triggeres the service in Integromat whereby the ID is fetched&locked, a delivery status (in our case always OK, but in reality the actual status of the delivery) as a variable sent back to Camunda.

### Personal consultation by pharmacist channel
If personal consultation is needed we print a ticket with the key for the customer and send make all the variables from the GForms visible for the consulting pharmacist.

# Outlook
The digitalized process presented in this readme is a simplified example of digitalization in a health care process. The following aspects complicate digitalization in this area:
- complexity: medicine is not an accurate science. Knowledge is mostly gained out of a (more or less) representative population that does not necessarily represent the individual accurately. Therefore additional control mechanisms are needed to protect those not represented by study populations. In our case, the model should be refined i.a. in the following aspects:
    - age: certain OTC medication is not suitable for elderly people. Differentiating only between <18 years old or older is not enough.
    - allergies: people with allergies to certain APIs (active pharmaceutical ingredients) need special attention
    - pregnancy: many OTC drugs are contraindicated during pregnancy or while breastfeeding

For further refinement of the process, the following points should be considered:
- integration of an existing anamnese REST API (e.g. Sublimd) to broaden field of use
- after completing self-anamnese which requires further consultation with the pharmacist, user data could be transmitted to pharmacist via webservice or interface with the pharmacy management system
- connect automated system with the pharmacy management system (contains customer data and medication history of known customers, stock information, prices)
    - customer data: if the customer could for example use a customer card barcode to log in to the automated system, information like age, other medication or allergies would be available to the automated system
    - stock information and prices: an integration of the stock database enables - instead of suggesting the same nose spray for every customer with a congested nose - medication suggestions dependent on the current availability, expiration date of products in stock or the margin from current purchasing conditions.
    - in this case, data privacy/security becomes an issue: medical data is particularly worth protecting. in our example, the process is kept anonymous.
- in principle, extensions for data gathering (measurement of basic biomarkes such as body temperature or blood pressure) could be added via sensors attached to the machine
- fun, interactive 3D animations of a human body might help the customer to indicate where he/she has got problems (like pain or rash)
- sound examples (sound of dry, irritable coughing vs. productive cough with mucus) or pictures (dermatological problems) could be presented to the customer, to help him self-diagnose
- in times of COVID-19, the selection of predefined symptoms could redirect the customer to a COVID test reservation tool

Instead of Google Forms, the implementation of a chatbot would be possible for the purpose of information gathering (anamnese). The chatbot could work with voice recognition. Technically it was easier to not implement a chatbot. It would include quite some programming to serve the same purpose as the Google Forms we used.
Medical anamnese is a highly complex procedure. The use of AI is an interesting approach. The more narrow the area of diagnosis is, the easier it is to train a model (e.g. detection of breast cancer in mammography pictures). For now, a broad spectrum of possible diagnoses requires the cooperation of human experience with artificial intelligence. For now.
After all, the solution presented here could as well be used as a self-dieagnosis tool combined with a webshop.


# Additional Information

## Abbreviations, Definitions
Expression | Explanation
| :------------- | :-------------
API | active pharmaceutical ingredient = the chemical that causes the therapeutic effect
red flag symptom | a symptom of an illness which requires thorough (differential) diagnosis
OTC drug | over the counter drugs = drugs that can be bought in pharmacies without a doctor's prescription
drug category | categories A, B, B+, C, D. Drugs are categorized in the approval process by the Swiss Agency for Therapeutic Products (Swissmedic). For drugs of lists A and B, a prescription is always needed. B+ requires at least a personal consultation with a pharmacist. C drugs will be listed B+ or D in the next few years and they require a consultation with a pharmacy employee. D drugs can also be sold in "Drogerien".
galenic form | pharmaceutical formulation, which can be a tablet, capsule, sirup, eye drops, etc.
BD Rowa | robotic system in modern pharmacies to store and automatically dispense drugs [see video](https://www.youtube.com/watch?v=erayPdbMNu0)

## Pictures
### Picture1
![Anamnese](https://user-images.githubusercontent.com/68386983/144747725-eb9af31f-c111-4efb-ba93-af1e028c0937.png)
_Selbstmedikation für die Kitteltasche, K. Lennecke/K. Hagel, 7. Auflage, Deutscher Apotheker Verlag_
