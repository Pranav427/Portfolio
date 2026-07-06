# Brand Content Pack — Pranav Obili
**Version 1.0 — FROZEN**
*Derived from Brand OS v1.0. Do not edit. All future content derives from this document.*

---

# SECTION 1 — POSITIONING STATEMENT

**Primary (portfolio, LinkedIn, full introductions):**
> I build AI systems that reduce friction — turning complex, manual workflows into intelligent products that let people focus on work that actually matters.

**Short form (resume headline, GitHub bio, character-limited contexts):**
> AI Engineer · Building intelligent systems that reduce friction and create measurable value.

**One-word anchor (for internal clarity):**
> Systems thinker. Not model trainer.

---

# SECTION 2 — HERO SECTION

*Answers: Who am I? What do I build? Why keep scrolling?*

**Tag line** *(monospace, above the name)*
```
AI Engineer · Applied AI Builder · Intelligent Systems Developer
```

**Main headline**
```
Pranav
Obili
```

**Supporting statement** *(human, not definitional — the positioning statement lives elsewhere)*
```
I don't just train models.
I build the systems around them —
from problem to product.
```

**Primary CTA**
```
See My Work
```
*(Scrolls to Projects)*

**Secondary CTA**
```
Work With Me
```
*(Opens inquiry modal)*

**Design note:** The hero video carries the human presence. The copy carries the identity. Keep copy minimal. Let the face create connection; let the words define the work.

---

# SECTION 3 — ABOUT NARRATIVE

*Answers: How did I get here? Why AI? Where am I heading?*
*Does not repeat the hero. Does not repeat the Mission. Opens with the journey, closes with direction.*

**Section label:** `About`
**Heading:** `How I think about building.`

---

My path into AI wasn't a straight line. I started computer science because I enjoyed programming and problem-solving — but I didn't know what kind of problems I actually wanted to solve.

Two projects answered that question.

The first was classifying patient conditions from drug reviews — 13,944 records of unstructured, patient-written text. What absorbed me wasn't the model. It was the engineering process: understanding what the data actually represented, deciding how to represent language as numbers in a way that matched the problem, choosing an evaluation metric that reflected real performance rather than just producing a high figure. That process — from messy raw data to a functioning, deployed system — is what I now recognise as my natural mode of thinking.

The second was undergraduate research on face anti-spoof detection, published at ICETCI-2025 in the Springer Conference Proceedings. Working at publication depth taught me something different: that every design decision needs a justification you're willing to put in writing. That discipline hasn't left me.

Both experiences pointed to the same conclusion: I'm not interested in building models. I'm interested in building systems. A model is a component. A system is a solution. The distinction shapes every decision I make.

I graduated with a B.Tech in Computer Science and Engineering (CGPA: 8.66) and I'm currently building ApplySmart AI — an intelligent job application platform — while working toward an MSc in Artificial Intelligence.

---

# SECTION 4 — MISSION STATEMENT

*Answers: Why do I build intelligent systems? What is the purpose behind the work?*
*Owns the problem statement. Does not repeat the About narrative.*

**Section label:** `Mission`

---

Most workflows are more complicated than they need to be. Not because the underlying problems are hard — but because the right system hasn't been built yet.

People spend hours on tasks that shouldn't require human attention: navigating fragmented processes, repeating manual steps, making decisions without access to the data that would make those decisions obvious. That friction is a design failure, not an inevitability.

I build AI systems that close that gap. Not to replace human judgment — but to eliminate the parts of work that shouldn't require it in the first place, so people can focus on decisions that genuinely need them.

Every system I build is evaluated against one question: does this create real value for the people who use it? If the answer isn't clear, the system isn't ready.

---

# SECTION 5 — PROJECT CASE STUDIES

*Answers: What have I built? How did I think through it? What did I learn?*
*Each case study follows: Problem → Engineering Decisions → Architecture → Results → Lessons*

---

## Project 01 — Applied NLP · Machine Learning · Deployed System

# Patient Condition Classification Using Drug Reviews

**Status:** Complete · Live Demo · Open Source

### The Problem

Online drug review platforms contain thousands of patient-written accounts of their medical experiences. Inside that unstructured text is a signal: which condition is this patient actually describing?

Classifying patient conditions from free-text reviews has real applications in pharmacovigilance, health informatics, and clinical decision support. But the data is messy, class-imbalanced, and written in natural language — which is inconsistent, emotional, and rarely technically precise.

