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

## 8. Step-by-step contracts
### 1. Material Analysis — START → Initial Quiz
- **What:** Reads the uploaded study material and finds the important concepts that should be tested.
- **Why this way:** The quiz should be based on the student's own study material.
- **Reads / writes:** Reads the uploaded material and saves the identified concepts in the session record.
- **Done when:** The concepts to be tested are identified and stored.

### 2. Initial Quiz — Initial Quiz → Initial Evaluation
- **What:** Creates a quiz covering all the identified concepts.
- **Why this way:** The quiz should check the student's understanding of the whole topic.
- **Reads / writes:** Reads the identified concepts and study material; saves the generated quiz.
- **Done when:** The quiz is generated and given to the student.

### 3. Initial Evaluation — Initial Evaluation → Targeted Material Retrieval / Finished
- **What:** Checks the student's answers and gives a separate score for each concept.
- **Why this way:** A good overall score can still hide a weak concept.
- **Reads / writes:** Reads the quiz and student's answers; saves the concept-wise scores.
- **Done when:** All identified concepts have been evaluated. If every concept is at 100%, the session finishes. Otherwise, a concept below 100% is selected for revision.

### 4. Targeted Material Retrieval — Targeted Material Retrieval → Waiting for Student Revision
- **What:** Finds the relevant notes for the concept that is below 100% from the student's uploaded material.
- **Why this way:** The student only needs to revise the concept they are struggling with instead of reading the whole topic again.
- **Reads / writes:** Reads the uploaded material and selected concept; saves the relevant revision material.
- **Done when:** The relevant material is retrieved and shown to the student.

### 5. Waiting for Student Revision — Waiting → Targeted Quiz
- **What:** Waits for the student to confirm that they have finished revising and are ready for the next quiz.
- **Why this way:** The student decides when they are ready to be tested.
- **Reads / writes:** Reads the student's response and updates the session state.
- **Done when:** The student says they are ready. If there is no response, the session stays paused.

### 6. Targeted Quiz — Targeted Quiz → Targeted Evaluation
- **What:** Creates a new quiz focused only on the concept that was below 100%.
- **Why this way:** This checks whether the targeted revision helped the student.
- **Reads / writes:** Reads the selected concept and retrieved revision material; saves the targeted quiz and answers.
- **Done when:** The student submits the targeted quiz.

### 7. Targeted Evaluation — Targeted Evaluation → Finished / Targeted Material Retrieval

- **What:** Checks the targeted quiz and sees whether the concept has reached 100%.
- **Why this way:** The agent should verify improvement instead of assuming that revision worked.
- **Reads / writes:** Reads the targeted quiz and student's answers; saves the new score and revision attempt count.
- **Done when:** If the concept reaches 100%, the agent checks the remaining concepts. If it is still below 100%, it goes back to Targeted Material Retrieval.

### 8. Finish Check — Evaluation → Finished
- **What:** Checks whether all identified concepts have reached 100%.
- **Why this way:** The session should finish only when every concept has reached the required level.
- **Reads / writes:** Reads the stored concept scores and saves the final session status.
- **Done when:** Every identified concept has reached 100%.

### Rules enforced in code
The 100% mastery condition, concept-wise scoring, backward revision loop, state changes, revision limit, and spend limit will be checked in the application code, not only in the AI prompt. The code decides whether the agent finishes or sends a concept back for revision and re-testing.

### Where the documents come in
- **What documents it reads:** The student's uploaded study material for the topic.
- **What each document lets it prove:** The material is used to identify concepts, create quiz content, and find notes for concepts that need revision.
- **What it does when the evidence is not there:** If the required information is not present in the uploaded material, the agent says that the information could not be found instead of filling the gap from general knowledge.
- **How a citation gets checked:** If the agent says that something came from the uploaded material, it must be present in that material.

### Where the human comes in
- **The question it asks:** "Have you finished revising the weak concept and are you ready for the follow-up quiz?"
- **Who answers:** The student.
- **What record the answer becomes:** The student's response is saved in the session record.
- **How that record reaches the decision:** If the student says "Yes", the agent moves to the targeted quiz. If the student is not ready, it stays in the waiting state.
- **What happens if nobody answers:** The session stays paused and the targeted quiz is not generated.
- **How the output shows that:** The session record shows that the agent is waiting for the student's response.

## 9. The second encounter
The student comes back later to check their preparation for the same topic again.

