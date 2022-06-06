# THM - Principles of Security

[TryHackMe | Principles of Security](https://tryhackme.com/room/principlesofsecurity)

> Michael Jack | 06/2022

---

## Task 1 - Intro

> The following room is going to outline some of the fundamental principles of information 
> security. The frameworks used to protect data and systems to the elements of what exactly makes data secure.
> 
> The measures, frameworks and protocols discussed throughout this room all play a small part in "Defence in Depth."
> 
> Defence in Depth is the use of multiple varied layers of security to an organisation's systems and data in the hopes that multiple layers will provide redundancy in an organisation's security perimeter.

---

### Task 2 - The CIA Triad

The CIA triad is a security model to be considered throughout security policy.

- Confidentiality
  
  - Keeping information only accessible to those who should have access.

- Integrity
  
  - Information should stay accurate and consistent unless authorized changes are made.

- Availability
  
  - In order for data to be useful, it must be available and accessible by the user.

> Q: What elenet of the CIA triad keep unauthorized people from altering data?

```
Integrity
```

> Q: What element makes sure that data is available?

```
Availability
```

> Q: What element ensures that data is only accessed by authorized people?

```
Confidentiality
```

---

### Task 3 - Principles of Privileges

> The levels of access given to individuals are determined on two primary factors:
> 
> - The individual's role/function within the organisation
> - The sensitivity of the information being stored on the system

Two key concepts in managing access rights are **Privileged Identity Management** (PIM) and **Privileged Access Management** (PAM).

> PIM is used to translate a user's role within an organisation into an access role on a system. Whereas PAM is the management of the privileges a system's access role has, amongst other things.

It's also important to consider the principle of least privilege. Users should have the minimum access to accomplish their tasks. 

> Q: What does PIM stand for?

```
privileged identity management
```

> Q: What does PAM stand for?

```
privileged access management
```

> Q: If you wanted to manage the privileges a system access role had, what methodology would you use?

```
PAM
```

> Q: If you wanted to create a system role that is based on a users 
> role/responsibilities with an organisation, what methodology is this?

```
PIM
```

---

## Task 4 - Security Models Continued

> According to a security model, any system or piece of technology storing information is called an information system, which is how we will reference systems and devices in this task.

### The Bell-La Padula Model

> The Bell-La Padula Model is used to achieve confidentiality. This model has a few assumptions, such as an organisation's hierarchical structure it is used in, where everyone's responsibilities/roles are well-defined.
> 
> The model works by granting access to pieces of data (called objects) on a strictly need to know basis. This model uses the rule "no write down, no read up".

### Biba Model

> The Biba model is arguably the equivalent of the Bell-La Padula model but for the integrity of the CIA triad.
> 
> This model applies the rule to objects (data) and subjects (users) that can be summarised as "no write up, no read down". This rule means that subjects **can** create or write content to objects at or below their level but **can only** read the contents of objects above the subject's level.

The Biba model is used in organisations or situations where integrity is more important than confidentiality. For example, in software development, developers may only have access to the code that is necessary for their job. They may not need access to critical pieces of information such as databases, etc.

> Q: What is the name of the model that uses the rule "**can't** read up, can read down"?

```
The Bell-La Padula Model
```

> Q: What is the name of the model that uses the rule "**can** read up, can't read down"? 

```
The Biba Model
```

> If you were a mility which would you use?

```
The Bell-La Padula Model
```

> Q: If you were a software developer, what security model would the company perhaps use?

```
The Biba Model
```

---

## Task 5 - Threat Modeling & Incident Response

> Threat modelling is the process of reviewing, improving, and testing the security protocols in place in an organisation's information technology infrastructure and services.

There are different frameworks to help constuct thrat models.

 **STRIDE** (**S**poofing identity, **T**ampering with data, **R**epudiation threats, **I**nformation disclosure, **D**enial of Service and **E**levation of privileges) is one.

**PASTA** (**P**rocess for **A**ttack **S**imulation and **T**hreat **A**nalysis) is another.

A breach of securt is an **incident** and is responded to by a **CSIRT** (Computer Securty Incident Response Team). Incidents are classified based on urgency and impact and resolving them is **Incident Response**.

> Q: What model outlines "spoofing"?

```
STRIDE
```

> Q: What does "IR" stand for?

```
Incident Response
```

> Q: You are tasked with adding some measures to an application to improve the integrity of data, what STRIDE principle is this?

```
Tampering
```

> Q: An attacker has penetrated your organisation's security and stolen data.
>  It is your task to return the organisation to business as usual. What 
> incident response stage is this?

```
Recovery
```

---