### Engineering Decisions

**Why Linear SVM over neural approaches?**
The dataset — 13,944 records — is sufficient for classical ML but too small to train a deep learning model from scratch without significant overfitting risk. Linear SVM with TF-IDF features offers interpretability, fast iteration, and strong performance on text classification at this scale. The choice was made based on constraints, not convention.

**Why TF-IDF over pre-trained embeddings?**
Word2Vec and GloVe embeddings are trained on general text. Medical language and patient-written reviews have a specific vocabulary that general embeddings represent poorly. TF-IDF captures term importance directly within this corpus, without importing assumptions from unrelated training data.

**Why VADER for sentiment?**
Patient reviews carry emotional signal — frustration, relief, uncertainty — that correlates with condition severity and treatment experience. VADER is a rule-based sentiment analyser built for informal text. Adding sentiment features enriched the representation without introducing a second learned model and its associated complexity.

**Why macro F1 over accuracy?**
Class imbalance meant a classifier predicting only the most frequent condition would achieve high accuracy while being practically useless. Macro F1 weights every class equally regardless of frequency — it is an honest measure of performance across the full distribution. Accuracy would have been a misleading metric here.

### Architecture

```
Raw Reviews
    ↓
Text Preprocessing
(cleaning · lowercasing · stopword removal)
    ↓
Feature Engineering
    ├── TF-IDF Vectorisation (unigrams + bigrams)
    └── VADER Sentiment Scores
    ↓
Linear SVM Classifier
    ↓
Hyperparameter Tuning (GridSearchCV)
    ↓
Evaluation (Accuracy · Macro F1 · Classification Report)
    ↓
Streamlit Deployment
```

### Results

| Metric | Score |
|---|---|
| Accuracy | 96.16% |
| Macro F1 | 94.60% |

The macro F1 of 94.60% across an imbalanced multi-class problem is the more meaningful figure. It demonstrates consistent performance across condition categories — not just on the most frequent ones.

### What I Learned

Metric selection is a design decision, not a formality. Choosing the wrong metric would have produced a model that looked good on paper and behaved poorly in practice. Thinking carefully about what "good performance" actually means in a specific problem context is now part of how I approach every modelling decision from the start.

**GitHub:** https://github.com/Pranav427/medical-condition-classification-drug-reviews-nlp
**Live Demo:** https://drug-review-nlp.streamlit.app/

---

## Project 02 — Computer Vision · Deep Learning · Published Research

# Face Anti-Spoof Detection

**Status:** Complete · Springer Publication · ICETCI-2025

### The Problem

Face recognition systems are used for authentication in banking, border control, and identity verification. They are vulnerable to presentation attacks: photographs, videos, 3D masks, or AI-generated faces presented to deceive the system.

Distinguishing a real, live human face from a spoofed presentation is a genuine security challenge. A system that can be defeated by a photograph of an authorised user is not a secure authentication system.

### Why This Was Research, Not a Project

This work was undertaken as undergraduate research — not a coursework exercise. The goal was to investigate whether transfer learning from a large pre-trained model could produce reliable anti-spoofing performance without requiring the dataset scale and computational infrastructure typically needed for security-critical vision systems.

### Engineering Decisions

**Why ResNet-50?**
ResNet-50 is a well-established convolutional architecture with demonstrated performance across vision tasks. Its residual connections address vanishing gradients in deep networks, and its ImageNet pre-training provides feature representations — particularly texture and edge detection — that transfer well to liveness and spoof detection.

**Why transfer learning rather than training from scratch?**
Training a deep network from scratch for a security task requires large, diverse datasets and significant compute. Transfer learning allowed the research to focus on the anti-spoofing problem itself — fine-tuning pre-learned representations on domain-specific data — rather than on infrastructure requirements.

**Why binary classification?**
The core security question is binary: real or presentation attack? A multi-class formulation (photo vs. video vs. mask attacks) would require a more diverse dataset and a more complex training regime. The binary framing allowed rigorous investigation of the fundamental problem.

### Architecture

```
Input Image
    ↓
Preprocessing (resize · normalisation · augmentation)
    ↓
ResNet-50 (ImageNet pre-trained)
    ↓
Fine-tuning on Anti-Spoof Dataset
    ↓
Binary Classification Head (Real / Fake)
    ↓
Evaluation (Accuracy · Precision · Recall · F1)
```

### Results

| Metric | Score |
|---|---|
| Accuracy | 94.04% |

