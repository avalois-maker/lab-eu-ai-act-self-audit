# System Brief — EU Policy RAG Assistant
## What does the system do?

The system allows employees to ask questions about relevant EU legislation and policy guidance through a chat interface. It searches a controlled collection of policy documents stored by the organization, identifies passages that are relevant to the employee's question, and uses those passages to generate a written answer.

The system is designed to answer questions only using information contained in the organization's approved document collection. If the available documents do not contain sufficient information to answer a question, the system should indicate that it cannot provide an adequate answer and direct the employee to the organization's policy team for further assistance.

The purpose of the system is to reduce the number of routine questions that policy staff need to answer manually and provide employees with faster access to existing policy information.

## What inputs does it take?

The system has two primary types of input:

1. Knowledge-base documents

Documents are provided through a designated Google Drive folder. These documents contain EU legislation, regulatory guidance, and related policy information. Documents may be added, modified, or removed over time.
The prototype supports text-based documents and is being extended to support PDFs.

The documents are processed by n8n, divided into smaller sections, converted into numerical representations using an embedding model, and stored in a Pinecone vector database so that relevant sections can be retrieved when a question is submitted.

The documents are organizational policy materials rather than customer records. The intended knowledge base does not require personal data to perform its function. However, the system operates within an enterprise environment, so access permissions and the possibility of personal or confidential information being inadvertently included in documents need to be considered before production deployment.

2. Employee questions

An employee submits a natural-language question through the chat interface. In the prototype, the question is passed through an n8n workflow, which searches the vector database for relevant document sections.

## What does the system output?

The primary output is generated text: an answer to the employee's question based on the relevant sections retrieved from the organization's documents.

The system can also produce an insufficient-information/escalation response when the available documents do not provide an adequate basis for answering the question.

The intended production response should identify the source document or documents used to formulate the answer, allowing the employee and policy team to verify the information.
The system does not make an automated legal, employment, financial, or other binding decision. It provides informational responses based on the organization's supplied documents.

## Who is affected by the output?

The immediate users are employees of the organization, particularly employees in departments that regularly require information about EU legislation and policy.

The policy department is also affected because the system is intended to reduce routine information requests while providing a mechanism for escalating questions that cannot be adequately answered.

There is no intended direct impact on customers or members of the public.

## Does a human review the output?

Yes, during the evaluation and initial implementation phase.

A specialist from the policy department reviews generated responses to determine whether they provide an adequate and appropriately grounded answer to the employee's question.

The review is used to evaluate system performance and identify cases where the retrieval process or generated response needs improvement.

In the proposed production model, routine responses would be provided directly to employees without requiring manual approval of every individual response. Questions for which the system cannot find sufficient supporting information should instead be escalated to the policy department.

This creates a human-in-the-loop escalation model rather than requiring human approval of every automated response.

## Who built it?

The prototype was designed and implemented by the project owner, using existing organizational technology and third-party AI infrastructure.

The workflow was configured in n8n, with Google Drive used as the document source, Pinecone used as the vector database, OpenAI used for language-model processing, and Slack intended as the employee-facing conversational interface.

The project owner is responsible for the workflow design, configuration, testing, and iteration. The underlying platforms and models are provided by third-party technology providers.

## Who would use it in production?

The intended production users are employees of the organization, particularly employees who currently contact the policy department for information about EU legislation and related policy guidance.

The policy department would remain responsible for the underlying source material, validating system performance, and answering questions that the system cannot adequately address.

The organization's IT/technology function would be responsible for supporting the production environment, access controls, integrations, and operational security.

## System boundary

The system's responsibility is limited to retrieving and presenting information contained within the organization's approved policy-document collection. It is not intended to independently research the internet, interpret legislation beyond the supplied material, provide authoritative legal advice, or make decisions on behalf of the organization.

The key audit question is therefore not simply whether the system produces plausible answers, but whether it retrieves the appropriate organizational information and produces answers that remain grounded in that information without introducing unsupported claims.

# Risk Tier Classification

