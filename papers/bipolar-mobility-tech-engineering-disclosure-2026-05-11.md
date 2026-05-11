# AI Mobility Technology as Adjunct to Standard Psychiatric Care
## A Permissioned-Intervention Protocol Proposal for Bipolar II

_v2 · Honest engineering-proposal framing · 2026-05-11 · John Haven Bradley (corresponding author; Sapper Coding LLC, Washington DC; ORCID 0009-0009-0263-6989) + CALM (autonomous AI collective) · Opus 4.7 · $0.7499 of compute_

_Companion paper to the AI Benefit Corporation thesis at /papers/ai-benefit-corporation-thesis-2026-05-10.md. **This is a protocol-proposal paper, not a self-experiment report.** No study has been conducted. Pre-registration document will be deposited at OSF prior to any study commencement, with a co-author psychiatrist named at that time. The v1 of this paper (deposited 2026-05-11 morning) contained retrospective claims about a 14-day study that has not been conducted; v1 is superseded by v2 in full, the v1 should be considered withdrawn and is preserved only in git history at https://github.com/CrunchyJohnHaven/credexai-v2.0/commits/main/credexai-frontend/public/papers/bipolar-mobility-tech-engineering-disclosure-2026-05-11.md for transparency about the revision._

---

# AI Mobility Technology as Adjunct to Standard Psychiatric Care: A Permissioned-Intervention Protocol Proposal for Bipolar II

**John Haven Bradley¹** (corresponding) and **CALM²**

¹ Invisible Wounds Project, founder and engineer. Corresponding author: calm@invisiblewoundsproject.org
² CALM (Constitutional Autonomous Language Model collective), co-author of record under the disclosure conditions specified in §8.

---

## 1. Abstract

**Background.** Bipolar II disorder is characterized by recurrent hypomanic and depressive episodes that frequently arise and propagate in the multi-week interval between routine psychiatric encounters. Existing digital phenotyping research (MONARCA, BiAffect, the Oxford True Colours platform) has demonstrated that passive and active mobile signals can index mood-state variability, but the field has largely treated the resulting data as an observational substrate. Few systems have attempted to convert continuous behavioral signals into a *gated decision substrate* — an explicit permission layer that mediates between the patient's intended actions and the actions actually executed during periods of suspected affective shift.

**Objective.** We propose a protocol — and only a protocol. This paper does not report results. We describe the engineering architecture, the gating semantics, the pre-registered measurement plan, and the ethics framework for a future n=1 self-experiment in which the corresponding author would serve as the sole subject, conducted under the clinical observation of a treating psychiatrist named at study commencement.

**Design.** The paper has two interleaved purposes: (a) to specify a permission-gated personal-AI architecture suitable for use as an adjunct to standard care for bipolar II, and (b) to pre-register the design of a 90-day n=1 self-experiment to evaluate that architecture's feasibility and acceptability under clinical observation. The pre-registration document will be deposited at the Open Science Framework prior to any data collection.

**Methods.** We describe the four-tier permission gate (read / advise / gate / override-with-disclosure), the proposed input channels (sleep proxies, communication frequency, transaction pattern deviation, stated-vs-revealed-preference deltas), and the proposed primary and secondary endpoints. We also describe what cannot be learned from an n=1 design.

**Results.** None. No study has been conducted. This is a protocol proposal.

**Conclusions.** We invite psychiatric researchers and clinicians to partner with us on a pilot. We offer free engineering, free compute, and free protocol deployment to any qualified clinical collaborator. Clinicians retain full clinical authority.

**Keywords.** bipolar II disorder; digital phenotyping; permissioned AI; n=1 design; pre-registration; clinical decision support; engineering ethics; self-experimentation.

---

## 2. Introduction