94.04% on binary real/fake classification demonstrates that transfer learning from ResNet-50 is a viable approach for face anti-spoofing under constrained conditions — without large-scale data collection or training infrastructure.

### Publication

*A Modern Security Advanced System for Detection of Real or Fake Human Faces*
ICETCI-2025 · Springer Conference Proceedings

### What I Learned

Research depth and engineering execution reinforce each other. Understanding *why* a model works — the representational power of residual networks, the transferability of ImageNet features — makes it possible to make better decisions about *how* to apply it. Working at publication depth, where every decision needs a justification that can be written down and defended, built a rigour that has stayed with me.

---

## Project 03 — Flagship · AI Product · Intelligent Automation

# ApplySmart AI

**Status:** Active Development

### The Problem

Job searching doesn't ask people for their best thinking. It asks for their tolerance for administrative repetition.

Reading job descriptions to assess fit, adjusting resume language for each role, writing cover letters that follow predictable structures, tracking which applications went where — these tasks consume hours of a job seeker's time while requiring almost no genuine judgment. The actual decision — whether a role is worth pursuing — takes minutes. The surrounding process takes days.

The result is a system that doesn't select for the best candidates. It selects for people who can most efficiently perform administrative repetition.

### Why I'm Building This

ApplySmart AI is a direct response to the problem I care most about: human potential wasted on work that intelligent systems could handle. The job application process is one of the clearest examples of this problem I've encountered — and one where the technical components are well within the current state of AI capability.

This is not a portfolio demonstration. It is a product I intend to ship.

### Current Architecture

```
User Profile
    ↓
Job Discovery (structured job data ingestion)
    ↓
Job Ranking (relevance scoring against profile)
    ↓
Application Workspace
    ├── Job Description Analysis (NLP extraction)
    ├── Resume Tailoring (LLM-assisted personalisation)
    ├── Cover Letter Generation (contextual drafting)
    └── ATS Optimisation (keyword alignment)
    ↓
Application Tracking (status management)
    ↓
Workflow Automation
```

### What Is Built

- Profile management system
- Job discovery and ingestion pipeline
- Job ranking and relevance scoring
- Application tracking and status management
- Application workspace (in progress)

### Roadmap

**Near-term:** LLM-powered job description analysis · Resume personalisation engine · Cover letter generation

**Medium-term:** ATS optimisation · AI Agents for workflow automation · Intelligent recommendations

**Long-term:** Full application workflow automation · Platform integrations · Application analytics

### Why This Is the Flagship

ApplySmart AI is where every capability I've developed converges: NLP for text understanding, ML for relevance scoring, LLMs for content generation, systems architecture for the overall design, and product thinking for the user experience. It is the clearest expression of what it means to build a system rather than a model.

---

# SECTION 6 — RESEARCH NARRATIVE

*Answers: What have I investigated? Why does it matter? What did I learn from working at this depth?*
*Distinct from the project case study — this section addresses significance and intellectual development.*

**Section label:** `Research`
**Heading:** `Published Research`

**Publication:**
*A Modern Security Advanced System for Detection of Real or Fake Human Faces*
ICETCI-2025 · Springer Conference Proceedings

---

Face anti-spoofing has become more urgent as generative AI makes synthetic face creation more accessible. Authentication systems that rely on facial recognition — across banking, border security, and identity verification — are increasingly exposed to presentation attacks that didn't exist at scale five years ago.

My undergraduate research investigated a constrained version of this problem: whether transfer learning from a large pre-trained model could produce reliable real/fake face classification without the dataset scale and infrastructure typically required for security-critical applications.

The practical question was: how far can a well-chosen pre-trained model take you when resources are constrained? At 94.04% classification accuracy, the answer was — further than naive approaches, and into a range with genuine practical relevance.

What the research taught me mattered more than the result. Working at publication depth means every decision needs a justification that can be written down, defended, and reproduced by someone else. You cannot handwave away a design choice when it belongs in a methodology section. That discipline has shaped how I approach engineering work generally: decisions need reasons, and reasons need evidence.

The problem itself remains open. As generative AI continues to improve, anti-spoofing systems will need to evolve in response. This work is a contribution to that ongoing challenge — not a solution to it.

**Publisher:** Springer Nature · **Conference:** ICETCI-2025 · **Domain:** Computer Vision · Deep Learning · Transfer Learning

---

# SECTION 7 — CURRENT FOCUS

