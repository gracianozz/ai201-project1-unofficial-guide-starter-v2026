# The Unofficial Guide

<!-- Gustavo Graciano, Campus Life Corpus -->

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

<!-- Three or four sentences. Which corpus you picked, and the kinds of
     questions your system answers. Write it for someone who has never seen
     this repo.


     Milestone 5. -->


-> This program answers questions based on the campus life corpus. The questions that my system answers are ranged from classes,housing, parking, and resources available. Documents regarding campus life are searched from using an algorithm with chunking to answer the question with the most relevancy.

## Chunking Strategy

**Chunk size:**
Every paragraph is made into a chunk. Each document is somewhat short and is split up into different sections.

**Overlap:**
Overlap is not used, since no sentence is cut off.

<!-- What about YOUR documents made you pick these numbers? Short posts and
     long sectioned guides don't want the same chunking, and "800 seemed
     reasonable" earns nothing. Point at something you noticed when you read
     the documents in Milestone 1.

     If you changed your mind partway through, say so and say why. That's worth
     more than pretending you got it right first time.

     Milestone 3. -->

-> For the chunk size, I chose for every paragraph to be converted into a chunk. At first, I chose for every post in every document to be a chunk on its own, but later on I found that each chunk(which is a whole document), may contain too many topics for it to be a whole chunk. When asking Claude what questions it can generate from the chunks with them being the whole document, it gave me multiple questions, which made me realize that the chunk was too big. 
     Having every paragraph be a chunk makes it so each chunk has at most 1 topic to cover, and helps with identifying information regarding questions faster.

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 1** — source: `admin_add_drop_deadline.txt#0` — produced by: `chunker.py::split_documents`

```
On the add/drop deadline

You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.
```

**Chunk 2** — source: `course_cs_340_exams.txt#1` — produced by: `chunker.py::split_documents`

```
CS 340 Databases — assessment

Start the term project in week three, not week eight; everyone learns this the hard way.

```

**Chunk 3** — source: `course_phys_130_workload.txt#0` — produced by: `chunker.py::split_documents`

```
Workload for PHYS 130 Mechanics

People keep asking so: 7 hours a week, plus 3 on lab weeks. That's real time, not optimistic time.
```

**Chunk 4** — source: `dining_verrill_street_grill_followup.txt#1` — produced by: `chunker.py::split_documents`

```
Re: Verrill Street Grill

Also worth saying: one register, so the queue is a single line no matter how busy. Nobody tells you this at orientation.

```

**Chunk 5** — source: ` housing_morrow_house.txt#1` — produced by: `chunker.py::split_documents`

```
Morrow House — what it's actually like

The good: cheapest housing tier by about $900 a year, and the singles are real singles.

```

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:**
"How many hours a week is the workload for PHYS 130 Mechanics?"

**Answer:**

```
"The workload for PHYS 130 Mechanics is 7 hours a week, plus an additional 3 hours on lab weeks [according to course_phys_130_workload.txt and course_phys_130.txt].

Sources retrieved: course_phys_130.txt, course_phys_130_workload.txt, course_stat_150_workload.txt"
```

**My relevance cutoff:**

The relevance cutoff I chose is .50. I chose this because of how the both groups distance resulted. For the questions relevant to the documents, the distance was ranged from .102 ->.360. For the out of scope questions, the distance was ranged from .787 -> .923. I chose the cutoff .50 so the effect is slightly more strict, but enough to the point that relevant or similar questions can still pass through.

<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. -->

| Question | In corpus? | Best distance |
|---|---|---|
| How much does laundry cost in Old Brewhouse? | yes | 0.144 |
| When are the walk in hours for the health center? | yes | 0.158|
| What is the window for dropping a class without a W on my transcript? | yes | 0.360 |
| How often does the campus shuttle run on weekdays? | yes | 0.182 |
| How many hours a week is the workload for PHYS 130 Mechanics? | yes | 0.102 |
| What is the capital of Mongolia? | no | 0.787 |
| How do I change the oil in a diesel engine? | no | 0.923 |
| Who won the 1994 World Cup? | no | 0.847 |
| What is the recommended dosage of ibuprofen for a headache? | no | 0.849 |
| How do I write a for loop in Rust? | no | 0.860 |


## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**1.**
When thinking I had my chunk size correct, I asked AI to make up possible questions that can be asked from those chunks. Claude returned multiple questions, which I then came to realize that my chunk size might be too big, since the questions were ranged differently accross different topics. I then asked Claude what best approach could I take from the current chunk size idea I had. I then came to choose chunking per paragraph. This way, the chunks are limited to at most 1 topic each, and can hold specific topics and information which makes it easier to find.

**2.**
I used AI to come up with how to actually set the algorithm for the proper chunking idea I had in mind. At first, without surprise, Claude automatically gave me code which told me was the "answer" to my question. But before actually just accepting, I asked what each line does and asked questions that could make the code better for the use. This way, I understand better on how the code works for chunking.

