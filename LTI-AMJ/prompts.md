Persona: Act as a Senior Software Architect and Product Manager specialized in EdTech and the LTI (Learning Tools Interoperability) standard.

Objective: Design the first version (v1) of a new LTI-compliant software platform. The goal is to provide a seamless integration between external learning tools and Learning Management Systems (LMS) like Canvas, Moodle, or Blackboard.

Required Artifacts (Markdown Format):
Please deliver the following sections in a single, structured Markdown document:

Product Overview: A brief description of the LTI software, its added value for the EdTech ecosystem, and its competitive advantages (e.g., security, ease of integration, data analytics).

Core Functionality: An explanation of the main functions (LTI Advantage support, Deep Linking, Grade Passback).

Lean Canvas: A text-based Lean Canvas diagram representing the business model.

Use Cases: Description of the 3 primary use cases (e.g., Instructor Tool Setup, Student Tool Access, Automatic Grading). Include a Mermaid.js syntax diagram for each.

Data Model: A detailed model covering entities (User, Context, Tool, ResourceLink, Score), their attributes (name and type), and their relationships.

High-Level System Design: An architectural explanation (Cloud-native, Microservices vs. Monolith) with an accompanying C1/System Context diagram in Mermaid.js.

C4 Diagram (Component Level): A detailed C4 Component diagram (Mermaid.js) focusing on the "LTI Provider Service" or "Authentication Module."

Constraints:

Use professional, technical language.

Ensure diagrams use Mermaid.js syntax so they can be rendered in Markdown viewers.

Focus on scalability and compliance with 1EdTech standards.

Strategy for Delivery
To fulfill your assignment requirements effectively, follow these steps once the AI generates the content:

1. File Organization
Create a local folder named LTI-AMJ (e.g., LTI-JD). Inside, create two files:

LTI-AMJ.md: The main documentation.

prompts.md: The prompt provided above.

2. Refining the Data Model
When checking the output, ensure the data types follow standard conventions. For example:

IDs: UUID or String.

Timestamps: DateTime.

Relations: Ensure 1:N or N:M mappings are clearly stated.

3. C4 Diagram Focus
The prompt asks the AI to choose a component for the C4 diagram. Usually, the LTI Tool Provider Service is the best choice to showcase, as it handles the OAuth2/OIDC flow, which is the "heart" of LTI security. 

4. Lean Canvas Format
Since Markdown doesn't support complex grid layouts natively, the prompt asks for a "text-based" diagram. Use mermaid syntax for diagrams