*Answers: What am I building now, and why does it matter?*
*Distinct from the ApplySmart case study — shorter, forward-looking, product-focused.*

**Section label:** `Currently Building`
**Heading:** `ApplySmart AI`
**Status badge:** `● Active Development`

---

Job searching asks the wrong thing of people. Not for their judgment — but for their patience with administrative repetition.

ApplySmart AI is an intelligent platform that handles the workflow — discovery, relevance scoring, resume tailoring, cover letter drafting, tracking — so the person can focus on the one thing that actually requires them: deciding which opportunities are worth pursuing and why.

The core architecture is in place. The next phase integrates LLMs for job description analysis and resume personalisation — the components that transform the platform from a structured tracker into an intelligent assistant.

This is not a side project. It is a product I intend to ship.

**Roadmap**
```
Phase 1  ████████████  Complete
         Profile · Discovery · Ranking · Tracking

Phase 2  ████░░░░░░░░  In Progress
         LLM Analysis · Resume Tailoring · Cover Letter Generation

Phase 3  ░░░░░░░░░░░░  Planned
         ATS Optimisation · AI Agents · Workflow Automation

Phase 4  ░░░░░░░░░░░░  Vision
         Full Automation · Platform Integration · Analytics
```

---

# SECTION 8 — TECHNICAL SKILLS

*Organised by capability — what can actually be built, not what technologies are known.*

**Section label:** `Skills`
**Heading:** `What I Can Build`

---

**Intelligent NLP Systems**
End-to-end natural language processing pipelines — from raw text through preprocessing, feature engineering, model selection, evaluation, and deployment. *Applied: patient condition classification, 96.16% accuracy, 94.60% macro F1, deployed on Streamlit.*
`Python · Scikit-learn · TF-IDF · VADER · NLTK · Streamlit`

---

**Computer Vision Systems**
Convolutional neural networks for image classification and security applications. Transfer learning from large pre-trained architectures for constrained problems. *Applied: face anti-spoof detection using ResNet-50, 94.04% accuracy, published.*
`Python · PyTorch · OpenCV · TensorFlow · ResNet-50`

---

**Machine Learning Engineering**
Complete ML pipelines: problem framing, data preprocessing, feature engineering, model selection, hyperparameter tuning, and evaluation strategy. Emphasis on choosing the right model for the right constraints.
`Python · Scikit-learn · Pandas · NumPy · Jupyter`

---

**LLM Integration** *(Active Development)*
Integrating large language models into intelligent workflows — job description analysis, contextual content generation, and automated reasoning pipelines. *Currently building for ApplySmart AI.*
`Python · LLM APIs · Prompt Engineering · Pydantic`

---

**AI System Design**
Designing complete intelligent systems: defining the problem, identifying components, choosing technologies based on constraints, and connecting everything into a working product.
*Applied: ApplySmart AI — full-stack AI product architecture.*

---

**Deployment and Engineering**
Building systems that ship — not prototypes that stay in notebooks.
`Streamlit · Git · GitHub · Docker · VS Code`

---

**Programming**
Python *(primary — all ML and AI work)* · SQL *(data querying)* · Java · C++ *(academic foundation)*

---

# SECTION 9 — ENGINEERING PRINCIPLES

*Answers: How do I think? What guides decisions?*
*Placed after Projects, Research, and Current Focus — so every principle is already supported by evidence the visitor has just seen.*

**Section label:** `Principles`
**Heading:** `How I Work`

---

**01 — Understand the problem before choosing the tool.**
Technology is a response to a problem, not the starting point. Before selecting a model, framework, or approach, the problem needs to be understood well enough to explain it to someone who knows nothing about AI.

**02 — The full system matters more than any single component.**
A well-trained model that isn't deployed hasn't solved anything. A deployed system with the wrong evaluation metric is measuring the wrong thing. Engineering means thinking about the complete pipeline — data, features, model, evaluation, and deployment — as a connected whole.

**03 — Choose the simplest approach that actually works.**
Complexity is not a signal of quality. For the NLP classifier, Linear SVM outperformed more complex alternatives — not despite its simplicity, but because its assumptions matched the problem's constraints. The right tool is the one that works, not the one that impresses.

**04 — Evaluation metrics are arguments, not scores.**
Choosing macro F1 over accuracy for the drug review classifier was a deliberate decision: class imbalance made accuracy a misleading measure. The choice of metric reflects how deeply a problem is understood. This principle extends beyond machine learning.

