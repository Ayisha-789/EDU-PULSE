# AgentSpec — EDU-PULSE Adaptive Revision Agent
**Team: New Stars**

**Department: Information Technology**

## 1. The Setting
A college student preparing for an upcoming examination has already studied a particular topic and wants to verify whether they are sufficiently prepared and understand the topic across its important concepts. The student usually rereads or revises the study material and then decides whether they are ready based mainly on their own confidence. However, rereading the material does not provide a systematic way to comprehensively check their understanding or discover weaknesses that they may not realize they have. This becomes especially difficult when the examination is approaching and the student has limited time to revise, as they may spend time reviewing concepts they already understand instead of focusing on the concepts that need more attention.

**Who exactly?**
A college student preparing for an upcoming examination who has already studied a particular topic and wants to confirm that they understand its important concepts well enough to confidently attempt the exam.

**What they do today?**
The student usually rereads or revises the study material and uses their own confidence to decide whether they are ready.

**Why is that hard?**
Rereading can make familiar information feel understood, but it does not reliably reveal which concepts the student has actually mastered and which concepts remain weak. This is particularly difficult when the exam is close and revision time is limited.

## 2. The problem this solves
A student studies a topic before an exam and feels that they understand it because they have read and revised the material. When they later try to check their preparation, they may find that they cannot answer some questions correctly. They know they have made mistakes, but they may not know exactly which concepts they are weak in or what they should revise next. So, they often go back and read the whole topic again, even though they already understand some parts, which wastes their limited revision time.

## 3. What we are building
**Input:**
The student provides a topic and its study material.

**Output:**
The agent produces a comprehensive quiz, concept-wise evaluation, identification of weak subtopics, targeted revision guidance, and follow-up quizzes until the required mastery level is reached.

**Never,however much a user wants it:**
The agent never declares the student ready based only on the overall score; it must check understanding of individual subtopics before finishing.

**Why this is agentic, in our own words:**
The agent keeps the student's progress and quiz results, decides which subtopic needs attention based on the student's answers, retrieves the relevant part of the uploaded material for revision, and chooses whether to finish or send the work back for targeted revision and another quiz. The student is part of the loop by answering the quizzes and confirming when they are ready to continue, and the workflow can pause for the student's response and resume later. The important difference from a normal AI quiz generator is that the agent does not simply generate questions and give a score—it evaluates the result, decides the next action, retrieves relevant learning material, and can move backwards through revision and retesting until the weak areas meet the required level.

## 4.A complete walkthrough
### Rules
- The agent first reads the student's uploaded study material and identifies the important concepts to be tested.
- The initial quiz covers the identified concepts.
- A concept is considered **not mastered if the student scores below 100%** on questions related to that concept.
- The student reaches the required mastery level when **every identified concept has a score of 100%**.
- If a concept is not mastered, the agent retrieves the relevant notes for that concept from the student's uploaded study material.
- The student rereads/revises the retrieved material and confirms when they are ready.
- The agent then generates a new targeted quiz specifically for that concept.
- If the student scores below 100% again, the agent repeats the **revision → re-testing** loop for that concept.
- The agent finishes only when **all identified concepts have reached 100%**.

### Step 1 — Student starts the revision session
**Student:** Ayisha

**Topic:** DBMS Normalisation

**Study material:** Uploaded DBMS Normalisation PDF

**The agent reads the material and identifies these important concepts:**

- Functional Dependencies
- 1NF
- 2NF
- 3NF
- BCNF
These concepts are covered in the uploaded material.

### Step 2 — Agent generates the initial quiz

The agent generates **10 questions**, with 2 questions covering each identified concept.

The student answers all 10 questions.

### Step 3 — Agent evaluates the answers

The agent evaluates the answers concept-wise and records:

| Concept | Correct | Score |
|---|---:|---:|
| Functional Dependencies | 2/2 | 100% |
| 1NF | 2/2 | 100% |
| 2NF | 1/2 | 50% |
| 3NF | 2/2 | 100% |
| BCNF | 2/2 | 100% |
| **Overall** | **9/10** | **90%** |

