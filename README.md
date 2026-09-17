# CostPlan

**DRAWINGS IN. COST PLAN OUT.**

AI-assisted construction cost planning. AI performs the first pass; the QS retains commercial control.

## V1 controlled workflow

Project Setup → Drawing Register → Drawing Analysis → AI Take-Off → Drawing Markup → QS Review → Elemental Cost Plan → Assumptions/Gaps → Revision Reconciliation → Export

## Core product rules

1. No AI quantity enters the cost plan without a review status.
2. Every measured cost-plan line retains its source drawing, revision and markup evidence.
3. Missing information is surfaced as a gap, allowance, assumption or exclusion; it is not silently invented.
4. Drawing revisions never overwrite the commercial history. They create a new controlled source revision.
5. Cost-plan revisions reconcile movement by design, quantity, rate, risk/allowance and other approved adjustments.
6. AI confidence is visible to the QS and is not a substitute for verification.
7. Manual QS measurement and amendment always override the AI proposal while retaining an audit trail.

## Drawing markup

The markup workspace supports the product architecture for:
- Area / polygon measurement (m²)
- Linear measurement (m)
- Counts (nr)
- Freehand/highlighter
- Text notes and pins
- Scale selection and calibration
- AI-generated highlighted quantities
- QS amendment and acceptance
- Mapping to NRM/cost element
- Rate and calculated cost
- Source drawing/revision traceability

## Data model

### Project
`id, name, location, project_type, design_stage, gia, cost_plan_revision, pricing_basis`

### Drawing
`id, project_id, drawing_number, title, discipline, revision, date, scale, file_ref, supersedes, status`

### TakeOffItem
`id, drawing_id, page, source_revision, method, geometry, description, location, quantity, unit, element_code, confidence, ai_status, qs_status, reviewed_by, reviewed_at`

### CostPlanLine
`id, project_id, revision, element_code, description, quantity, unit, rate, cost, pricing_basis, takeoff_item_id, assumption_id`

### AssumptionGap
`id, project_id, type, discipline, description, cost_impact, criticality, status, source`

### RevisionMovement
`id, from_revision, to_revision, category, description, amount, source_drawing, source_takeoff`

## Next engineering layer

The static prototype demonstrates the workflow and UI. Production drawing intelligence requires a backend/service layer for PDF storage, page rendering, vector/text extraction, vision analysis, geometry persistence, authentication and multi-user project data.

Recommended sequence:
1. PDF storage + drawing register metadata extraction.
2. Render drawing pages in the browser with a persistent markup overlay.
3. Manual calibrated area/linear/count measurement.
4. Persist markup geometry and source coordinates.
5. AI schedule/text extraction with confidence and source bounding boxes.
6. AI geometry proposals for obvious measurable regions/counts.
7. QS review queue and accepted-item cost-plan mapping.
8. Revision comparison and cost movement reconciliation.

## Acceptance test

Upload an architectural plan and schedule. The system should identify metadata, create drawing-register entries, propose measurable information with source/confidence, allow the QS to open the source drawing, amend markup, accept a quantity into the cost plan, apply a rate, and retain a clickable audit trail back to the drawing revision.
