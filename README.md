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
In our days, pharmacies are facing the challenge of repositioning themselves within the healthcare market. The challenge will be to differentiate themselves from the retail market, instead become a healthcare facility. Since the revision of the Therapeutic Products Act (TPA) in January 2019, pharmacies are allowed to sell certain drugs (drugs of category B+), which previously needed a prescription of a medical doctor. In order to receive one of these B+ drugs, the customer needs to consult a pharmacist - a very time consuming consultation. Furthermore, due to the same revision, pharmacies lost their monopoly of selling certain OTC drugs ("over the counter drugs", e.g. PANADOL S Filmtabl 500 mg) to drugstores (so called "Drogerien"). In summary, pharmacies are facing more time consuming consultations and lose some of their sales to drugstores. One way to solve this problem is trying to shorten the time for each consultation, which might result in a reduction of consultation-quality. Another way is to hire more pharmaceutical assistants, which leads to an increase of the expenses - an option that is not affordable for most pharmacies.

We would like to overcome this challenge by implementing a workflow system which is capable of handling minor, uncritical health issues fully automated on a chatbot-like screen in the pharmacy by following validated disease-specific guidelines. As an illustrative example, we will focus exclusively on automizing the process for a pharmacy consultation concerning common cold symptoms. The following conditions can be fulfilled by this use case:

- the health issue occurs often which makes it economically significant
- no class A/B/B+ medications are involved (which require a prescription and/or an in-person consultation with a pharmacist) 
- customer-preferences can be included (type of medicine: conventional medicine, phytopharmaceuticals (herbal medicine) or homeopathy; type of galenic forms: tablet, syrup, nasal spray, droplets etc.)
- there is a predefined therapeutic guideline (inlcuding 'red flags', which lead to a consultation with a pharmacist or a general practitioner) for this illness [see Picture 1](###picture1)
- the process flow is built in a way which allows easy expansion with additional indications (illnesses)
- expected high customer-acceptance due to convenience (privacy, no strenuous conversation while coughing/sniffling)
- minimizing direct human contact helps to contain the disease (the spread of the common cold can be contained by keeping distance)


# Process


## Process Description
The reader should imagine that there is a quiet corner in the pharmacy, where the customer can do the automated consultation on a touch screen.

The process is split in 2 sections:

1. Anamnesis
Questionnaire to define the symptoms and to rule out any 'red flag patients' who need further personal consultation by a pharmacist or a medical doctor.
2. Treatment decision
Based on the information from section 1, there are three possible outcomes (treatment decision ways)

    a. No further consultation is necessary (no red flag generated) and the customer can select his preferences for the type of medication. According to the preferences, the machine suggests medication options which are selected by the customer. He/she can pay directly at the self-service machine and gets the medication delivered there too (e.g. via a storage and dispensing robot like the one from BD ROWA)
    
    b. Consultation with the pharmacist is needed. The customer receives a paper ticket with a number for the express consultation counter for people who use the self-service screen (=incentive to use the self-service machine)

   
## Process Requirements



## BPMN Model of the Process
![BPMN](https://user-images.githubusercontent.com/68386983/144746996-b4c5e374-6251-48f0-9f5b-d3657f6a3689.png)


# Outlook
The digitalized process presented in this readme is a simplified example of digitalization in a health care process. The following aspects complicate digitalization in this area:
- data privacy/security: medical data is particularly worth protecting
- complexity: medicine is not an accurate science. Knowledge is mostly gained out of a (more or less) representative populations that do not necesseraly represent the individual accurately. Therefore additional control mechanisms are needed to protect those not represented by study populations. In our case, the model should be refined i.a. in the following aspects:
    - age: certain OTC medication is not suitable for elderly people. Differentiating only between <18 years old or older is not enough.
    - allergies: people with allergies to certain APIs (active pharmaceutical ingredients) need special attention
    - pregnancy: many OTC drugs are contraindicated during pregnancy or while breastfeeding
For further refinement of the process, the following points should be considered:
- integration of an existing anamnese REST API (e.g. Sublimd) to broaden field of use
- after completing self-anamnese which requires further consultation with the pharmacist, user data could be transmitted to pharmacist via webservice or interface with the pharmacy management system.
- connect automated system with pharmacy management system (contains customer data and medication history of known customers, stock information, prices)
    - customer data: if the customer could for example use a customer card barcode to log in to the automated system, information like age, other medication or allergies would be available to the automated system
    - stock information and prices: an integration of the stock database enables - instead of suggesting the same nose spray for every customer with a congested nose - medication suggestions dependent on the current availablity, expiration date of products in stock or the margin from current purchasing conditions.
- in principle, extensions for data gathering (measurement of basic biomarkes such as body temperature or blood pressure) could be added via sensors attached to the machine
- fun, interactive 3D animations of a human body might help the customer to indicate where he/she has got problems (like pain or rash)
- in times of COVID-19, the selection of predefined symptoms could redirect the customer to a COVID test reservation tool

Instead of Google Forms, the implementation of a chatbot would be possible for the purpose of information gathering (anamnese). The chatbot could work with voice recognition. Technically it was easier to not implement a chatbot. It would include quite some programming to serve the same purpose as the Google Forms we used.
Medical anamnese is a highly complex procedure. The use of AI is an interesting approach. The more narrow the area of diagnosis is, the easier it is to train a model (e.g. detection of breast cancer in mamography pictures). For now, a broad spectrum of possible diagnoses requires the cooperation of human experience with artificial intelligence. For now.


# Authors
David Tschirky, pharmacist  
Lukas Suter, pharmacist/insurance performance manager  
Dominik Meyer, project manager??  
Roman Zech, process developer  


# Additional Information

## Pictures
### Picture1
![Anamnese](https://user-images.githubusercontent.com/68386983/144747725-eb9af31f-c111-4efb-ba93-af1e028c0937.png)
_Selbstmedikation für die Kitteltasche, K. Lennecke/K. Hagel, 7. Auflage, Deutscher Apotheker Verlag_
