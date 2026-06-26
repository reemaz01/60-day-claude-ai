Day 26
Build a Prior Authorization Workflow Simulator
Prior Authorization Workflow Simulator

Project Overview

The Prior Authorization Workflow Simulator is an interactive web-based application that demonstrates the healthcare prior authorization process between patients, healthcare providers, and insurance payers.

The simulator helps users understand how authorization requests move through different stages, the factors affecting approval decisions, and how delays impact overall workflow efficiency.

---

Problem Statement

Prior authorization is a time-consuming healthcare process that often causes treatment delays due to incomplete documentation, medical necessity reviews, and insurance approval requirements.

This simulator provides an educational and visual representation of that workflow.

---

Objectives

- Simulate the complete prior authorization process.
- Visualize workflow stages.
- Demonstrate approval, denial, and pending scenarios.
- Track processing days and efficiency.
- Provide an interactive learning experience.

---

Features

Dynamic Patient Scenarios

The simulator randomly selects one of several authorization cases:

- Lumbar Spine MRI
- Elective Knee Surgery
- Specialty Medication
- Inpatient Admission

Workflow Stages

1. Patient Intake
2. Provider Referral
3. Medical Necessity Review
4. Documentation Collection
5. Submission to Payer
6. Decision
7. Resolution

Decision Logic

Each scenario has a predefined medical necessity score that determines the probability of:

- Approved
- Pended
- Denied

If denied, users can file an appeal.

If pended, users perform a Peer-to-Peer review before approval.

---

User Interface

The application includes:

- Dashboard header
- Progress tracker
- Patient lane
- Provider lane
- Payer lane
- Status panel
- Restart/New Patient button

---

Technologies Used

- HTML5
- CSS3
- JavaScript (Vanilla)

No external frameworks or backend services are required.

---

Workflow

1. User starts a new patient case.
2. A scenario is selected randomly.
3. Patient information enters the workflow.
4. Provider evaluates medical necessity.
5. Required documents are collected.
6. Request is submitted to the payer.
7. The payer generates one of three outcomes:
   - Approved
   - Pended
   - Denied
8. If necessary, Peer-to-Peer review or Appeal is completed.
9. Final approval and efficiency metrics are displayed.

---

Performance Metrics

The simulator tracks:

- Total processing days
- Workflow efficiency
- Authorization status
- Current workflow stage

---

Future Improvements

- Real patient information forms
- Provider login
- Insurance-specific rules
- PDF document uploads
- Analytics dashboard
- Database integration
- User authentication
- AI-assisted medical necessity review

#HTML File
Prior Authorisation Simulator
https://github.com/reemaz01/60-day-claude-ai/blob/8c915f15974c1527b6f7dbb03bf582ab880fe22c/Prior_Authorization_Workflow_Simulator.html