**05 — Research and engineering belong together.**
Research without engineering produces papers that don't ship. Engineering without research produces tools without understanding. The most reliable path to work that matters runs through both.

**06 — Measure what the system does for people, not how clever it is.**
A simpler system that works reliably for real users is worth more than a sophisticated system that performs well in benchmarks. The question is always: does this create genuine value?

---

# SECTION 10 — CONTACT SECTION

*Answers: What's next? Why should someone reach out?*
*Closes the portfolio with purpose and a clear invitation.*

**Section label:** `Contact`
**Heading:**
```
Let's build something
that matters.
```

---

If you're working on intelligent systems, exploring applied AI, or looking for someone who thinks carefully about both the engineering and the purpose behind it — I'd like to hear from you.

I'm currently open to AI engineering roles, research collaborations, and MSc opportunities.

**Footer line:**
```
Pranav Obili · AI Engineer · Applied AI Builder · Future AI Researcher
Andhra Pradesh, India
```

**Closing quote:**
```
"The best way to predict the future is to build it."
```

---

# FINAL CONSISTENCY REVIEW — V1.0 FREEZE CHECK

## 8 Issues Found and Resolved

| # | Issue | Resolution |
|---|---|---|
| 1 | Hero statement duplicated positioning statement | Rewritten — hero is now human/directional ("I don't just train models. I build the systems around them."), positioning statement is definitional |
| 2 | About para 4 duplicated Mission opening | About now ends on personal direction (MSc, ApplySmart). Mission owns the problem statement entirely |
| 3 | Current Focus duplicated ApplySmart case study opening | Current Focus is now shorter, forward-looking, product-framed. Case study is retrospective and decision-focused |
| 4 | Rejected positioning candidates retained in document | Removed. Only the chosen statements remain |
| 5 | Research narrative last line was weak | Replaced: "This work is a contribution to that ongoing challenge — not a solution to it." Honest and precise |
| 6 | CGPA 8.66 missing from all content | Added to About narrative, one line, factual |
| 7 | Contact copy had weak filler line | "I'm also always interested in conversations" removed. Contact is now direct and purposeful |
| 8 | Section label voice inconsistent | Standardised: About · Mission · Research · Currently Building · Skills · Principles · Contact |

## Brand OS v1.0 Compliance

| Check | Status |
|---|---|
| No buzzwords ("cutting-edge", "revolutionary", "passionate about AI") | ✓ Clear |
| Every claim backed by specific evidence | ✓ Clear |
| AI positioned as tool, not goal | ✓ Clear — About narrative, Mission, ApplySmart case study |
| Systems thinking over model training | ✓ Clear — Hero, About, all case studies, Principles |
| Calm, confident, precise voice throughout | ✓ Clear |
| No generic phrases without substance | ✓ Clear |
| CGPA included for academic audiences | ✓ Added |
| No overclaiming on LLM/AI Agent experience | ✓ Marked "Active Development" throughout |
| Research treated as evidence, not project | ✓ Separate section with distinct framing |
| Instagram excluded | ✓ Not present anywhere |

## Section Overlap Audit

| Pair | Risk | Status |
|---|---|---|
| Hero ↔ Positioning | Previously overlapping | ✓ Resolved — different registers |
| About ↔ Mission | Previously overlapping on problem statement | ✓ Resolved — About = journey, Mission = purpose |
| ApplySmart Case Study ↔ Current Focus | Previously near-identical opening | ✓ Resolved — different angles, different length |
| Research Narrative ↔ Anti-Spoof Case Study | Deliberate overlap — different purpose | ✓ Acceptable — Case Study = decisions, Research = significance |
| Engineering Principles ↔ About | Principles reference same projects | ✓ Acceptable — by design, principles land after evidence |

---

# APPROVED PORTFOLIO STRUCTURE

```
Hero
  ↓ Who am I?

About
  ↓ How did I get here?

Mission
  ↓ Why do I build?

Featured Projects (Case Studies)
  ↓ What have I built?

Research
  ↓ What have I investigated?

Currently Building — ApplySmart AI
  ↓ What am I building now?

Technical Skills
  ↓ What can I build?

Engineering Principles
  ↓ How do I think?

Contact
  ↓ What's next?
```

---

*Brand Content Pack v1.0 — FROZEN*
*Pranav Obili · AI Engineer · Applied AI Builder · Future AI Researcher*
*Source: Brand OS v1.0 · Implementation: Portfolio V3*