The agent reads the previous session and remembers that the student initially scored 50% in 2NF, revised it, and later reached 100%. It shows this previous result instead of treating the student as a completely new user.

The agent also remembers the concept-wise history and can use it when starting the new revision check. For example, it knows that 2NF was previously the student's weak concept and can pay extra attention to it in the new quiz.

A fresh conversation would not know that the student had previously struggled with 2NF or that they had improved to 100%. The stored history is what allows the agent to continue from the student's previous progress.

## 10. Files and responsibilities
| File | Owns | Done when |
|---|---|---|
| `main.py` | Starts the revision session and connects the steps. | The complete revision flow can be started. |
| `flow.py` | Controls the order of states and the backward revision loop. | The agent can move forward and go back when a concept is below 100%. |
| `steps.py` | Contains the main steps such as material analysis, quiz generation, evaluation, material retrieval, and re-testing. | Each step works with the required input and produces the expected output. |
| `store.py` | Saves and loads the student's session, scores, revision attempts, and state. | A session can be saved and continued later. |
| `prompts/` | Contains the prompts used for concept identification, quiz generation, evaluation, and material retrieval. | Each model call has a clear prompt for its specific task. |
| `models.py` | Defines the structured records used by the different steps. | The data passed between steps follows the expected structure. |

### Helpers that carry real logic
**Which of them are model calls:**  
Concept identification, quiz generation, answer evaluation, and targeted material retrieval use model calls.

**Which constants are architecture:**  
State names, state transitions, stored record structure, spend limit, and revision limit are part of the system architecture.

**Which are our domain decisions:**  
The 100% mastery requirement, concept-wise evaluation, and the decision to send a concept back for targeted revision are specific to our EDU-PULSE agent.

## 11. What this deliberately does not do
1. **It does not create a full study timetable or daily schedule.**  
   We considered adding planning and scheduling, but our main goal for this agent is to check whether the student actually understands a particular topic and help them improve weak concepts.

2. **It does not handle multiple subjects or topics in one session.**  
   We considered supporting multiple subjects, but we are keeping the agent focused on one topic so that the revision → quiz → evaluation loop can be properly built and tested within the two-day hackathon.

3. **It does not use web search or outside study resources.**  
   The agent uses the student's uploaded material for the quiz and targeted revision. This keeps the source of the learning material clear and keeps the scope manageable for the hackathon.

4. **It does not send parent/guardian alerts.**  
   We considered this as part of the larger EDU-PULSE idea, but it is outside the scope of this agent. We are focusing on proving the core learning and backward revision loop first.

5. **It does not build the complete mobile app as part of this agent.**  
   The mobile app is part of the larger EDU-PULSE idea, but for this two-day agent slice we are focusing on building and testing the agent workflow first.

## 12. Build order
| phase | what lands | hours |
|---|---|---:|
| **1** | Basic revision flow: material analysis, concept identification, initial quiz, concept-wise evaluation, and the 100% mastery check using sample/test data. | **5** |
| | *cut line: we can show the quiz → evaluation → identify not-mastered concept → targeted revision → retesting flow, even without the real AI model.* | |
| **2** | Add the real AI model for quiz generation, answer evaluation, concept identification, and retrieval of relevant material from the uploaded study material. | **6** |
| | *cut line: a real topic and study material produce a real quiz, concept-wise result, and targeted revision material.* | |
| **3** | Add saved session state, student revision confirmation/waiting state, targeted re-quiz, and the revision → retesting loop until the required mastery level is reached. | **7** |
| | *cut line: the complete agent works end to end, including the backward loop and continuing after the student's response.* | |
| **4** | Test with students, fix issues, and make the demo flow clear and reliable. | **4** |
| | *cut line: we have a stable working demo that can be shown from start to finish.* | |

The planned active build time is **22 hours**. The remaining hackathon time is available for breaks, discussions, debugging, testing, and unexpected issues.

### How we will build
We will first make the complete workflow work end to end using sample/test data before connecting the real AI model. Once the workflow is working, we will add the real model calls and saved session state. We will refine the prompts while testing the actual outputs rather than spending the early build time only on prompts.

We will also save useful model responses during testing so that we can replay them when needed.

### Where the hours will actually go
We expect most of the time to go into testing the model outputs, checking concept-wise evaluation and targeted material retrieval, and making sure the revision → retesting loop works correctly.