<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 3/5 | 3/5 | 3/5 | MISSED |
| 2. Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 4. All 5 of the sampled chunks will be paragraphs of the documents used | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 5. For all 5 questions, the answer the model gives contains the expects phrase. | 5 of 5 | 2/5 | 2/5 | 2/5 | MISSED |



<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->


### Which dining hall has the longest wait at lunchtime? — run 1

- Best distance: 0.2922 (passed the gate)
- Sources retrieved: dining_halden_hall_followup.txt, dining_pellew_dining_hall.txt, dining_pellew_dining_hall_followup.txt, dining_the_ridgeway_cafe_followup.txt

```
Based on the provided documents, Pellew Dining Hall has the longest wait at peak lunchtime, with wait times of 12 to 18 minutes [according to dining_pellew_dining_hall.txt]. In comparison, Halden Hall has a wait of rarely more than 8 minutes [according to dining_halden_hall_followup.txt], and The Ridgeway Café has a wait of 10 to 15 minutes at 12:30 [according to dining_the_ridgeway_cafe_followup.txt].
```

### Which dining hall has the longest wait at lunchtime? — run 2

- Best distance: 0.2922 (passed the gate)
- Sources retrieved: dining_halden_hall_followup.txt, dining_pellew_dining_hall.txt, dining_pellew_dining_hall_followup.txt, dining_the_ridgeway_cafe_followup.txt

```
Based on the provided documents, Pellew Dining Hall has a peak wait time of 12 to 18 minutes [dining_pellew_dining_hall.txt]. Halden Hall has a wait time of rarely more than 8 minutes [dining_halden_hall_followup.txt]. (The Ridgeway Café is also mentioned with a wait of 10 to 15 minutes, but it is referred to as a café rather than a dining hall) [dining_the_ridgeway_cafe_followup.txt]. Therefore, Pellew Dining Hall has the longest wait [dining_pellew_dining_hall.txt].
```

### Which dining hall has the longest wait at lunchtime? — run 3

- Best distance: 0.2922 (passed the gate)
- Sources retrieved: dining_halden_hall_followup.txt, dining_pellew_dining_hall.txt, dining_pellew_dining_hall_followup.txt, dining_the_ridgeway_cafe_followup.txt

```
Based on the provided documents, Pellew Dining Hall has a peak wait time of 12 to 18 minutes [dining_pellew_dining_hall.txt]. Halden Hall has a wait time of rarely more than 8 minutes [dining_halden_hall_followup.txt]. (The Ridgeway Café is also mentioned with a 10 to 15 minute wait, but it is referred to as a café rather than a dining hall) [dining_the_ridgeway_cafe_followup.txt]. Therefore, Pellew Dining Hall has the longest wait [dining_pellew_dining_hall.txt].
```

### When are the walk in hours for the health center? — run 1

- Best distance: 0.1575 (passed the gate)
- Sources retrieved: dining_the_atrium.txt, health_center.txt, transit_walking.txt

```
The walk-in hours for the health centre are from 8:00 am to 11:00 am [according to health_center.txt].
```

### When are the walk in hours for the health center? — run 2

- Best distance: 0.1575 (passed the gate)
- Sources retrieved: dining_the_atrium.txt, health_center.txt, transit_walking.txt

```
The walk-in hours for the health centre are from 8am to 11am [According to health_center.txt].
```

### When are the walk in hours for the health center? — run 3

- Best distance: 0.1575 (passed the gate)
- Sources retrieved: dining_the_atrium.txt, health_center.txt, transit_walking.txt

```
The walk-in hours for the health centre are from 8am to 11am [according to health_center.txt].
```

### What is the window for dropping a class without a penalty of W on my transcript? — run 1

- Best distance: 0.3600 (passed the gate)
- Sources retrieved: admin_add_drop_deadline.txt, admin_grade_appeals.txt, admin_transcript_requests.txt, admin_withdrawal_deadline.txt

```
You can add or drop a course through the end of the second week without a W appearing on your transcript, as a drop after week two shows as a W [admin_add_drop_deadline.txt].
```

### What is the window for dropping a class without a penalty of W on my transcript? — run 2

- Best distance: 0.3600 (passed the gate)
- Sources retrieved: admin_add_drop_deadline.txt, admin_grade_appeals.txt, admin_transcript_requests.txt, admin_withdrawal_deadline.txt

```
You can drop a class through the end of the second week without a "W" appearing on your transcript, as a drop after week two results in a "W" [admin_add_drop_deadline.txt].
```

### What is the window for dropping a class without a penalty of W on my transcript? — run 3

- Best distance: 0.3600 (passed the gate)
- Sources retrieved: admin_add_drop_deadline.txt, admin_grade_appeals.txt, admin_transcript_requests.txt, admin_withdrawal_deadline.txt

```
[According to admin_add_drop_deadline.txt], dropping a course can be done through the end of week six, but any drop after week two will show as a W on your transcript. Therefore, the window to drop a class without a W on your transcript is through the end of the second week [admin_add_drop_deadline.txt].
```

### How many dorms let you pay for laundry with coins? — run 1

- Best distance: 0.4317 (passed the gate)
- Sources retrieved: housing_aldridge_hall.txt, housing_morrow_house_laundry.txt, housing_old_brewhouse.txt, housing_old_brewhouse_laundry.txt

