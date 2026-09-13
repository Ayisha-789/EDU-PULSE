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
The agent keeps the student's progress and quiz results, decides which subtopic needs attention based on the student's answers, and chooses whether to finish or send the work back for revision and another targeted quiz. The student is part of the loop by answering the quizzes, and the workflow can pause for the student's response and resume later. The important difference from a normal AI quiz is that the agent does not simply generate questions and give a score—it evaluates the result, decides the next action, and can move backwards until the student's weak areas are improved.