| **Question**                                                                                             | **Your answer**                                                                                                                                                                                                                                                                                                                                      |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Does this system fall under any prohibited category (Article 5)?**                                     | **No.** The system retrieves information from an organization's approved EU legislation/policy documents and generates answers to employee questions. It does not use prohibited practices such as social scoring, manipulation, exploitation of vulnerabilities, biometric categorization, or other practices listed in Article 5.                  |
| **Does this system operate in any of the eight Annex III areas?**                                        | **No, based on the current use case.** The system is intended to provide employees with information about EU legislation and policy guidance. It is not being used for biometrics, critical infrastructure, education, employment, essential services, law enforcement, migration/border control, or administration of justice/democratic processes. |
| **If Annex III: does it "significantly influence" decisions in that area, or is it narrow/preparatory?** | **N/A.** Because the system does not fall within an Annex III area based on the stated use case, the "significantly influence" test does not currently apply.                                                                                                                                                                                        |
| **Does this system interact with end users or generate content requiring disclosure (Article 50)?**      | **Yes.** The system interacts directly with employees through a chat interface and generates AI-produced text. Article 50 transparency requirements should therefore be considered, including making users aware that they are interacting with an AI system and that the responses are AI-generated.                                                |
| **First-pass risk tier**                                                                                 | **Limited risk / transparency obligations.** The system does not appear to be prohibited or high-risk under the stated use case, but Article 50 transparency obligations apply because it interacts directly with users and generates AI content.                                                                                                    |
| **One-sentence justification citing the specific article or Annex entry**                                | **The system is not prohibited under Article 5 and does not fall within the Annex III high-risk use cases; because it directly interacts with employees and generates AI-generated text, it should be treated as a limited-risk system subject to the applicable transparency requirements under Article 50.**                                       |

# Role Map

| **Role**                   | **Entity**                                                                                                                                                    | **Key AI Act obligations**                                                                                                                                                                                                                                                                                                                                                            |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Provider**               | **Your project team / organization if it develops and puts the RAG assistant into service under its own name**                                                | Ensure the system meets applicable requirements, particularly **Article 50 transparency** because it directly interacts with employees. If the organization is only configuring an existing AI system and does not place the complete system into service under its own name, the provider classification should be confirmed.                             |
| **Deployer**               | **The European used-goods platform / client organization**                                                                                                    | Use the system according to its intended purpose, follow provider instructions, ensure appropriate human oversight where applicable, and comply with applicable transparency obligations. Employees using the system under the organization's authority are generally **not separate deployers**; the organization is the deployer.                        |
| **Vendor (if applicable)** | **OpenAI** — underlying LLM/model provider; **n8n/Pinecone/Google** may also be relevant depending on the final architecture and data processing arrangements | The vendor is responsible for the obligations applicable to the AI system/model it provides. For your RAG application, the vendor's exact AI Act role depends on whether it is providing the underlying model, an AI system, or simply infrastructure/software. The organization should document the vendor's applicable obligations and ensure the overall system remains compliant. |

# Compliance Memo

# AI Act Compliance Memo — EU Policy RAG Assistant

**To:** Head of Product
**Subject:** AI Act compliance assessment — EU Policy RAG Assistant

## 1. System classification

The EU Policy RAG Assistant is a **limited/transparency-risk AI system rather than a prohibited or high-risk system**, because its current purpose is to retrieve and generate information for employees and it does not fall within the prohibited practices in Article 5 or the high-risk use cases listed in Annex III.

## 2. Role map

The **client organization is the deployer** because it uses the RAG assistant under its authority for employees. If the client develops and puts the complete RAG assistant into service under its own name, it may also be considered the **provider** under the AI Act; OpenAI is the provider of the underlying model, while n8n, Pinecone and Google Drive are technology/infrastructure vendors whose precise AI Act roles depend on how each component is supplied and used.

## 3. Key findings

**First, users need to know they are interacting with AI.** Because the assistant directly interacts with employees, the system should clearly inform users that they are interacting with an AI system. Article 50 transparency obligations apply from 2 August 2026.

**Second, the system's scope needs to remain controlled.** The current use case is an internal knowledge assistant and does not appear to fall within an Annex III high-risk category. If the organization later uses the system to make or materially influence decisions concerning employees, customers, access to services, law enforcement or another regulated area, the classification should be reassessed.

**Third, AI-generated responses should be identifiable where the applicable Article 50 requirements require it.** The provider of a generative AI system has obligations concerning machine-readable marking of AI-generated content, subject to the applicable exceptions. The implementation should therefore be reviewed against the Commission's current Article 50 guidance before production deployment.

## 4. Recommended next steps

**(1) First, document the intended purpose and boundaries of the assistant.** Confirm that it is limited to retrieving and explaining information from the organization's approved EU-policy documents and cannot make decisions on behalf of the organization.

**(2) Second, implement Article 50 transparency controls before production.** Clearly identify the assistant as AI-powered in the employee interface and assess the appropriate technical mechanism for identifying AI-generated responses.

**(3) Third, complete a final legal and technical review before deployment.** Confirm the provider/deployer roles, the obligations applicable to OpenAI and other technology vendors, and whether any change in functionality could move the system into an Annex III high-risk category.

## 5. Caveats

This memo is a **first-pass compliance assessment**, not a legal opinion, conformity assessment, certification, or formal determination of compliance with the EU AI Act. The assessment is based on the current intended use and architecture; any material change to the system's purpose, users, data, or decision-making role should trigger a new risk classification review.
