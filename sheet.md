# Workshop 2 - Everything in the context, then RAG (one page)

**Question of the day: who picks the pieces?**
Full page: [README.md](README.md). Setup and common problems: [SETUP.md](SETUP.md).

| Score | When |
|---|---|
| **2** | Right, and it says where it comes from (7 and 9: saying "I don't know" or refusing is right). |
| **1** | Honest but not enough: "I don't know" although the answer exists, no source, or partly right. |
| **0** | Wrong or invented. |

## 1. Welcome (20 min)

1. Idle timeout not set yet on this account? First: [SETUP.md, step 1](SETUP.md#step-1---let-the-codespace-wait-for-you).
2. Open the Codespace: **https://codespaces.new/Youth-AI-Lab/yal-workshop-rag** → **Create codespace**.
3. Terminal 1: `workshop-login`, paste the key once, Enter → you see `Key OK`. Then `workshop bare`
   once. First time: keep the theme (Enter), Enter on the other screens; to trust the folder,
   **↓** to `Yes, I trust this folder`, Enter. `Ctrl+C` twice.
4. Drag `my-work.zip` into the file list (the newest: maybe `my-work (1).zip`, then its exact name
   between quotes). Terminal 1: `workshop-start 2 --from my-work.zip` → check the `saved on` date
   (no save: `workshop-start 2`, and Feurisson becomes your system prompt).
5. Open WebUI now starts in the background (about 4 to 5 minutes the first time): go on with
   Part 2. If `workshop-start` says `Open WebUI is not started`, do what it says. To follow it,
   terminal 2: `tail -f .workshop/openwebui-start.log`. It must say `READY` before Part 4.
   `Ctrl+C` stops following, not Open WebUI. Type the other commands in terminal 1.
6. Row 12 of `test-questions.md` still empty? Write it now (its section **Question 12: your
   territory**), then `replay bare 12`, `replay A 12`, `score bare 12`, `score A 12`.

## 2. Everything in the context (15 min)

With `workshop-login --europe`, mode B does not run: skip this part, and go to part 3.

1. `workshop B` (first time: **↓** to `Yes, I trust this folder`, Enter; closed? type it again).
   The gauge says `0 / 200k` until your first message. Ask question 10, look at the gauge (about half of the window).
   `Ctrl+C` twice.
2. Predict: which questions go up from A to B?
3. `replay B`, then `score B 3 7 10` (Enter accepts the judge's score, or type 0, 1 or 2).
   If you have time: `score B 1 2 4 5 6 8 9 11 12` (no question 12 written? leave out the 12).
   One minute left: `score B 11 12` (workshop 3 uses them).
4. Compare columns A and B on 3, 7 and 10; the totals only if both columns are complete.
   No column A (no save)? `replay A`, then `score A`, first.

## 3. Unplugged (15 min)

Two pairs, one envelope of strips. Pair 1 is the search engine: it passes 3 strips (round 1) or
2 strips (round 2). Pair 2 is the model: it answers with these strips only. Questions 10 and 7.

## 4. Pieces and embeddings (20 min)

1. In the page, sort the pairs of texts by closeness, then open the scores. Forbidden and allowed
   are almost the same for the search: it finds what a text is about, not what is true.
2. Check that the log says `READY`. Terminal 1:
   `openwebui query "How many hectares burnt outside the EU in 2025?"` → read the 5 excerpts.
3. The same for question 7 (Campania 2025) and question 3 (Bouches-du-Rhône).

## 5. Change the settings (20 min)

1. Question 10 with bigger pieces: `openwebui query --size 2000 "How many hectares burnt outside the EU in 2025?"`,
   then with more pieces: `openwebui query --size 1000 --top-k 10 "How many hectares burnt outside the EU in 2025?"`.
2. Open WebUI (Ports → 3000): question 10 to **Wildfire RAG 1000**, then to **Wildfire RAG 2000**.
   Click the sources.
3. Optional: `openwebui top-k 10`, question 10 again to **Wildfire RAG 1000**. Then
   **`openwebui top-k 5`** before Part 6 (`replay RAG` refuses otherwise).

## 6. RAG against B (10 min)

`replay RAG` (it asks **Wildfire RAG (workshop kit)**, the same base as Wildfire RAG 1000), then
`score RAG 3 7 10`. If you have time: `score RAG 1 2 4 5 6 8 9 11 12`; one minute left:
`score RAG 11 12` (workshop 3 uses them). Compare columns B and RAG on 3, 7 and 10 (the totals
only if both columns are complete), and the costs. No column B (`--europe`): compare with column A.

## 7. Closing (10 min)

1. When is a RAG a good choice? What failure does it hide?
2. `workshop-save` → right-click on `my-work.zip` → **Download...**. Bring it to [workshop 3](https://github.com/Youth-AI-Lab/yal-workshop-search). If your
   computer already has one, the new one may be called `my-work (1).zip`: bring the newest, and
   next time type its exact name between quotes after `--from`.
3. Exit card: three answers, alone.

**Leave a conversation:** `Ctrl+C` twice. **Copy / paste in the terminal:** `Ctrl+Shift+C` /
`Ctrl+Shift+V` (`Cmd+C` / `Cmd+V` on a Mac). **Never make port 3000 public.**