The overall score is 90%, but the agent does not finish because the student has not achieved 100% in every concept.

### Step 4 — Agent identifies the concept that needs revision

The agent identifies:

**2NF — 50% — Not mastered**

The agent goes back to the student's uploaded material and retrieves the relevant 2NF notes instead of asking the student to reread the entire topic.

**The agent tells the student:** "You have not yet reached 100% in 2NF. Please reread the 2NF material provided from your uploaded notes before attempting the next quiz."

### Step 5 — Student revises the concept

The student rereads the retrieved 2NF material.

**The agent asks:** "Have you finished revising 2NF and are you ready for the follow-up quiz?"

**Student:** "Yes, I'm ready."

The workflow waits for the student's response before continuing.

### Step 6 — Agent generates a targeted quiz

The agent generates **3 new questions specifically about 2NF**.

The student answers all 3 questions.

### Step 7 — Agent evaluates the targeted quiz

The student gets:

**2NF: 3/3 = 100%**

The agent now checks all concepts again:

| Concept | Score | Status |
|---|---:|---|
| Functional Dependencies | 100% | Mastered |
| 1NF | 100% | Mastered |
| 2NF | 100% | Mastered |
| 3NF | 100% | Mastered |
| BCNF | 100% | Mastered |

Since every concept has reached 100%, the mastery condition is satisfied.

### Step 8 — Agent finishes

The agent stores the final revision result:

- **Student:** Ayisha
- **Topic:** DBMS Normalisation
- **Initial overall score:** 90%
- **Concept requiring revision:** 2NF
- **Initial 2NF score:** 50%
- **Targeted revision:** Completed
- **Follow-up 2NF score:** 100%
- **Final mastery:** 100%

## 5. Who is doing the thinking 
| Step | The agent does it | The human does it | What the human loses if the agent does it |
|---|---|---|---|
| **1. Material analysis** | Reads the uploaded study material and identifies the important concepts to be tested. | Provides the topic and study material. | The student loses control over which material is used for preparation. |
| **2. Quiz generation** | Generates questions covering the identified concepts. | Answers the questions based on their understanding. | The student loses the opportunity to actively recall and demonstrate their own understanding. |
| **3. Answer evaluation** | Evaluates the student's answers and calculates scores for each concept. | — | The student would not get an independent assessment of which concepts they understand well. |
| **4. Weak-concept identification** | Compares concept-wise scores with the required 100% mastery level and identifies concepts that are not mastered. | — | The student may overlook weaknesses that are not obvious from their overall score. |
| **5. Targeted material retrieval** | Retrieves the relevant notes/explanation for the concept that is not mastered from the uploaded study material. | Reads and revises the retrieved material. | The student loses the actual revision step needed to improve their understanding. |
| **6. Revision confirmation** | Asks the student whether they have finished revising and are ready for the follow-up quiz. | Decides when they are ready and responds. | The student loses control over when they personally feel ready to be tested. |
| **7. Targeted re-testing** | Generates a new quiz specifically for the concept that was not mastered and evaluates the answers. | Answers the targeted quiz. | The student loses the opportunity to verify whether their revision actually improved their understanding. |
| **8. Next-action decision** | Decides whether all concepts have reached 100% or whether the workflow should go back to revision and retesting. | Continues revising if a concept is still not mastered. | The student may incorrectly assume they are ready without evidence of concept-level understanding. |

**If my agent asks a person something:**
**The question it asks:** “Have you finished revising the weak concept and are you ready for the follow-up quiz?”

**Who answers it:** The student.

**If the student says “Yes”:** The agent generates the targeted quiz.

**If the student says “No”:** The agent keeps the session in the waiting/revision state until the student is ready.

**What happens if nobody answers:** The session remains paused in the waiting state, and the targeted quiz is not generated. The session can resume when the student responds.

**How the output shows that:** The session record shows that the agent is waiting for the student's response, rather than continuing automatically. Once the student responds, the record is updated and the agent either proceeds to the targeted quiz or remains waiting if the student is not ready.