```
Based on the provided documents, Old Brewhouse requires coins for laundry [housing_old_brewhouse.txt, housing_old_brewhouse_laundry.txt]. Morrow House accepts coins or cards [housing_morrow_house_laundry.txt].
```

### How many dorms let you pay for laundry with coins? — run 2

- Best distance: 0.4317 (passed the gate)
- Sources retrieved: housing_aldridge_hall.txt, housing_morrow_house_laundry.txt, housing_old_brewhouse.txt, housing_old_brewhouse_laundry.txt

```
Based on the provided documents, there are two dorms—Old Brewhouse and Morrow House—that accept coins for laundry [according to housing_old_brewhouse.txt, housing_old_brewhouse_laundry.txt, and housing_morrow_house_laundry.txt].
```

### How many dorms let you pay for laundry with coins? — run 3

- Best distance: 0.4317 (passed the gate)
- Sources retrieved: housing_aldridge_hall.txt, housing_morrow_house_laundry.txt, housing_old_brewhouse.txt, housing_old_brewhouse_laundry.txt

```
Based on the provided documents, Old Brewhouse requires coins for laundry (costing $1.50 for a wash and $1.50 for a dry) [housing_old_brewhouse.txt, housing_old_brewhouse_laundry.txt]. Morrow House also takes coins (along with cards) for laundry [housing_morrow_house_laundry.txt]. This means two dorms (Old Brewhouse and Morrow House) let you pay with coins [housing_old_brewhouse.txt, housing_old_brewhouse_laundry.txt, housing_morrow_house_laundry.txt].
```

### Which dorms use app-based laundry? — run 1

- Best distance: 0.4797 (passed the gate)
- Sources retrieved: housing_aldridge_hall_laundry.txt, housing_innisfree_hall_laundry.txt, housing_old_brewhouse.txt, housing_old_brewhouse_laundry.txt

```
I do not have enough information to answer the question about which dorms use app-based laundry.
```

### Which dorms use app-based laundry? — run 2

- Best distance: 0.4797 (passed the gate)
- Sources retrieved: housing_aldridge_hall_laundry.txt, housing_innisfree_hall_laundry.txt, housing_old_brewhouse.txt, housing_old_brewhouse_laundry.txt

```
I do not have enough information to answer the question, as the provided documents do not mention which dorms use app-based laundry.
```

### Which dorms use app-based laundry? — run 3

- Best distance: 0.4797 (passed the gate)
- Sources retrieved: housing_aldridge_hall_laundry.txt, housing_innisfree_hall_laundry.txt, housing_old_brewhouse.txt, housing_old_brewhouse_laundry.txt

```
I do not have enough information to answer the question about which dorms use app-based laundry.
```

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided | 
|---|---|---|---|
| 1 | Retrieved chunk contains the answer | MET | Using the sources that were retrieved and displayed, I checked whether the file holds the answer that was in it. Each of the five questions accross all 3 runs contained the right file. |
| 2 | Every answer names a source | MET | In each of the answers, it has a 'Sources Retrieved' and a 'According to' section that displays the different sources used to display the answer.   |
| 3 | Gate stops out-of-corpus questions  | MET | By reading the Out-of-Scope questions in the results file and ensuring their distance does not pass the relevance cutoff and is shown as "refused", I was able to confirm that the gate works properly.
| 4 | All of the 5 sampled chunks will be paragraphs of each of the documents used. Each paragraph will be made into one chunk. | MET | Using the command "python app.py chunks" it helped with checking if the chunking method I implemented worked, and all were shown as full paragraphs with no cutoffs. |
| 5 | For all 5 questions, the answer the model gives contains the expects phrase. | MISSED | Checking each answer for each run, only 2 of the 5 questions in each run had the "expects" phrase in their answers.  |


## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->
At first, nothing was missed, this was due to how straightforward the questions were. Although it may say that there was one fail, the only reason it did fail was because the wording of the "expects" was off. When fixing that, all passed.

1. Question 1 says, "Which dining hall has the longest wait at lunchtime?". This question failed at retrieval. In order for this question to be answered, it has to compare all of the dining halls, which is more than what the top-k is(top-k being 4). Kestrel Commons, which is the right answer of 20-25 minutes, was not a chunk that was retrieved. The model used the available sources and answered based off those, but it left out the actual correct one.

2.  Question 3 says, "Which dorms use app-based laundry?". This question also failed at retrieval. Since the chunker splits every paragraph into a chunk and have the same title as to keep the relevance, they can be seen as pretty much equals in relevancy. This made it so other chunks take up the top-k slots, leaving out multiple chunks that contain the right answer.

3. Question 4 says, "How many dorms let you pay for laundry with coins?". This question failed at generation. It obtained the correct documents and sources to be able to format the answer, but in the first run it never actually considered them as both being the overall correct answer. This made it so the answer did not include the "expects" word.



## The Improvement

**What I changed:**
I added an extra rule for the grounding prompt in generate.py


**Why I picked it:**
This was a miss that could have been avoided,

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
