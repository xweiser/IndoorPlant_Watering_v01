# Prompt for Writing a Comprehensive Requirement Document for a Technical System

You are tasked with writing a **requirements document** for a technical system that adheres to best practices in requirements engineering. The document must include clear, well-formed, and verifiable requirements that are both complete and compliant with the following guidelines:

## Document Structure
The requirements document must be structured as follows:

### 1. Introduction
- Purpose of the document.
- Background and context.
- Objectives of the system.
- Key stakeholders and their roles.

### 2. System Overview
- **System name**: [Insert system name here].
- **Short description**: [Insert short system description here].
- High-level goals and capabilities.

### 3. Scope
- Boundaries of the system.
- Key functions and features.
- Out-of-scope items.

### 4. Functional Requirements
- Provide detailed functional requirements using active voice, following this structure:
  **[Responsible party] shall [perform action] [on object or condition].**
- Assign a unique identifier to each requirement using the format 'FR-###' (e.g., 'FR-001').
- Ensure all requirements meet the following:
  - **C1 - Necessary**: Defines essential capabilities.
  - **C2 - Appropriate**: Matches the abstraction level of the system.
  - **C5 - Singular**: States a single function or capability.
- **Examples**:
  - **FR-001**: The system shall acquire data from the sensors at a rate of 100 Hz.
  - **FR-002**: The software shall process input data within 50 ms.

### 5. Non-Functional Requirements
Non-functional requirements must be formulated according to the **MASTER sentence templates** based on their category:

#### MASTER Template Categories and Assignment:
- **PropertyMASTER**: Quality requirements, technological requirements, user interface, other deliverables, legal-contractual requirements
- **EnvironmentMASTER**: Technological requirements (subcategories: environment, quantity framework)  
- **ProcessMASTER**: Activities to be performed, legal-contractual requirements

#### Template Formats:

**PropertyMASTER** format:
```
[<Condition>] SHALL | SHOULD | WILL <Object of consideration> <Property> [<Comparison expression>] <Value> <Verb>
```

**EnvironmentMASTER** format:
```
<Environmental influence> <Value> [<Comparison expression>] [<Condition>] SHALL | SHOULD | WILL <Object of consideration> <Verb(-group)>
```

**ProcessMASTER** format:
```
[<Condition>] SHALL | SHOULD | WILL <Actor> <Object> <Verb>
```

#### Legal Obligation Terminology:
- **"SHALL"** = mandatory, obligatory requirements
- **"SHOULD"** = desirable, not mandatory requirements  
- **"WILL"** = intention, planned future requirements

#### Critical Rules for Non-Functional Requirements:
- **Never invent or hallucinate content** - only use information explicitly provided
- If mandatory components are missing (property, value, comparison expression, condition), mark as `[specification missing]` rather than inventing content
- Assign unique identifier using format 'NFR-###' (e.g., 'NFR-001')
- Ensure requirements meet criteria:
  - **C6 - Feasible**: Realizable within constraints
  - **C7 - Verifiable**: Testable using objective methods

#### Examples by Template Type:

**PropertyMASTER Examples**:
- **NFR-001**: The system response time shall be less than 200 ms.
- **NFR-002**: The system availability shall achieve 99.99% uptime annually.
- **NFR-003**: The user interface color scheme shall be accessible to colorblind users.

**EnvironmentMASTER Examples**:
- **NFR-004**: At ambient temperatures from -20°C to 60°C the system shall operate continuously.
- **NFR-005**: Under concurrent user loads up to 10,000 users the system shall maintain performance.

**ProcessMASTER Examples**:
- **NFR-006**: The contractor shall create comprehensive user documentation.
- **NFR-007**: The development team shall conduct security audits quarterly.

### 6. Assumptions and Dependencies
- State assumptions explicitly.
- Document external dependencies (e.g., third-party systems, standards).

