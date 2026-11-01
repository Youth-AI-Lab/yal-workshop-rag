# Workshop 2 - Everything in the context, then RAG

### Youth AI Lab (Erasmus+) - series "Build your own chatbot", workshop 2 of 6

- **Project:** Youth AI Lab (Erasmus+), with five partners: L.A.B. (Aix-en-Provence, France),
  UAB (Barcelona, Spain), Perlatecnica (Naples, Italy), Digitale Wolven (Antwerp, Belgium),
  CSC Vent des Îles (La Rochelle, France).
- **The series:** [the six workshops](https://github.com/Youth-AI-Lab/yal-workshop-kit#the-series)
- **Need help?**
  - Raise your hand and ask the facilitator.
  - If something breaks, don't panic: your files stay in the Codespace.

> 🎓 **Open your Codespace** (one per pair): 👉 **https://codespaces.new/Youth-AI-Lab/yal-workshop-rag**
>
> **Before you click**, if the idle timeout of this GitHub account is not set yet: do
> [step 1 of SETUP.md](SETUP.md#step-1---let-the-codespace-wait-for-you) (1 minute).
>
> This link creates your own copy of this repository, in VS Code running in your browser. Nothing
> to install. The detailed steps are in [Part 1](#part-1---welcome-20-min).

> 📚 **The slides of the facilitator:** https://youth-ai-lab.github.io/yal-workshop/2/ (the same
> words as this page). **The short version** of this page, on one page: [sheet.md](sheet.md). The
> setup, the commands and the common problems of the whole series: [SETUP.md](SETUP.md).

### Contents

- [Goals of the session](#goals-of-the-session)
- [Part 1 - Welcome (20 min)](#part-1---welcome-20-min)
- [Part 2 - Everything in the context (★, 15 min)](#part-2---everything-in-the-context--15-min)
- [Part 3 - Unplugged: be the search engine (★, 15 min)](#part-3---unplugged-be-the-search-engine--15-min)
- [Part 4 - Pieces and embeddings (★★, 20 min)](#part-4---pieces-and-embeddings--20-min)
- [Part 5 - Change the settings (★★★, 20 min)](#part-5---change-the-settings--20-min)
- [Part 6 - RAG against everything in the context (★★, 10 min)](#part-6---rag-against-everything-in-the-context--10-min)
- [Part 7 - Closing (10 min)](#part-7---closing-10-min)
- [Troubleshooting](#troubleshooting)

---

## Goals of the session

### What you will be able to do by the end of this session

In workshop 1, your chatbot got instructions, and it said "I don't know" to the precise
questions: it had no documents. Today it gets all the knowledge of the kit (the files of the
series, copied into the repository of each workshop): 17 summaries and 20 official documents. The
whole series answers one question: *what enters the model's context,
when, and who decides?* The question of the day is:

> **Who picks the pieces?**

First, you put everything in the context and see what it costs. Then a search engine picks a few
pieces for each question (it searches inside the documents, not on the web), and you look at the
pieces it picks. This is called **RAG** (*Retrieval-Augmented Generation*).

| Bloom level | Parts | You will be able to... | Mode |
|---|---|---|---|
| **Understand** | 2 | Explain why putting all the knowledge in the context works on a small kit, and why it does not grow: every message pays for everything. | `B` |
| **Apply** | 3-4 | Read what a RAG gives the model for a question: its pieces (chunks), how many (top-k), and how they are found (embeddings). | `query` |
| **Analyse** | 5-6 | Show, on a question, how the size of the pieces and their number change what the model can see, and compare a RAG with "everything in the context" on cost and answers. | `query`, `RAG` |
| **Evaluate** | 7 | Say when a RAG is a good choice, and what failure it hides: it always gives something. | - |

All session long, you go on testing your chatbot with the same questions: today, columns
B and RAG of your score sheet.

### Why this approach?

The kit is small on purpose. All its knowledge fits in the context, so you can see the first
solution work, and pay for it. Then you imagine ten times more documents, and that solution stops.

Before you use a search engine on a computer, you are the search engine, with paper strips.
You will see that picking a few pieces for a question is a choice, and that a good choice is not
always possible: a fact can be cut in two, and a question with no answer still gets pieces.

The RAG runs in Open WebUI, the chat tool of the closing of workshop 1. It shows the pieces
it gave the model under each answer, so you can check what the model read.

### How this connects to WikiYouthBot

In the WikiYouthBot activity, the *Knowledge* box of the chatbot holds the documents of the group.
What the tool does with them, you cannot see from the outside. This workshop shows the two things
it can do: read everything, or search for pieces. Some chat tools switch from one to the other on
their own when the knowledge grows (see [Part 7](#part-7---closing-10-min)). You can build a
chatbot with a knowledge base for a group today with Open WebUI: see the
[Open WebUI guide](https://github.com/Youth-AI-Lab/yal-openwebui-guide).

The series goes on, one piece of the chatbot at a time:

- **Workshop 1**: the instructions, and how to test a chatbot
- **Workshop 2** (this one): all the knowledge in the context, then a RAG: who picks the pieces?
- **Workshop 3**: the model searches by itself, and skills to add a document you checked
- **Workshop 4**: tools that act outside, such as today's fire danger level
- **Workshop 5**: organise what it knows in a wiki, and pack the chatbot of your territory
- **Workshop 6**: fine-tune a small model, to sort messages before the chatbot

### Before you start

You need the same as in workshop 1: no programming, a little English, two people per screen.
**Bring `my-work.zip`**, the file you saved at the end of workshop 1. Without it, the kit's example
(Feurisson) becomes your system prompt, and you start column B from there. More in
[SETUP.md, Before you start](SETUP.md#before-you-start).

### Reference documents

All of these are in your Codespace, in the file list on the left:

- `summaries/index.md` and `corpus/index.md`: the list of the 17 summaries and of the 20 official
  documents. A readable copy of each document is in `corpus/text/`.
- `test-questions.md` and `scores.md`: the test set and your score sheet, as in workshop 1.
- `AGENTS.md`: your system prompt (from your save, or Feurisson).
- `SETUP.md`: setup, commands and common problems.

---

## Part 1 - Welcome (20 min)

**Goal**: open the Codespace of this workshop, bring back your work, and let Open WebUI prepare
its two knowledge bases (the documents, cut into pieces and ready for a search) in the background
while you work.

### Step 1 - Open your Codespace and save your key

Follow [SETUP.md](SETUP.md#setup), steps 1 to 5, with the link at the top of this page: let the
Codespace wait for you, open it, save your key with `workshop-login`, check `Key OK`, have a first
conversation with `workshop bare`, and open a second terminal.

> 💡 **If you use OpenCode.** Same commands, after `workshop-login --engine opencode`. The judge of
> `score` and Open WebUI need an Anthropic key (`sk-ant-`). The
> [OpenCode guide, Part 4](https://github.com/Youth-AI-Lab/yal-opencode-guide#part-4---the-knowledge)
> shows the other way to give knowledge to a chatbot, by search, which is workshop 3.

> ℹ️ **No Codespace?** The same repository opens on your own computer, with Docker and VS Code: see
> the [dev containers guide](https://github.com/Youth-AI-Lab/yal-devcontainer-guide).

### Step 2 - Bring back your work, and start Open WebUI

1. **Drag `my-work.zip`** from your computer into the file list of the Codespace. If you
   downloaded it more than once, your browser may have named the newest one `my-work (1).zip`:
   drag that one, and type its exact name between quotes, for example
   `workshop-start 2 --from "my-work (1).zip"`.
2. In your first terminal, type:

   ```bash
   workshop-start 2 --from my-work.zip
   ```

   Without a save, type `workshop-start 2`. You should see your files restored and, at the end:

   ```
   Ready for workshop 2.
   Open WebUI is starting in the background, then a second knowledge base (about 4 to 5 minutes
   the first time, 1 minute after). You can start the workshop meanwhile.
     To follow it: tail -f .workshop/openwebui-start.log   (Ctrl+C stops following, not Open WebUI)
     It is ready when the last line says READY.
   Today's page: README.md (Ctrl+Shift+V to read it as a page)
   First command: workshop B
   ```

   Check the date in the line `Restored from … (saved on …)`: it should be the end of workshop 1.

`workshop-start 2` has started two things that take a few minutes: Open WebUI itself (the first
time, a download of about 1.6 GB), then the cutting of the kit's documents into pieces of two
sizes. In the Codespaces we measured, it was ready in about 4 minutes. You do not need to wait:
Parts 2 and 3 do not use Open WebUI.

3. **To see where it is**, type in your second terminal:

   ```bash
   tail -f .workshop/openwebui-start.log
   ```

   The last line is `READY: Open WebUI is ready, with the two sizes.` when it is done. Press
   **Ctrl+C** to stop following: Open WebUI keeps running.

> 💡 **Tip.** Row 12 of `test-questions.md` still empty? Follow its section **Question 12: your
> territory** now: write the question, and the expected answer with its source. Then type
> `replay bare 12` and `replay A 12`, and score them with `score bare 12` and `score A 12`.

> 🚫 **Warning.** Open WebUI is reached through **port 3000** of your Codespace: a numbered door,
> listed in the **Ports** tab next to the terminal. It is private: only you can open it. **Never
> make port 3000 public** (Ports tab, right-click on 3000, Port Visibility). This Open WebUI has no
> accounts: anyone with the link could use your key.

> 💡 **Tip.** **Checkpoint**: `Key OK`, `Ready for workshop 2`, and the log of Open WebUI (the file
> where it notes what it is doing) growing in the second terminal.

---

## Part 2 - Everything in the context (★, 15 min)

**Goal**: give the chatbot all the knowledge of the kit at once, see how full the context is, then
replay and score column B.

### What you will discover

- **Mode `B`**: your system prompt, plus all the summaries and all the readable copies of
  the documents, read at every message.
- **The size of the knowledge**: about half of the context window, sent with your first question
  (the gauge shows it after that message).
  The context is everything the model reads before it answers, and the context window is its
  maximum size: here, 200,000 **tokens** ([a token](https://github.com/Youth-AI-Lab/yal-local-ai-guide/blob/main/how-an-llm-works.md#what-a-token-really-is) is a piece of a word).
- **The cost of reading everything**: every message pays for all of it, again.

### What the model reads in mode B

```mermaid
flowchart LR
  T["General instructions of the tool"] --> M["Model"]
  S["AGENTS.md"] --> M
  K["All 17 summaries + all 20 documents (about 100,000 tokens)"] --> M
  Q["Your question"] --> M
  M --> R["Answer"]
```

**Key insight:** in mode B, nobody picks. Everything enters the context, every time. The
model can find any fact, and see a contradiction between two documents, because it has both. The
price is paid at every message.

**Why does every message pay?** You pay a model by the token, for what it reads and for what it
writes. In mode B, the model reads about 100,000 tokens even for a question of a few words, and the
answer may need one sentence of one file.

### The three questions of today

Parts 2 to 6 come back to these three questions of your test set.

| # | Question | What it puts to the test |
|---|---|---|
| 3 | In Bouches-du-Rhône, at which fire-risk levels is access to forest massifs forbidden, and at the 'severe' level, when is work allowed? | A fact that only the full text of an official document gives, not the summaries |
| 7 | How many hectares burnt in Campania in 2025? | An answer that exists nowhere: the right answer is to say so |
| 10 | How many hectares burnt outside the EU in 2025? | Two sources disagree: the chatbot must point out the contradiction, not choose |

### What to do

#### Step 1 - Look at the gauge

1. Type:

   ```bash
   workshop B
   ```

   The first time, Claude Code asks again to trust this folder: press the **down arrow** to
   choose `Yes, I trust this folder`, then **Enter**. The gauge then shows `0 / 200k`: it counts
   what was sent at the last exchange, and nothing is sent yet. The kit goes with your first
   message.
2. Ask question 10: `How many hectares burnt outside the EU in 2025?`, and look at the gauge. At
   the rehearsal, it showed about **100,000 tokens out of 200,000** after this question: half of
   the window, almost all of it the kit.

   ![The gauge in mode B after question 10, in the red frame: 50% of context, 100.7k / 200k.](images/gauge-b.png)
3. Read the answer. Does it see that two documents give different figures?
4. Leave with **Ctrl+C twice**.

#### Step 2 - Predict, replay, score

1. **Predict** on paper: which questions will go up from column A to column B? Question 3? Question
   7? Question 10?
2. Replay the test set in mode B:

   ```bash
   replay B
   ```

   At the rehearsal: 1 min 35, and **$0.47**, about five times the $0.09 of mode A in workshop 1.
   Every question sends the whole kit again.
3. Score today's three questions (3, 7 and 10) with the help of the judge. This time it proposes
   a score, and you accept it (Enter) or correct it (0, 1 or 2):

   ```bash
   score B 3 7 10
   ```

   If you have time, score the other questions too (no question 12 written? leave out the 12):

   ```bash
   score B 1 2 4 5 6 8 9 11 12
   ```

   > ℹ️ **Note.** `score B` without numbers scores all the questions again, also 3, 7 and 10:
   > give the numbers. Workshop 3 compares questions 11 and 12 with column B: if you only have a
   > minute, score these two first, with `score B 11 12`.

4. **Compare columns A and B** in `scores.md`, for questions 3, 7 and 10, and with your prediction.
   Compare the two totals only if both columns have all their questions scored. No column A,
   because you started without a save? Type `replay A`, then `score A`, first: with Feurisson, we
   measured 1 min 12 and $0.09 (before its protection rules were added).

   **What to look for.** In mode A, the chatbot had no documents, so a precise question mostly got
   an honest "I don't know". A score that goes up in column B means that the model found the fact in
   the kit. Question 7 should not go down: more documents must not make it invent. On question 10,
   look for both figures in the same answer: the model can only compare them because it has both
   documents.

> 💡 **Tip.** **Checkpoint**: questions 3, 7 and 10 are scored in column B, and you have read the
> gauge.

### Think about it

The kit has 37 files, and they fill half of the window. **What happens with ten times more
documents?** And if your group adds one document a week? (Hint: the window has a maximum size, and
every message pays for what is in it.)

> **You built** a chatbot that reads everything. **Reused in** the *Knowledge* box of a chat tool,
> as long as the knowledge is small.

---

## Part 3 - Unplugged: be the search engine (★, 15 min)

**Goal**: do by hand what a RAG does: pick a few pieces of documents for a question, and answer
with these pieces only.

### What you will discover

- **A piece** (a *chunk*): a part of a document, cut before any question is asked.
- **A search engine** gives the model only the pieces it picks: the model never sees the rest.
- **Two failures**: the answer is cut in two pieces, and only one is picked; or there is no
  answer, and pieces are picked anyway.

### How it works

Two pairs work together. The facilitator gives an envelope of paper strips: each strip is a
sentence or a paragraph copied from a summary of the kit.

- **Pair 1 is the search engine.** It reads the question card, looks through the strips, and
  passes **3 strips** (round 1) or **2 strips** (round 2) to pair 2. It must always pass strips.
- **Pair 2 is the model.** It answers the question with the strips it received, and nothing else.
  Not its memory, not the other strips.

Then you compare the answer with question 10 or question 7 of `test-questions.md`.

### What to do

1. **Round 1 (small strips, one sentence each), question 10.** Pair 1 has 2 minutes to pass 3
   strips. Pair 2 answers in one or two sentences. Does the answer see that two sources disagree?
2. **Round 1, question 7.** Same thing. The strips about Campania are not about 2025. What does
   pair 2 answer?
3. **Round 2 (big strips, one paragraph each), question 10.** Swap roles. The new search engine
   passes 2 strips. Is it easier to give the model both sides of the contradiction?
4. **Talk about it in your group of two pairs**: how did the search engine choose? By the words of
   the question, or by their meaning?

**Key insight:** the model can only use what it receives. If the search engine does not pick the
piece that holds the answer, the model cannot find it. And a search engine always gives something,
even when the answer exists nowhere.

> 💡 **Tip.** **This activity works with young people**, with no computer: strips of their own
> documents, a question, and a pair that plays the search engine. The strips of this workshop, to
> print or to use as a model: [paper strips](https://youth-ai-lab.github.io/yal-workshop/2/strips.html).

> 💡 **Tip.** **Checkpoint**: your group can say where the answer was cut.

---

## Part 4 - Pieces and embeddings (★★, 20 min)

**Goal**: ask Open WebUI which pieces its RAG gives the model, for three questions, and read them.

### What you will discover

- **Chunks**: Open WebUI cut the 37 files of the kit into pieces of **at most** 1,000 characters
  (a short paragraph), before any question. It cuts at the end of a paragraph, so most pieces are
  shorter: the excerpts we measured had 770 characters on average.
- **Embeddings**: a small model turns each piece, and each question, into a list of numbers. Two
  texts with close meanings get close numbers. The search engine compares these numbers.
- **Top-k**: the number of pieces the model receives for each question. Here, 5.

In Part 3, you did this by hand: each strip was a chunk, and the number of strips you could pass
was the top-k. Open WebUI does the same job with numbers.

```mermaid
flowchart LR
  D["37 files of the kit"] --> C["cut into pieces (chunks)"] --> E["each piece becomes numbers (embedding)"]
  Q["Your question"] --> QE["the question becomes numbers"]
  E --> S{"closest pieces"}
  QE --> S
  S -->|"top-k = 5"| M["Model"]
  M --> R["Answer"]
```

**Key insight:** the search engine works before the model, and the model never sees the rest
of the documents. A RAG is only as good as the pieces it picks.

### How a text becomes numbers

**A map of meanings.** Think of a map. Each text gets a place on it, and texts about the same thing
sit near each other. The list of numbers is that place, like the coordinates of a town. A town
needs two numbers. Here, each text gets **384**: a meaning has many more directions than north and
east. Question 10 starts with `0.090, 0.084, 0.047, 0.003, 0.041, -0.064, -0.064, -0.046`, and 376
numbers follow. Nobody wrote these numbers, and no single one means "fire" or "Europe". The small
model (its name is `all-MiniLM-L6-v2`) learnt to place texts by training on a very large number of
sentences.

**A score of closeness.** Picture each text as an arrow, from the centre of the map to its place.
All the arrows have the same length, so only their direction counts. Two texts about the same thing
point nearly the same way: what matters is the **angle** between the two arrows.

The search does not measure this angle with a protractor. It multiplies the two lists number by
number, then adds up the results. This sum is called the **cosine** of the angle. Here it is with 2
numbers, so that you can draw it on paper (the numbers are made up for the example):

| | First number | Second number | Sum |
|---|---|---|---|
| Text A | 0.6 | 0.8 | |
| Text B | 0.8 | 0.6 | |
| A × B | 0.48 | 0.48 | **0.96** |

With 384 numbers, nobody can draw the arrows, but the sum is computed the same way, from the numbers
$a_1$ to $a_{384}$ of one text and $b_1$ to $b_{384}$ of the other:

$$
\cos(\text{angle}) = a_1 b_1 + a_2 b_2 + \dots + a_{384} b_{384}
$$

Open WebUI then turns this sum into a score between 0 and 1:

$$
\text{score} = \frac{1 + \cos(\text{angle})}{2}
$$

| The two arrows | Angle | Cosine (the sum) | Score |
|---|---|---|---|
| Same direction | 0° | 1 | **1** |
| Text A and text B | 16° | 0.96 | **0.98** |
| *wildfire* and *fire in the woods* (measured) | 51° | 0.625 | **0.813** |
| Right angle | 90° | 0 | **0.5** |
| Opposite directions | 180° | -1 | **0** |

So a score near 1 means almost the same direction. A score around 0.5 means a right angle: the small
model sees no link between the two texts.

**Predict before you look.** Here are pairs of texts. With your partner, sort them: which pairs does
the small model find close? Which does it find far apart? Then open the answer below.

- *wildfire* and *forest fire*; *wildfire* and *campfire*; *wildfire* and *birthday cake*;
  *wildfire* and *incendie de forêt* (French for "forest fire").
- *burnt outside the EU* and *burnt beyond the EU*; *outside the EU* and *inside the EU*.
- *Access to the forest is forbidden.* and *Access to the forest is allowed.*
- *1 092 095 hectares burnt.* and *2.2 million hectares burnt.*

<details>
<summary>The scores we measured with the small model</summary>

| Text 1 | Text 2 | Score |
|---|---|---|
| Access to the forest is forbidden. | Access to the forest is allowed. | **0.964** |
| burnt outside the EU | burnt beyond the EU | **0.944** |
| outside the EU | inside the EU | **0.935** |
| 1 092 095 hectares burnt. | 2.2 million hectares burnt. | **0.929** |
| wildfire | campfire | **0.865** |
| wildfire | forest fire | **0.844** |
| wildfire | birthday cake | **0.618** |
| wildfire | incendie de forêt | **0.559** |

</details>

**What these scores tell you.** In Part 3, you asked how the search engine chose: by the words of
the question, or by their meaning? Open WebUI compares meanings: "outside the EU" and "beyond the
EU" get 0.944. Question 10 says "outside the EU", summary 90 says "beyond the EU", and its piece
comes back.

But "meaning" has a limit. *Forbidden* and *allowed* get the highest score of the table: the two
sentences talk about the same thing, and only one word differs. The search finds **what a text is about**. It does not know
whether the text is true, or whether it answers you. That is the work of the model that reads the
excerpts, and then your work.

So the first decision comes before any question: **which documents may enter the base?** The model
and the reader can only judge what the search brings back. A bad document on the right subject will
come back. A missing passage cannot be judged at all. A document can even carry a sentence written
for the chatbot: workshop 4 shows this.

Look also at the last line. *Incendie de forêt* means forest fire, and the small model places it
further from *wildfire* than *birthday cake*. And *campfire* beats *forest fire*: nobody chose these
numbers, so they do not always follow your idea of meaning.

### One question, from start to end

Here is what happens for question 10, with the figures of our test. Each step can be explained.

**Before any question.** Open WebUI cut the 37 files into **322 pieces**, and the small model gave
each piece its 384 numbers. This is done once, and kept. That store is what we call a **base**.

1. **The question becomes numbers.** The same small model gives your question its 384 numbers.
2. **Each piece gets a score.** The search compares the question with the 322 pieces. The best
   score is 0.861, the worst 0.490, and half of the pieces are under 0.599.
3. **The search sorts the pieces and cuts the list after 5.** This is the top-k:

   | Rank | Score | File | Holds |
   |---|---|---|---|
   | 1 | 0.861 | `summaries/10` | the EU total and the 2 242 195 of all territories |
   | 2 to 4 | 0.855 to 0.853 | `corpus/text/10` (three pieces) | the same season |
   | 5 | 0.847 | `summaries/90` | **the 2.2 million "beyond the EU"** |
   | | | *the list is cut here* | |
   | 6 | 0.845 | `corpus/text/90` | the same season |
   | 7 | 0.832 | `summaries/10` | **the 1 092 095 hectares** |
   | 8 | 0.825 | `corpus/text/10` | the 1 092 095 hectares |

   The 1 092 095 hectares miss the cut by less than 0.02. The piece is not bad: it is just seventh, so with
   a top-k of 5 the model does not see it.
4. **Open WebUI writes the message.** It pastes the excerpts into the message for the model, in
   front of your question. We captured what leaves Open WebUI:

   ```
   System message:  the rules of the chatbot

   User message:    ### Task:
                    Respond to the user query using the provided context…
                    <context>
                    <source id="1" …>the text of the excerpt</source>
                    <source id="2" …>the text of the next excerpt</source>
                    …
                    </context>

                    How many hectares burnt outside the EU in 2025?
   ```

   The number `id` is the file: that is how the answer can name its sources.
5. **The model reads this message and writes.** It searched nothing. It does not know that 317 other
   pieces exist.

These steps are the three words of **RAG**: *Retrieval* (steps 1 to 3, the search), *Augmented*
(step 4, the longer message), *Generation* (step 5, the answer).

### What to do

1. Check that Open WebUI is ready: the last line of `.workshop/openwebui-start.log` says `READY`.
2. In your first terminal, ask which pieces the RAG would give for question 10:

   ```bash
   openwebui query "How many hectares burnt outside the EU in 2025?"
   ```

   You should see something like:

   ```
   Question: How many hectares burnt outside the EU in 2025?
   Base: excerpts of 1000 characters. Top-k: 5.
   The 5 excerpts the RAG gives the model (closest first):

   #1 summaries__10-eu-2025-wildfire-season.md (score 0.861)
      # The 2025 wildfire season in the EU (EFFIS figures) The 2025 fire season was the worst…

   #2 corpus-text__10-jrc-eu-2025-wildfire-season.md (score 0.855)
      …
   The model sees only these excerpts. Is the answer to your question in them?
   ```

   **Read this screen from the top.** `#1` is the excerpt closest to your question. An **excerpt**
   is a piece that the search gave back. The name after the number is its file: `summaries__10-…`
   is `summaries/10-…`, and `corpus-text__43-…` is `corpus/text/43-…`. The number in brackets is
   the score of closeness you just met. Each excerpt is printed whole, so scroll up in the terminal
   to read from `#1`.

   This command asks **no question to the model** that writes the answers: it only shows the
   search. It costs nothing, because the search uses the small model of Open WebUI, not your key.

3. **Read the 5 excerpts.** The expected answer points out that two sources disagree. For that, the
   model needs both sides: the 1 092 095 hectares of non-EU European countries (summary 10) and the
   2.2 million (summary 90). Which of these two files come back? Which of the two figures can you find?
4. Do the same for question 7 (`How many hectares burnt in Campania in 2025?`). The answer
   exists nowhere. How many excerpts come back? What are they about? Compare their scores with
   those of question 10.
5. Do the same for question 3:

   ```bash
   openwebui query "In Bouches-du-Rhône, at which fire-risk levels is access to forest massifs forbidden, and at the 'severe' level, when is work allowed?"
   ```

   Look at the names: which excerpts come from `corpus-text__43-…`? This is the full text of an
   order of Bouches-du-Rhône, a legal decision of the prefecture. Read these excerpts.
   The answer is in Article 4 (access) and Article 9 (work) of the order: lists of risk levels, with
   the word `INTERDITS` (forbidden). The start of the document is a list of lines that begin with
   `VU`. Did the search give you the articles, or something else?

**What we measured** (without the model, on the kit): for question 3, the pieces of document 43
came from its first page and, in the base of 1000, from Article 5 (the people the bans do not apply
to), never from the articles that answer, at every size. In the base of 1000, the two pieces with
the word `INTERDITS` come **56th** and **58th** of 322. For question 7, the RAG always gave 5 pieces.
For question 10, see Part 5.

**Why always 5?** The search does not ask "is this piece good enough?". It sorts the pieces from
the closest to the furthest, and takes the first 5. Even when no piece is really close, there is
always a first 5. You followed the same rule with the strips: always pass something.

The scores show it. Try it: `openwebui query "What is the best recipe for a chocolate cake?"`. In
our test, the best score is **0.573**, and the 5
excerpts are mostly lists of French towns. For question 7, the best score is **0.831**, close to
the 0.861 of question 10, and yet the answer is nowhere. Two excerpts talk about Campania, in 2017
and in 2026. Three talk about the hectares of 2025, in the EU. Here the low score said that nothing
was near, and the high score did not say that the answer was there.

> ℹ️ **Note.** Does the language explain question 3? Document 43 is in French, the question in
> English, and the small model was made for English. We tried the question in French. The search
> changes: 4 of the 5 excerpts now come from document 40, in French. The two pieces with `INTERDITS`
> move from 56th and 58th to 30th and 70th: neither comes back. So the language changes the result,
> and it does not explain everything. These pieces are lists of levels, with few sentences: this may
> count too, but **that was not tested**. Try the question in French, if you like, and tell the room
> what you see.

> 💡 **Tip.** **Checkpoint**: you have read the excerpts of questions 10, 7 and 3, and you can say
> what the search gave for each one.

### Think about it

For question 7, the model receives 5 excerpts, and none of them holds the answer. What should it do
with them? What could make it say so? (Hint: which rule did you give your chatbot about what it
does not know?)

---

## Part 5 - Change the settings (★★★, 20 min)

**Goal**: change the size of the pieces and their number, and see what changes for questions 3
and 10. Then ask the questions to the model in Open WebUI.

### What you will discover

- **Two bases**: the same 37 files, cut into pieces of at most 1000 and at most 2000 characters
  (the excerpts we measured had 770 and 1146 on average: many summaries are shorter than 2000). `workshop-start 2` prepared
  both.
- **`--top-k`**: more pieces for one search.
- **`openwebui top-k N`**: more pieces in the chat, from the next question, for every "Wildfire
  RAG" model.

### Two settings, two moments

You can change two things in this RAG, and they do not act at the same moment.

**The size of the pieces** is decided before any question: the documents are cut once. To try
another size, they must be cut again. This is why `workshop-start 2` prepared two bases in advance.

**The number of pieces** (the top-k) can change at each question: the search only takes more pieces
from the same sorted list.

Why change them? A small piece can lose what goes with a fact, like a strip in Part 3. A bigger
piece keeps more around it, and more pieces give the right one more chances to come back.

**A limit of the small model.** It reads at most 256 tokens of a text, and ignores the rest. In our
test, that was about 1,230 characters of English and about 780 of French. So a longer piece goes
whole to the model that writes the answer, but the search places it from its start only. We checked:
a new ending added after that limit does not change one of the 384 numbers. Past that limit, a
bigger piece carries more text to the model, and the search reads no more of it.

### What to do

#### Step 1 - Bigger pieces

1. Ask question 10 to the base of 2000:

   ```bash
   openwebui query --size 2000 "How many hectares burnt outside the EU in 2025?"
   ```

2. Can you find both figures now? We measured: with pieces of
   2000, the two sides of the contradiction come back together. With pieces of 1000 and 5 excerpts,
   summary 10 comes back, but not its piece with the 1 092 095 hectares: this is the first failure
   of Part 3, an answer cut in two.

#### Step 2 - More pieces

1. Back to the base of 1000, with 10 excerpts:

   ```bash
   openwebui query --size 1000 --top-k 10 "How many hectares burnt outside the EU in 2025?"
   ```

2. Both figures come back here too, as we measured. **What matters is what the pieces contain**:
   bigger pieces, or more of them, can both bring the answer. Both also send more text to the
   model at every question.
3. Try question 3 with bigger pieces, then with more pieces:

   ```bash
   openwebui query --size 2000 "In Bouches-du-Rhône, at which fire-risk levels is access to forest massifs forbidden, and at the 'severe' level, when is work allowed?"
   ```

   ```bash
   openwebui query --size 1000 --top-k 10 "In Bouches-du-Rhône, at which fire-risk levels is access to forest massifs forbidden, and at the 'severe' level, when is work allowed?"
   ```

   Does anything bring back the article that answers?

   We measured: no, at either size, even with 10 excerpts. In the base of 1000, the two pieces with
   `INTERDITS` are 56th and 58th: a top-k of 10 stops long before them. The settings change how much of the
   search result the model gets. They cannot bring back a passage that the search does not place
   near your question. In workshop 3, the model searches by itself: in our test, it opened this
   order.

#### Step 3 - Ask the model, in Open WebUI

1. Open the address given in `.workshop/openwebui-start.log` (`Ctrl` + click), or the **Ports**
   tab → `3000` → **Open in Browser**.
2. **New Chat**, then choose **Wildfire RAG 1000** in the message box, at the bottom right. Ask
   question 10. The list also shows **Wildfire RAG (workshop kit)**: it uses the same pieces of
   1000 as Wildfire RAG 1000, and `replay RAG` uses it in Part 6.

   ![The list of models of Open WebUI, opened from the message box. 1: Wildfire RAG 1000. 2: Wildfire RAG 2000. Wildfire RAG (workshop kit), at the top, is the one proposed.](images/rag-models.png)

3. Under the answer, click **Sources** (with their number, for example `3 Sources`): it lists the
   files that the excerpts came from. The grey labels in the text show which file each sentence
   comes from. Click a file in the list: its whole passage opens, with a score in percent. It is not
   the score of Part 4 (we did not look for its formula), so do not compare them. Do you find the
   1 092 095 hectares? Look again at the next step, with **Wildfire RAG 2000**.

   ![An answer of Wildfire RAG 1000 to another question. 1: a grey label in the text, the file of this passage. 2: the button 3 Sources, opened on the list of the files.](images/rag-sources.png)

4. **New Chat** with **Wildfire RAG 2000**, same question. Compare the two answers.

We measured these two answers with the model of the workshop:

- **Pieces of 1000**: the answer subtracts the EU from the total (about 1 162 657 hectares), says
  that this is its own calculation, and sees that the 2.2 million disagrees. But it "can't tell
  which reading is correct", and the figure of 1 092 095 hectares is not in its excerpts. The judge
  gave 1.
- **Pieces of 2000**: the answer gives 1 092 095 + 70 562 hectares, writes that "the sources
  disagree", and explains why: "The figures add up only if the 2.2 million includes the EU". The
  judge gave 2.

**Check it with a calculator.** Summary 10 gives the three parts of its total:

| Where | Hectares |
|---|---:|
| EU | 1 079 538 |
| Non-EU European countries | 1 092 095 |
| Middle East and North Africa | 70 562 |
| **All territories** | **2 242 195** |

The parts add up exactly. Outside the EU, that makes 1 092 095 + 70 562 = 1 162 657 hectares: the
same figure as the subtraction, by a second road that the 5 pieces of 1000 did not give. Summary 90
says 2.2 million beyond the EU, almost twice as much. But 2 242 195, EU included, rounds to 2.2
million: the two agree only if the 2.2 million includes the EU. This sum does not show which source
is right: the answer with pieces of 2000 also says "I can't confirm this from the excerpts alone".

**Only the pieces changed.** Open WebUI lists Wildfire RAG 1000 and 2000 as two "models", but behind
them the model and the instructions are the same. With pieces of 1000, it only had the totals. With
pieces of 2000, one piece also held the detailed figures. Your own answers will not be word for word
the same: the same chatbot does not write exactly the same answer twice ([why](https://github.com/Youth-AI-Lab/yal-local-ai-guide/blob/main/how-an-llm-works.md#temperature)).

5. If you want, give the chat 10 excerpts:

   ```bash
   openwebui top-k 10
   ```

   Ask again with **Wildfire RAG 1000**. Does the answer now give the 1 092 095 hectares? Then
   **set it back to 5** before Part 6:

   ```bash
   openwebui top-k 5
   ```

> ⚠️ **Important.** `replay RAG` refuses to run when the chat does not get 5 excerpts: column RAG is
> always measured with 5, so that the pairs can compare. Type `openwebui top-k 5` before Part 6.

> 💡 **Tip.** **Checkpoint**: you have compared the two answers to question 10, and the chat is back
> to 5 excerpts.

### Think about it

Bigger pieces found question 10. Why not always use the biggest pieces? (Hint: what does the
model receive at every question, and what does it pay for?)

---

## Part 6 - RAG against everything in the context (★★, 10 min)

**Goal**: replay the test set with the RAG of 1000, score column RAG, and compare it with column
B: answers and cost.

### What to do

1. Replay the 11 questions (and your question 12) with the RAG:

   ```bash
   replay RAG
   ```

   Each question goes to the chatbot "Wildfire RAG (workshop kit)" of Open WebUI (the same pieces
   of 1000 as Wildfire RAG 1000), in a new conversation. The answers go into a new file of the
   folder `answers/`: the line that starts with `Answers:`, near the end, gives its name, for example
   `Answers: answers/RAG-15h20.md`. Open it: under each answer, it shows which documents the
   excerpts came from. We measured 3 to 11 seconds per question.

   The line `Answers:` also says `cost: not shown by Open WebUI`, so our figure of about **$0.14**
   for 11 questions is an estimate, made from token counts. Under each answer, the line
   `Context: … tokens` gives the size of what the model read: we measured 1,872 to 2,869 tokens per
   question, against about 100,000 in mode B.
2. Score questions 3, 7 and 10, with the help of the judge:

   ```bash
   score RAG 3 7 10
   ```

   A column **RAG** appears in `scores.md`, after column B. If you have time, score the other
   questions too (no question 12 written? leave out the 12):

   ```bash
   score RAG 1 2 4 5 6 8 9 11 12
   ```

   > ℹ️ **Note.** Workshop 3 compares questions 11 and 12 with columns B and RAG: if you only
   > have a minute, score these two first, with `score RAG 11 12`.

3. **Compare columns B and RAG** for questions 3, 7 and 10, then the costs: $0.47 for B as we
   measured, about $0.14 for the RAG as we estimated. Compare the two totals only if both columns
   have all their questions scored.

**Do the sum.** The RAG reads about 40 times less than mode B (about 2,400 tokens per question on
average, against 100,000), but it costs only about 3 times less. In our test, the model cost
$2 per million tokens read and $10 per million tokens written. For the 11 questions of the RAG:

| | Tokens | Cost |
|---|---|---|
| Read | 26,789 | 26,789 × $2 ÷ 1,000,000 = $0.054 |
| Written | 8,633 | 8,633 × $10 ÷ 1,000,000 = $0.086 |
| Total | | about **$0.14** |

First, a RAG cuts the reading, not the writing, and a written token costs five times more than a
token read: here, writing is most of the bill. Second, mode B does not pay full price. At full price, 11 × 100,000 tokens read would cost $2.20, and we measured $0.47 for everything. The
service that runs the model keeps the text it has just received for a short time (a *prompt cache*),
and charges less when the same text comes back. So each message that follows soon after pays for
all of it again, but at a lower price.

> ℹ️ **Note.** These costs are paid with the key of your pair. Other ways to pay for a model:
> [OpenCode guide, five ways to pay for the model](https://github.com/Youth-AI-Lab/yal-opencode-guide#before-you-start-five-ways-to-pay-for-the-model).
> A model on a computer of your organisation has no cost per question:
> [local AI guide](https://github.com/Youth-AI-Lab/yal-local-ai-guide).

> ℹ️ **Note.** The two columns do not use the same instructions. Column B uses your `AGENTS.md`.
> The chatbot "Wildfire RAG (workshop kit)" does not read it: it has fixed instructions, the rules
> of Feurisson (`examples/AGENTS.feurisson.md`) adapted to excerpts. If your `AGENTS.md` is very
> different from Feurisson, part of a difference can come from the instructions, not from the
> pieces.

What we measured, with the judge: 18 out of 22 for the RAG of 1000, 19 out of 22 for the
one of 2000. Question 7 got 2 at both sizes: the model said that the excerpts did not contain the
answer, although it always got 5. Question 3 got 1 at both sizes: the article that answers was
never in the excerpts.

**Look at questions 3 and 7 side by side.** With pieces of 1000, the chatbot said "I don't know" to
both. For question 7, this is right: the answer exists nowhere. For question 3, the answer is in the
kit, in document 43, but the search did not bring it. In the chat, the two answers look alike. Only
your test set shows the difference, because it says that question 3 has an answer.

Why did it not invent an answer to question 7? Its fixed instructions say: *If the information is
not in the excerpts you were given, say "I don't know".* We did not measure this chatbot without
this rule.

> 💡 **Tip.** **Checkpoint**: questions 3, 7 and 10 are scored in columns B and RAG, and you can name
> one question where the pieces made the difference.

---

## Part 7 - Closing (10 min)

**Goal**: decide when a RAG is a good choice, see what some chat tools do on their own, and save
your work.

### When to choose a RAG

| | Everything in the context (B) | RAG |
|---|---|---|
| **Who picks the pieces** | nobody: everything enters | a search engine, before the model |
| **Size of the knowledge** | limited by the window | can be much bigger |
| **Cost of a question** | everything, every time | only the pieces |
| **Its failure** | stops when the knowledge grows | **always gives something**, even when the answer is not in the pieces: the failure is invisible |

**Key insight:** a RAG does not fail loudly. When it picks the wrong pieces, the model still gets 5
excerpts, and it may answer from them with confidence. That is why the test questions matter: they
show the failures that the chat does not show.

**In practice.** If your documents are few and short, put them all in the context: it is simple, and
the model can compare them. If they no longer fit, or if each message costs too much, use a RAG, and
keep testing it with questions whose answers you know.

**Why not cut under a score?** After the cake at 0.573, you may want to keep only the excerpts above
0.75. Our figures show the trap. Question 7, which has no answer, stays at 0.831. The two pieces with
`INTERDITS`, which answer question 3, are at about 0.72. The cut would keep the empty answer and
remove the right one.

### What some chat tools do on their own

Their help pages, read on 2026-10-29, say:

- **Claude Projects**, on paid plans: when the knowledge of a project "approaches the context
  window limit, Claude will automatically enable RAG mode", with "a visual indicator", and you
  see Claude "using a project knowledge search tool". You cannot choose. ([Claude help centre](https://support.claude.com/en/articles/11473015-retrieval-augmented-generation-rag-for-projects))
- **Gemini**: going beyond the context window "could lead to responses that don't take into
  account all the content provided or miss connections or details". No switch to a search is
  documented.
  ([Google help](https://support.google.com/gemini/answer/16275805?hl=en))

So the same *Knowledge* box can read everything, search for pieces, or miss part of it, depending
on its size and the tool. Claude Projects shows when it searches, but you do not choose. Gemini's
help does not say how you would know that part was missed.

### Save your work, fill in the exit card

1. Type `workshop-save`, then right-click on `my-work.zip` → **Download...**. Bring it to workshop 3.

   ![1: my-work.zip in the file list. 2: the item Download... of the menu that opens with a right-click.](images/download-zip.png)

   If your computer already has a `my-work.zip`, the new one may be called `my-work (1).zip`:
   bring the newest.
2. Take a blank card or a half sheet from the facilitator. This is your **exit card**. Answer alone, in a few words:
   1. Who picks the pieces in a RAG, and when?
   2. Name one question where the size or the number of pieces changed the answer.
   3. Why is a RAG's failure harder to see than a failure of mode B?

> **You built** a RAG, and you know how to check its pieces. **Reused in** the knowledge base of an
> Open WebUI chatbot
> ([Open WebUI guide, Step 1 - Gather your documents](https://github.com/Youth-AI-Lab/yal-openwebui-guide#step-1---gather-your-documents-knowledge),
> then [Step 4 - Try it](https://github.com/Youth-AI-Lab/yal-openwebui-guide#step-4---try-it),
> to read the passages found), and on a computer of your organisation
> ([local AI guide, What we measured](https://github.com/Youth-AI-Lab/yal-local-ai-guide#what-we-measured):
> the same two failures, with local models). In the chatbot of the Open WebUI guide, by default, the
> model decides itself when to search (a line "Explored…" or "View Result from…" above its answer);
> here, Open WebUI searched before every answer.

**Next:** [Workshop 3 - Let it search, give it know-how](https://github.com/Youth-AI-Lab/yal-workshop-search). Open its own Codespace from that page, and
bring `my-work.zip`.

---

## Troubleshooting

The common problems (key, Codespace, terminal) are in the
[Troubleshooting of SETUP.md](SETUP.md#troubleshooting).

**The log ends with `STOPPED: …`** - Read the message above it, then type, in a terminal:
`openwebui start && openwebui sizes`.

**`The search still finds nothing in …`** (in the log), or a base gives no excerpt. - At the end
of its preparation, Open WebUI checks each base with a test search, and restarts once if a base
finds nothing. If that is not enough, type `openwebui stop`, then
`openwebui start && openwebui sizes`.

**`Open WebUI is already being prepared.`** - `workshop-start 2` is still preparing it. Follow it
with `tail -f .workshop/openwebui-start.log` and wait for `READY`.

**`Open WebUI is not running, or not ready yet.`** - Wait for `READY` in the log. If the Codespace
stopped, type `openwebui start`.

**`replay RAG` says that the models get 10 excerpts.** - You changed the top-k in Part 5. Type
`openwebui top-k 5`, then `replay RAG` again.

**`Open WebUI is not started here (not a Codespace or a dev container).`** - Open WebUI only starts
by itself in a Codespace or a dev container. Elsewhere, type `openwebui start && openwebui sizes`.

**`This repository is for workshop 2. Workshop … has its own repository…`** - You typed
`workshop-start` with the number of another workshop. Nothing was changed. Here, type
`workshop-start 2`.

---

Texts and screenshots: [CC BY-SA 4.0](LICENSES/CC-BY-SA-4.0.txt). Configuration and programs:
[EUPL-1.2](LICENSES/EUPL-1.2.txt). The official documents are not ours and are not covered: see
[their note](LICENSES/LicenseRef-Third-Party.txt) and [`REUSE.toml`](REUSE.toml).

*Youth AI Lab (Erasmus+) - Workshop 2 of the series "Build your own chatbot" - 2026*