## 6. The state machine
```text
Material Analysis → Initial Quiz → Initial Evaluation
                                      ↓
                              All concepts = 100%?
                                ↙             ↘
                              Yes              No
                              ↓                ↓
                          FINISHED      Targeted Material
                                           Retrieval
                                               ↓
                                    Waiting for Student
                                         Revision
                                               ↓
                                        Targeted Quiz
                                               ↓
                                      Targeted Evaluation
                                               ↓
                                      Concept = 100%?
                                        ↙          ↘
                                      Yes           No
                                       ↓             ↓
                              Check remaining      ↩
                                 concepts       Revision Loop
                                       ↓
                                    FINISHED
```

| State | Active / Waiting / Finished | What moves it on |
|---|---|---|
| **Material Analysis** | Active | Agent identifies the important concepts from the uploaded study material. |
| **Initial Quiz** | Active | Student submits answers to the generated quiz. |
| **Initial Evaluation** | Active | Agent evaluates answers concept-wise and checks the mastery condition. |
| **Targeted Material Retrieval** | Active | Agent retrieves the relevant material for a concept below 100%. |
| **Waiting for Student Revision** | Waiting | Student confirms that they have finished revising and are ready for the targeted quiz. |
| **Targeted Quiz** | Active | Student submits answers to the targeted quiz. |
| **Targeted Evaluation** | Active | Agent evaluates the targeted quiz and decides whether to finish or send the work backward. |
| **Finished** | Finished | All identified concepts have reached 100% mastery. |
| **Stopped** | Finished | The run reaches its revision or spend limit before all concepts reach 100%. |

**What can send work backwards:** The **Targeted Evaluation** state can send the work back to **Targeted Material Retrieval** when the student's score for that concept is below 100%. This creates the revision → re-testing loop.

**What the run decides that the diagram cannot show:**  The agent decides which concepts need revision based on the student's concept-wise quiz scores, retrieves the relevant material for those concepts, decides when a targeted re-test is needed, and decides whether the concept has reached 100% mastery or needs another revision cycle. The agent also decides which concept to handle next when multiple concepts are not mastered.

**Spend limit:** Maximum **30 model calls per run** to prevent excessive API usage and prevent excessive agent execution.

**Revision limit:** Maximum **3 revision → targeted re-test cycles per concept** to prevent the agent from looping indefinitely.

These are separate counters. The spend limit controls the cost of the run, while the revision limit controls how many times the agent can send a concept backward for revision and re-testing.

## 7. The data model
The agent stores the student's revision session as typed records so that progress can be saved and resumed across runs.
### Main records
```python
class Concept(BaseModel):
    name: str
    description: str


class QuizQuestion(BaseModel):
    question: str
    concept: str
    answer: str


class StudentAnswer(BaseModel):
    question: str
    concept: str
    answer: str
    correct: bool


class ConceptResult(BaseModel):
    concept: str
    correct_answers: int
    total_questions: int
    score: float
    mastered: bool


class RevisionSession(BaseModel):
    student_name: str
    topic: str
    material_reference: str
    concepts: list[Concept]
    concept_results: list[ConceptResult]
    current_concept: str | None
    revision_attempts: dict[str, int]
    state: str

```
**Record kinds written to the store:** 
| Kind               | Written by              | When                                                  |
| ------------------ | ----------------------- | ----------------------------------------------------- |
| **session**        | Session manager         | When a new revision session starts                    |
| **quiz**           | Quiz generation step    | When a quiz is generated                              |
| **answer**         | Evaluation step         | When the student submits answers                      |
| **concept_result** | Evaluation step         | After concept-wise evaluation                         |
| **revision**       | Material retrieval step | When material for a non-mastered concept is retrieved |
| **state**          | State manager           | Whenever the session moves to a new state             |

**One check worth doing:** Any record kind that is written more than once in a run is read back as a history, not just as the latest record. This ensures that previous quiz attempts and concept scores are not overwritten.

**Why it helps:** Typed records make the data passed between steps clear and structured. They also allow the agent to preserve the student's progress, quiz history, and concept-wise results so the session can be resumed correctly.

## 8.