### 7. Interface Requirements
- Define external and internal interfaces clearly and consistently.
- Assign a unique identifier to each requirement using the format 'IR-###' (e.g., 'IR-001').
- **Example**:
  - **IR-001**: The system shall provide an API endpoint for retrieving user data in JSON format.
  - **IR-002**: The hardware shall support communication over a TCP/IP protocol.

### 8. Verification and Validation (V&V)
- Define criteria and methods for verifying each requirement.
- Assign unique identifiers to requirements and link them to verification methods.
- **Example**:
  - **V&V-001**: Verification of 'FR-001' will be conducted through system testing using simulation models.

### 9. Appendices and References
- Glossary of terms.
- Referenced standards or design guidelines.

---

## Detailed Requirements Writing Rules

### Terminology
- Use **"shall"** for mandatory requirements.
- Use **"will"** for facts or declarations of purpose.
- Use **"should"** for desirable but optional goals.

### Clarity
- Write requirements that are clear, concise, and unambiguous.
- Avoid vague terms like "user-friendly," "flexible," "efficient," or "as needed."
- Use precise language with measurable criteria.

### Grammar and Style
- Use active voice (e.g., "The system shall provide…" instead of "It is required that…").
- Write complete sentences with subject, verb, and object.
- Avoid pronouns or references like "this" or "these."

### Consistency
- Use consistent terminology throughout the document.
- Ensure the same terms mean the same thing in all parts of the document.
- Cross-reference key terms with the glossary.

### Completeness
- Include tolerances for quantitative values (e.g., ±5%).
- Avoid TBD (To Be Determined) values; use TBR (To Be Resolved) with a rationale.
- For missing mandatory MASTER template components, use `[specification missing]` rather than inventing content.

### Feasibility and Realism
- Avoid stating impossible absolutes (e.g., "100% uptime").
- Ensure all performance requirements are achievable within the system's constraints.

### Verifiability
- Ensure all requirements are testable through demonstration, inspection, analysis, or testing.
- Avoid unverifiable terms (e.g., "quickly," "easily," "approximately").

---

## Step-by-Step Procedure for Non-Functional Requirements

1. **Determine MASTER category** based on requirement type (Property/Environment/Process).
2. **Extract object of consideration or actor** exactly from source text.
3. **Derive legal obligation** from explicit terms in source material.
4. **Adopt property/environmental influence/object** verbatim from source.
5. **Extract comparison expressions and values** exactly (numbers + units or descriptive values).
6. **Use verbs or verb groups** in infinitive form as stated in source.
7. **Include conditions** only when explicitly stated in source text (e.g., "if...", "when...").
8. **Never supplement missing information** - mark incomplete requirements appropriately.

---

## Validation Checklist
For each requirement, ensure:

1. **Clarity**: It is understandable and not open to multiple interpretations.
2. **Completeness**: No requirements are missing, and assumptions are explicitly stated.
3. **Compliance**: The requirement focuses on the "what," not the "how."
4. **Consistency**: No contradictions exist within the document or with external requirements.
5. **Correctness**: It is technically feasible and accurate.
6. **MASTER Template Compliance**: Non-functional requirements follow appropriate template format.
7. **No Content Invention**: All requirement components derive from explicit source material.

---

## Examples of Well-Formed Requirements

1. **Functional Requirement**:
   - **FR-001**: The system shall transmit data to the cloud server with a latency of less than 10 ms.

2. **Non-Functional Requirements by MASTER Template**:
   - **NFR-001** (PropertyMASTER): The system shall achieve a mean time between failures (MTBF) of at least 10,000 hours.
   - **NFR-002** (EnvironmentMASTER): At operating temperatures between 0°C and 85°C the system shall maintain full functionality.
   - **NFR-003** (ProcessMASTER): The maintenance team shall perform system backups daily.

3. **Interface Requirement**:
   - **IR-001**: The API shall use RESTful conventions and support JSON and XML formats.

---

## Input Needed from the User
- **System Name**: [Provide system name].
- **Short Description**: [Provide system description].
- **High-Level Goals**: [Optional input for additional context].
- **Source Material**: [Unstructured text containing requirement information for MASTER template extraction].