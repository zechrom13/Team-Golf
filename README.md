# Project Idea & Aim
In our days, pharmacies are facing the challenge of repositioning themselves within the healthcare market. The challenge will be to differentiate itself from the retail market and position itself as a healthcare facility. Since the revision of the Therapeutic Products Act (TPA) in January 2019, pharmacies are allowed to sell certain drugs (drugs of category B+), which needed previously prescriptions from a general practinioner. In order to receive one of these B+ drugs, the customer needs to consult a pharmacist - a very time consuming consultation. Furthermore, due to the same revision, pharmacies lost their monopol of selling certain drugs (e.g. PANADOL S Filmtabl 500 mg) to drugstores (so called "Drogerien"). In summary, pharmacies are phasing more time consuming consultations and lose some of their current easy going sales to drugstores. One way to solve this problem is trying to shorten the time for each consultation, which could have the downgrade of a lower consultation-quality. Another way is to hire more pharmaceutical assistants, which leads to an increase of the expenses - an option that is not affordable for most pharmacies.

We would like to overcome this challenge by implementing a workflow system which is capable of handling minor, uncritical health issues fully automated on a chatbot-like screen in the pharmacy by following validated disease-specific guidelines. In our case, we will soley focus on automizing the process for a pharmacy consultation concerning common cold symptoms. The following conditions can be fulfilled by this use case:

- the health issue occures often enough that it is of economic significant
- no class A/B/B+ medications are involved (which require a prescription and/or an in-person consultation with name and address) 
- customer-preferences can be included (type of medicine: conventional medicine, phytopharmaceuticals or homeopathy; type of galenic forms: tablet, syrup, nasal spray, droplets etc.)
- there is a pre-defined therapeutic guideline (inlcuding 'red flags', which lead to a consultation with a pharmacist or a general practioner)
- it is a typical process flow, which could later be amended with other indications
- expected high costumer-acceptance rates due to convenience (privacy, no strenuous conversation while coughing/sniffling)
- minimizing direct human contact helps to contain the disease (the spread of the common cold can be contained by keeping distance)


# Process


## Process Description
The reader should imagine that there is a quiet corner in the pharmacy, where they can do the automated consultation on a touch screen.

The process is split in 2 sections:

1. Anamnesis
Questionnaire to define the symptoms and to rule out any 'red flag patients' who need further personal consultation by a pharmacist or a doctor.
2. Treatment decision
Based on the information from section 1, there are three possible outcomes (treatment decision ways)

    a. No further consultation is necessary (no red flag generated) and the customer can select his preferences for the type of medication and he gets suggestions for medications. He can directly pay at the self-service machine and gets the medication delivered there too (E.g. directly via an storage and dispensing robot like the one from BD ROWA)
    
    b. Consultation by the pharmacist is needed. The data entry from the chatbot gets transferred to a screen visible to the consulting pharmacist. The costomer receives a paper ticket with a number for the express consultation counter for people who use the self-service screen. (=incentive to use the self-service machine)
    
    c. A medical consultation is necessary at a general practitioner (GP). The data entry from the chatbot gets transfered to a screen visible to the consulting pharmacist (highlitet that a GP-consultation is recommended). The costomer receives a paper ticket with a number for the express consultation counter for people who use the self-service screen. (The pharmacist discusses the results with the customer and recommends (if necessary) a GP-appointment (or even books an appointment at a GP for the Customer))
   
## Process requirements



## BPMN model of process


# Autors
David Tschirky, pharmacist
Lukas Suter, pharmacist/insurance performance manager
Dominik Meyer, project manager??
Roman Zech, process developer 