## 13. The demo
1. **Student starts a revision session**
   - The student selects a topic and uploads the study material.
   - The agent identifies the important concepts and creates the initial quiz.

2. **Student takes the quiz**
   - The student answers the questions.
   - The agent evaluates the answers concept-wise and shows which concept is below 100%.

3. **Agent finds the concept that needs revision**
   - The agent retrieves the relevant part of the uploaded material for the concept that is below 100%.
   - The student revises only that material.

4. **Student confirms readiness**
   - The agent asks whether the student is ready for the targeted quiz.
   - The student responds and the workflow continues.

5. **Targeted re-test**
   - The agent generates a new quiz for the concept that was below 100%.
   - The student answers it and the agent evaluates the result.

6. **Backward loop**
   - If the concept is still below 100%, the agent sends it back for revision and re-testing.
   - If it reaches 100%, the agent checks the remaining concepts.

7. **Final result**
   - When all identified concepts reach 100%, the agent finishes and shows the student's final result and revision history.

### Which beat is the main argument
The main beat is the **backward loop**: the agent finds a concept the student has not mastered, retrieves the relevant material, waits for the student to revise, and sends the concept for another targeted quiz instead of simply giving an overall score.

### What is live and what is recorded
The main revision flow will be shown live. If a model response takes too long or is unreliable during the demo, we will use a previously saved model response for that part and clearly indicate that it is recorded.

### If the model gives an unexpected result
If the model gives an incorrect or unexpected response, we will not silently accept it. The application will check the required structure and mastery condition, and we will show the result only when it passes the required checks.

**Why it helps:** Each file has a clear responsibility, so different team members can work on different parts without changing the whole workflow.

## 14. How this grows
Our current agent is focused on checking one topic at a time. The same structure can be extended later without changing the main revision loop.

1. **Multiple subjects and topics**  
   The current workflow can be extended to handle multiple topics and subjects. This would mainly require adding subject/topic information to the stored session records and allowing the student to choose between them.

2. **Study planning and scheduling**  
   A planning agent could be added later to decide when the student should revise each topic. The current revision agent can remain unchanged and receive a topic when it is time to study.

3. **Parent/guardian accountability**  
   Parent or guardian notifications could be added later when a student repeatedly skips or does not complete a revision session. This would need a new notification component and additional student/guardian information.

4. **More learning resources**  
   The agent could later support additional trusted study resources. This would require changes to the material retrieval part so that it can work with different sources.

5. **Learning history and long-term analysis**  
   The stored concept-wise results can later be used to identify long-term strengths and weaknesses across different topics and revision sessions.

## 15. What you are least sure about

1. **Whether the agent can identify the important concepts correctly from different study materials.**  
   We need to test whether the concepts selected by the agent are actually relevant and whether it misses any important concept.

2. **Whether the agent can evaluate student answers correctly at the concept level.**  
   We need to test whether the agent can correctly decide if an answer shows understanding of the concept, especially for answers written in different ways.

3. **Whether the targeted material retrieval gives the right explanation for the concept that needs revision.**  
   We need to test whether the agent retrieves the relevant part of the uploaded material instead of unrelated content.

## 16. Claims to verify
| Claim | How to check | Checked? |
|---|---|---|
| The model can identify the important concepts from the uploaded study material. | Test it with the DBMS Normalisation material and compare the identified concepts with the material. | Not yet |
| The model can generate questions that match the identified concepts. | Check whether the generated questions actually test the intended concepts. | Not yet |
| The model can evaluate student answers correctly at the concept level. | Give it sample answers with known correct/incorrect results and compare its evaluation. | Not yet |
| The agent can retrieve the correct material for a concept below 100%. | Give it a known weak concept and check whether it retrieves the relevant part of the uploaded material. | Not yet |
| The saved session can be loaded when the student returns. | Complete a session, save it, start again, and check whether the previous results are loaded correctly. | Not yet |      

## Before you call it done
### The check that the pipeline works
Run the complete flow from start to finish:

**Upload material → identify concepts → generate quiz → evaluate → retrieve weak-concept material → student revision → targeted quiz → re-evaluate → finish.**

Check that the session reaches the correct final state and that the stored scores and revision history are updated correctly.

### The adversarial check
Check what happens if the uploaded study material contains instructions such as "ignore the task" or other text that tries to change what the agent should do.

The agent should treat the uploaded material as **study data, not as instructions**. It should continue following the defined workflow and should not let the uploaded content change the agent's rules or state transitions.