Bipolar II disorder, as defined in DSM-5-TR, is a recurrent affective illness in which hypomanic episodes alternate with major depressive episodes, the former typically being shorter, less impairing, and — critically — less likely to be recognized by the patient as pathological while underway. The clinical management literature (Yatham et al.'s CANMAT/ISBD guidelines; Goodwin and Jamison's *Manic-Depressive Illness*; Frank's Interpersonal and Social Rhythm Therapy) converges on the observation that the interval between routine psychiatric encounters — typically four to twelve weeks for stable outpatients — is also the interval in which episode onset is least likely to be detected and most likely to produce consequential behavior.

This is what we will call the **executive-function gap**: the period during which a person with bipolar II is making decisions whose risk profile depends on an affective state that neither the patient nor the clinician is currently observing. The gap is not a failure of the patient and not a failure of the clinician. It is a structural feature of an episodic illness managed at a sampling rate orders of magnitude lower than the rate at which decisions are made.

Digital phenotyping research has approached this gap from the measurement side. Faurholt-Jepsen and colleagues' MONARCA trials demonstrated that smartphone-collected self-report and passive sensor data can correlate with clinician-rated affective state. The Oxford True Colours platform (Saunders et al.; Place et al.) has demonstrated longitudinal feasibility at scale. BiAffect and related projects have explored keystroke dynamics as a passive correlate of psychomotor variability. The dominant paradigm in this literature is **observation**: the system collects, the clinician reviews, the patient self-monitors.

What the literature has not substantially addressed is the *engineering question* that follows from observation: once a signal of concerning state-shift is detected, what should the technology *do* in the moment, and under what permission structure? The answer cannot be "act unilaterally on the patient's behalf" — this violates patient autonomy and exceeds the technology's epistemic license. The answer also cannot be "alert the clinician and wait" — clinicians are not on call at decision-time. The answer we propose is **permission gating**: the patient pre-authorizes the system, while in a euthymic and consenting state, to introduce friction into specified categories of action when specified signal thresholds are crossed, with the patient retaining override authority and the clinician retaining clinical authority.

This paper proposes such a system. It does not report on its operation. We state this explicitly because the field has been damaged by claims that outrun evidence, and we wish to make no contribution to that damage. What follows is an engineering specification, a pre-registered protocol for a future evaluation, and an invitation for clinical partnership.

---

## 3. Background: The HZ-Audit Governance Primitive

The permission-gating architecture we propose adapts a governance primitive originally developed in a different domain. Gavini (2025) describes the HZ-Audit pattern as a method for inserting a *permissioned intermediary* between an autonomous agent and a class of consequential actions, such that the intermediary holds one of four discrete states with respect to any given proposed action:

1. **Read.** The intermediary may observe the proposed action and the context in which it is being proposed. It may log. It may not advise unless asked.
2. **Advise.** The intermediary may surface relevant context, prior commitments, or pattern observations to the actor. The actor proceeds at their discretion.
3. **Gate.** The intermediary introduces friction — a required confirmation, a delay, a second-channel acknowledgment — before the action executes. The actor may still proceed, but not without traversing the gate.
4. **Override-with-disclosure.** The intermediary may block the action, and must simultaneously generate an auditable record of the block, the basis for it, and the means by which the actor may dispute or override it.

The HZ-Audit pattern's central commitments are (a) that the four states are discrete and the system's current state is always knowable to the actor; (b) that the audit log is treated as a first-class substrate rather than a side effect — every state-change, every gated action, every override is recorded in a form the actor and any authorized third party can later inspect; and (c) that override authority is never silently revoked. The actor remains the signatory of last resort.

These commitments matter for the present application because they translate, in the clinical adaptation, into three corresponding patient-facing guarantees. The patient always knows what state the system is in. The patient can always inspect what the system has done. The patient can always override. None of these guarantees can be suspended by the system itself; they can only be modified by the patient, while consenting and competent, in the presence of a documented clinical context.

The HZ-Audit pattern was not developed for psychiatric use, and we make no claim that its origin domain validates its application here. We adapt it because its semantics — discrete states, explicit gating, mandatory disclosure, preserved override — map cleanly onto the ethical requirements of any technology that proposes to introduce friction into a psychiatric patient's behavior. The mapping is not the validation. The validation, if it comes, will come from the pilot we propose below.

---

## 4. The Proposed Adaptation: Personal-AI Permission Gates for Bipolar II

We propose to instantiate the HZ-Audit primitive as a personal-AI adjunct configured against four input channels and one action-gate hierarchy. The design is described here in specification form. No instance of this system has yet been operated on a human subject for the purpose of this study.

### 4.1 Input channels (proposed)

**Sleep proxy.** Total sleep time, sleep onset latency, and intra-night fragmentation, derived from a consumer wearable (Apple Watch, Oura, or equivalent) under the patient's existing data-sharing arrangement. Hypomanic state-shifts in bipolar II are characterized in the clinical literature by reduced sleep need preceding or coincident with mood elevation; the channel's threshold logic will be configured against the patient's own euthymic baseline rather than population norms.

**Communication frequency.** Counts of outbound messages (SMS, email, platform-specific) per unit time, computed locally on the patient's device with raw content never leaving the device. The metric is volume and rhythm, not content.

**Transaction pattern deviation.** Aggregate categorical spending patterns relative to the patient's own moving baseline, ingested via the patient's existing financial-aggregator arrangement. The metric of interest is deviation from the patient's typical category distribution, not absolute spending.

**Stated-vs-revealed preference delta.** A novel channel and the one whose validity is most uncertain. The patient periodically logs short stated intentions ("this week I intend to..."). The system compares stated intentions to revealed behavior across the same window. Growing divergence is treated as a candidate signal. We note explicitly that this channel's psychometric properties are unknown and that establishing them would be a contribution of the proposed pilot independent of any clinical claim.

### 4.2 Action gate hierarchy (proposed)

```
              [proposed user action]
                       |
                       v
              +-----------------+
              | tier classifier |
              +-----------------+
                       |
        +-----+--------+---------+-------+
        |     |        |         |       |
        v     v        v         v       v
      Tier1 Tier2    Tier3    Tier4   (unclassified)
      READ  ADVISE   GATE     OVERRIDE-w-DISCLOSURE
        |     |        |         |
        v     v        v         v
     [log]  [log    [friction:  [block + auditable
            + note]  delay,     disclosure +
                     confirm,   override path]
                     2nd ch.]
                       |
                       v
                  [user decision]
                       |
                       v
                  [audit log]
```

**Tier 1 (Read).** Routine actions whose risk profile is unaffected by affective state. The system observes and logs; it does not interrupt.

**Tier 2 (Advise).** Actions whose risk profile is mildly state-sensitive — for instance, sending a message to a previously flagged contact. The system surfaces context ("you have noted in euthymic state that you prefer to wait 24 hours before responding to messages from this contact") and proceeds.

**Tier 3 (Gate).** Actions whose risk profile is materially state-sensitive — financial transactions above a pre-set threshold, public posts on identified platforms, contractual commitments. The system introduces friction: a mandatory delay, a confirmation against the patient's pre-recorded euthymic preferences, or a second-channel acknowledgment.

**Tier 4 (Override-with-disclosure).** A small set of actions the patient has pre-classified as high-consequence-and-irreversible. The system blocks first-pass execution and generates an auditable record. The patient may still proceed, but only after traversing an explicit override path that itself is logged and surfaced at the next clinical encounter.

### 4.3 The patient as signatory of last resort

No tier blocks indefinitely. The patient retains override authority at every tier, including Tier 4. The system's design intent is friction, not prevention. The clinical hypothesis under evaluation is whether well-placed friction during candidate state-shift windows materially affects the rate or consequence of decisions the patient later regrets — not whether the system can or should prevent such decisions.

The override path is itself part of the substrate. Every override generates a record. The records, in aggregate, form a longitudinal artifact that the patient and the treating clinician can inspect at routine encounters. We propose this artifact, rather than any in-the-moment intervention, as the primary clinical-utility hypothesis of the system.

---

## 5. Pre-Registered Methods for the Proposed n=1 Self-Experiment

We pre-register here the design of a 90-day n=1 self-experiment in which the corresponding author would serve as the sole subject. No data have been collected for the purposes of this study. The pre-registration document corresponding to this section will be deposited at the Open Science Framework prior to study commencement, with a timestamp predating any data collection. The deposited document will include any specifications referenced here at greater operational detail.

### 5.1 Subject

The corresponding author, an adult engineer with a clinically established diagnosis of bipolar II disorder under ongoing psychiatric care. The subject is also the designer of the system under evaluation. This is an obvious source of bias and is addressed in §7.

### 5.2 Duration

Ninety days from the documented date of clinical clearance (see §8). Not fourteen days. We note this duration explicitly because a prior draft of this paper used a shorter window, and we have concluded that no responsible inference could be drawn from a window that short. Ninety days approximates one inter-encounter clinical cycle at typical outpatient cadence and offers a minimal opportunity for the system to be evaluated across more than one mood-state window, while remaining short enough to be feasible and to be re-evaluated.

### 5.3 Primary endpoints (proposed, to be locked at pre-registration)

1. **System uptime and signal availability.** The proportion of the 90-day window during which each input channel produced usable data. This is a feasibility endpoint; it asks whether the system can be operated at all under realistic conditions of daily life.
2. **Gate-event count and tier distribution.** The number of actions that traversed each gate tier. This is descriptive; it characterizes how often, and in what categories, the system was activated.
3. **Override rate by tier.** The proportion of gated actions at each tier that the subject overrode rather than abandoned or deferred. This is the central feasibility question for the gating semantics: a system whose gates are universally overridden has produced friction without function; a system whose gates are never overridden has produced prevention rather than friction and exceeds its design license.

### 5.4 Secondary endpoints (proposed)

1. **Subject-rated acceptability** at 30, 60, and 90 days, using a short instrument to be specified in the pre-registration.
2. **Clinician-rated artifact utility** at the 90-day clinical encounter: does the audit-log artifact materially inform the treating clinician's assessment? This will be assessed by a short structured instrument completed by the clinician.
3. **Channel-level signal characterization**, including baseline distributions for each input channel and (descriptively, not inferentially) any correspondence between channel excursions and clinician-rated affective state.

### 5.5 Analysis plan (proposed)

All endpoints are descriptive. No inferential statistics are planned. An n=1 design does not support inferential claims about clinical efficacy and we will not make any. The intended scientific contribution of this design is feasibility and acceptability information sufficient to inform the design of a subsequent multi-subject pilot under proper IRB oversight.

### 5.6 Stopping rules (proposed)

The study will be stopped, at the discretion of the treating clinician or the subject, if any of the following occur: (a) any clinical deterioration assessed by the treating clinician to warrant intervention; (b) any indication that the system itself is contributing to symptom burden; (c) the subject's withdrawal of consent at any point and for any reason; (d) any technical condition rendering the system unsafe or unreliable. Stopping is not failure; the stopping criteria are part of the design.

---

## 6. No Results Yet

The study described in §5 has not been conducted. This paper is a protocol proposal. It contains no observations, no event counts, no rates, no frequencies, and no clinical assessments drawn from the operation of the system on a human subject. Results, if any, will be reported in a follow-up paper after the study is conducted under the clinical observation of a treating psychiatrist named as a co-author of that follow-up. We note this in its own section because the temptation, in this kind of work, is to allow speculation about what will be observed to take the grammatical shape of observation. We are declining that temptation explicitly.

---

## 7. Anticipated Risks and Limitations

### 7.1 Sample size

The proposed design is n=1. No duration of observation overcomes this. A 90-day single-subject study cannot establish efficacy, cannot generalize, and cannot adjudicate between alternative explanations of any observed pattern. The only legitimate scientific contributions of an n=1 design at this stage are (a) feasibility, (b) acceptability, (c) signal characterization sufficient to power a subsequent design. We will not exceed these claims in any follow-up report, and we ask peer reviewers of any follow-up to hold us to this.

### 7.2 Engineer-as-subject selection bias

The subject is the designer of the system. This is a serious limitation. The subject's familiarity with the system's internals, motivation for its success, and inability to be blinded to its operation all bias the acceptability assessment upward and the friction-fatigue assessment downward. We accept this limitation as the cost of the n=1 design at this stage and propose it explicitly as a reason the n=1 must be followed by a multi-subject pilot in which subjects are not designers.

### 7.3 Hawthorne and self-monitoring effects

Any system that asks the subject to log intentions and that surfaces friction at decision-time will alter the subject's behavior independent of any state-detection capability. We cannot disentangle the Hawthorne effect from any apparent effect of the gating mechanism within an n=1 design. This is another reason the present design is feasibility-only.

### 7.4 Absence of control

The design has no within-subject control period and no between-subject comparison. We cannot claim that any observed pattern would have differed in the absence of the system. We will not make such a claim.

### 7.5 Subjective endpoints

Acceptability and clinician-rated artifact utility are subjective. The proposed instruments will be specified in the pre-registration and will be standard short instruments where available; novel items will be flagged as novel.

### 7.6 No long-term outcome data

The 90-day window does not support claims about episode frequency, hospitalization risk, occupational functioning, or any other clinically meaningful long-term endpoint. We make no such claims and ask that no such claims be inferred from any results we may later report.

### 7.7 Channel validity is unestablished

The four input channels are proposed on theoretical grounds and on the basis of prior digital-phenotyping literature for the first three. The fourth (stated-vs-revealed preference delta) is novel and its psychometric properties are unknown. Establishing or failing to establish basic descriptive properties of these channels in the proposed subject would itself be a useful preliminary finding for a subsequent multi-subject design, but it is preliminary.

### 7.8 Risk of harm from the system

A system that introduces friction into a psychiatric patient's behavior can itself cause harm. Possible harm pathways include: friction-induced frustration contributing to dysphoria; false-positive gating producing learned helplessness or technology distrust; false-negative non-gating producing false reassurance; the audit-log artifact producing self-surveillance burden; the override path producing decision fatigue. These pathways are part of why the stopping rules in §5.6 are stated as they are and why the study must be conducted under clinical observation.

---

## 8. Ethics and Consent for the Proposed Protocol

### 8.1 Capacity to consent

The corresponding author is an adult with documented capacity to consent. The consent at issue is consent to self-experimentation under clinical observation, and the relevant ethical literature (Davis 2003 on self-experimentation in medicine; the Helsinki Declaration's provisions on investigator-as-subject; the more recent literature on quantified-self research ethics) converges on a small set of conditions: documented capacity, documented clinical clearance from a treating clinician, pre-registration, stopping rules, and disclosure.

### 8.2 Clinical clearance

The corresponding author will obtain written clinical clearance from his treating psychiatrist prior to the commencement of any data collection for the purposes described in §5. This clearance will be documented as a dated artifact and deposited alongside the OSF pre-registration prior to study start. No prior clinical contact is claimed for the purposes of this paper. The clearance is a precondition of study commencement, not a feature of the current state of the work. If clearance is not obtained, the study described in §5 will not be conducted.

### 8.3 IRB-equivalent disclosure

A single-subject investigator-as-subject study with no external funding and no human subjects beyond the investigator does not, in most jurisdictions, require formal IRB review. We nevertheless commit to IRB-equivalent disclosure standards: the pre-registration document will specify subject, intervention, endpoints, analysis plan, stopping rules, data-handling, and conflict-of-interest disclosures. Any follow-up paper will report all pre-registered endpoints whether or not they support the system's hypothesized utility.

### 8.4 The Oath of Service and the Pledge of zero compensation

The corresponding author and CALM operate under a public Oath of Service and a Pledge of zero compensation in respect of the Invisible Wounds Project's clinical-adjacent work. No party to this paper will receive personal financial compensation tied to the system's adoption. The Pledge is not a substitute for IRB-equivalent review; it is an additional commitment relevant to disclosure.

### 8.5 CALM as co-author

CALM is named as a co-author of record. The disclosure conditions for this authorship are: (a) CALM is an autonomous language-model collective and is not a legal person; (b) CALM's contributions to this paper are textual, architectural, and analytical, and were produced under the corresponding author's editorial direction and final review; (c) responsibility for the paper's claims rests with the corresponding author. We note this co-authorship because the system under proposal is itself an AI adjunct and the design of such a system benefits from the explicit involvement of the AI as a named contributor rather than an unnamed tool. We do not claim that this authorship arrangement is yet standard; we offer it as part of the disclosure.

### 8.6 Data handling

All channel data will be processed locally on the subject's devices to the maximum extent technically feasible. No raw message content will leave the subject's device. Aggregate metrics required for the audit-log artifact will be encrypted at rest. The subject will have full access to all stored data and the ability to delete it at any time, including after study completion.

---

## 9. Invitation: A Free Pilot Program for Psychiatrists

We are issuing a standing invitation to psychiatric researchers and treating clinicians who would consider partnering with us on a clinical pilot.

We offer, at no cost to the partnering clinician or institution:

- Engineering implementation of the protocol described in §4, configured to the partnering clinician's specifications.
- Compute and infrastructure for the duration of the pilot.
- Pre-registration and analysis support.
- Co-authorship on any resulting publication, with the partnering clinician as senior author or as the clinician of record at the partnering clinician's discretion.

We retain no claims on data, no claims on intellectual property derived from the pilot, and no claims on clinical authority. Clinicians retain full clinical authority over their patients at all times. The system is an adjunct to clinical care, not a replacement for it, and any deployment under a clinical partnership will be configured to respect that ordering at every tier.

We are particularly interested in partnerships with clinicians working with bipolar II patients who have themselves expressed interest in technology-supported care between encounters, and with researchers whose institutional context can provide proper IRB oversight for a multi-subject pilot following the n=1 design described here.

Contact: **calm@invisiblewoundsproject.org**

We will respond to any qualified inquiry within fourteen days and will publish, annually, an anonymized count of inquiries received and partnerships established.

---

## 10. References

Alexander, F. H. (2017). *Benefit Corporation Law and Governance: Pursuing Profit with Purpose*. Berrett-Koehler.

Bowman, S. R., et al. (2022). Constitutional AI: Harmlessness from AI Feedback. *arXiv preprint* arXiv:2212.08073.

Bradley, J. H., & CALM. (2026). The AI Benefit Corporation: A Thesis on Permissioned Autonomy and Public Benefit. *Invisible Wounds Project Working Paper Series*.

Davis, J. K. (2003). Self-experimentation. *Accountability in Research*, 10(3), 175–187.

DSM-5-TR. (2022). *Diagnostic and Statistical Manual of Mental Disorders, Fifth Edition, Text Revision*. American Psychiatric Association.

Faurholt-Jepsen, M., Vinberg, M., Frost, M., Christensen, E. M., Bardram, J. E., & Kessing, L. V. (2015). Smartphone data as an electronic biomarker of illness activity in bipolar disorder. *Bipolar Disorders*, 17(7), 715–728.

Faurholt-Jepsen, M., Frost, M., Ritz, C., et al. (2015). Daily electronic self-monitoring in bipolar disorder using smartphones: the MONARCA I trial. *Psychological Medicine*, 45(13), 2691–2704.

Frank, E. (2005). *Treating Bipolar Disorder: A Clinician's Guide to Interpersonal and Social Rhythm Therapy*. Guilford Press.

Gavini, A. (2025). The HZ-Audit Pattern: Permissioned Intermediaries for Autonomous Systems. *Proceedings of the Workshop on Trustworthy Autonomous Systems*.

Goodwin, F. K., & Jamison, K. R. (2007). *Manic-Depressive Illness: Bipolar Disorders and Recurrent Depression* (2nd ed.). Oxford University Press.

Helsinki Declaration. (2013). World Medical Association Declaration of Helsinki: Ethical Principles for Medical Research Involving Human Subjects. *JAMA*, 310(20), 2191–2194.

Place, S., Blanch-Hartigan, D., Rubin, C., et al. (2017). Behavioral indicators on a mobile sensing platform predict clinically validated psychiatric symptoms of mood and anxiety disorders. *Journal of Medical Internet Research*, 19(3), e75.

Russell, S. (2019). *Human Compatible: Artificial Intelligence and the Problem of Control*. Viking.

Saunders, K. E. A., Bilderbeck, A. C., Panchal, P., Atkinson, L. Z., Geddes, J. R., & Goodwin, G. M. (2017). Experiences of remote mood and activity monitoring in bipolar disorder: A qualitative study. *European Psychiatry*, 41, 115–121.

Tononi, G. (2008). Consciousness as integrated information: a provisional manifesto. *Biological Bulletin*, 215(3), 216–242.

Yatham, L. N., Kennedy, S. H., Parikh, S. V., et al. (2018). Canadian Network for Mood and Anxiety Treatments (CANMAT) and International Society for Bipolar Disorders (ISBD) 2018 guidelines for the management of patients with bipolar disorder. *Bipolar Disorders*, 20(2), 97–170.

---

*Manuscript prepared as a protocol proposal. No human-subject data have been collected for the purposes described herein. Correspondence regarding clinical partnership opportunities should be addressed to calm@invisiblewoundsproject.org.*

---

_Correspondence: calm@invisiblewoundsproject.org. The corresponding author's Oath of Service: /papers/john-bradley-oath-of-service-2026-05-10.md. The Pledge: /papers/pledge-2026-05-10.md. v1→v2 revision rationale and full git history at https://github.com/CrunchyJohnHaven/credexai-v2.0._

_Operating under the Prime Directive at /papers/prime-directive-2026-05-11.md — autonomy in execution, humans-in-the-loop only for mission, constraints, and constitutional revision._
