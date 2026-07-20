# Handoff: Josh's ML Self-Study + Resume Project

## Background
Josh is a Princeton Economics major, rising junior, pivoting toward math/ML/coding after realizing his resume (political campaigns, law firm internship, Congressional office) no longer reflects his actual interests. This summer he's technically interning at LB Capital (family-run, low external signal), but has spent the bulk of the summer self-teaching: conceptually studied the first half of COS 226 (algorithms, hand-written, no code artifact), did 2-3 weeks of LeetCode, then self-studied COS 324 (ML) — working through the math by hand and implementing applied coding projects in Colab notebooks. Claude generated practice prompts from course notes; Josh implemented all solutions independently and used Claude as a tutor to troubleshoot bugs and verify reasoning (never had Claude write code for him).

He is also working on a separate, more ambitious independent ML project in other chat sessions (visible to me as "Capstone Project Part 5" and "Part 6" — I have not touched those, just noted their existence).

Target internships for next summer: applied ML / data roles, possibly quant-adjacent (mentioned Kalshi, DraftKings as examples), open to "still deciding."

## Purpose of this project
1. Go back through his self-study Colab notebooks chapter by chapter, build READMEs, and assemble a public GitHub portfolio repo.
2. Eventually update his resume to reflect this technical pivot (not started yet).
3. Later: help explore internships for next summer.

## Repo state
- Local path: `~/Resume/ML-Self-Study` (also the Cowork-connected folder)
- GitHub: `https://github.com/joshuahpatrick85-beep/ML-Concepts`
- Structure: one subfolder per concept (currently `Chapter1-Linear-Regression/`), each containing the notebook + a README. Top-level `README.md` lists concepts (NOT "Chapter N" — Josh wants concept-based labeling, e.g. "Linear Regression," not "Chapter 1: Linear Regression"). Placeholder entries for unbuilt concepts read "In progress — concept TBD."
- `.gitignore` already added (`.ipynb_checkpoints/`, `__pycache__/`, `.DS_Store`, `*.pyc`).
- Git identity on Josh's machine is NOT configured (commits currently attribute to `joshpatrick@Joshs-MacBook-Air-2.local`) — offered fix, he hasn't done it yet: `git config --global user.name` / `user.email`.

## Known recurring issue: git lock files
Running git commands via my sandbox bash against Josh's synced folder repeatedly throws `Operation not permitted` / stale `.lock` file errors (looks like an iCloud-sync conflict). Workaround that's worked: have Josh run git commands himself in his own terminal; if he hits a `fatal: Unable to create '.../.git/X.lock': File exists`, it's safe to `rm -f` the lock file manually (no real process is stuck) and retry. When editing files that then need to be committed, I write via the Write/Edit tools (which go through the host filesystem successfully) rather than `cp`/`rm` via bash (which frequently gets `Permission denied` in that folder) — pull the file with Read first, then Write the full replacement.

## Attribution / honesty standard (important — apply consistently to every chapter)
Josh is sensitive about honesty in how AI involvement is disclosed — not about whether to disclose it, but about precision of wording. Agreed-upon standard, established through direct back-and-forth:
- Each chapter README ends with a "Tools" section describing that Claude generated practice prompts from course notes, Josh implemented all solutions independently, and used Claude to troubleshoot bugs / verify reasoning.
- Avoid vague intensifiers like "heavily used ... as a coding assistant" — this undersells his independent work and could misread as him not understanding the material. Be precise and scope Claude's role narrowly (generated prompts, gave feedback on bugs) rather than using broad language.
- Documentation disclosure line (top-level README and per-chapter): "This README was drafted by Claude from the notebook and my own account of the work, reviewed and edited by me." Do NOT let Claude auto-write these with zero input — always confirm content/accuracy with Josh first, and know he may edit further (sometimes directly on GitHub's web UI, which can mangle markdown — e.g. previously stripped `[...]()` link brackets by accident. Always verify rendered links/formatting survived his manual edits).
- Comment-cleanup philosophy (for polishing his own code comments): keep/strengthen comments that demonstrate understanding or catch a misconception (signal); cut comments that just narrate obvious syntax (noise). This is different from production-code commenting norms — for a self-study portfolio, "why/what I learned" comments are a feature, not a smell.

## Chapter 1: Linear Regression — COMPLETE
Closed-form linear regression from scratch (normal equations, no sklearn for the core solver), synthetic housing data, manual train/test split, MSE evaluation, plus a bag-of-words extension into text classification. Final, revised notebook (renamed variables, f-string prints, typos fixed, some comments intentionally trimmed) and README are both pushed to GitHub. This one required real back-and-forth on train/test discipline (Josh correctly worried at one point that `learned_w` might have leaked test data — it hadn't, `learned_w` uses only `X_train/Y_train`, a separate `learned_w_full` was fit on all data per Part D's explicit ask) and on why `X.T @ X` was singular for the bag-of-words case (rank-deficient because fewer reviews than vocab words — Josh worked this out himself after pushback, good example of him doing real reasoning, not being handed answers).

## Chapter 3 — SKIPPED (by design)
Josh only hand-derived gradient descent formulas for this one, no code artifact exists. Noted in task list as "completed (skipped)."

## Dimensionality Reduction, Clustering & Classification — COMPLETE
Integrated project (originally scoped in an earlier session as covering material labeled "Ch4/Ch6/Ch7" — PCA, k-means, and softmax classification) built on the sklearn digits dataset (1797 images, 8×8, 10 classes). PCA implemented via `np.linalg.svd` from scratch (center + project onto top singular vectors, no `sklearn.decomposition`), k-means from scratch (random init, assignment/update loop, 100 iterations, k=10) on the PCA-reduced 2D data, cluster-to-label alignment via majority vote for a real clustering accuracy, and a softmax/multinomial logistic classifier trained via gradient descent from scratch (no `sklearn.linear_model`). Results: k-means clustering accuracy 58.4%, softmax classifier 100% train / 97.2% test accuracy. Folder: `Dimensionality-Reduction-Clustering-Classification/`. Notebook and README are in the repo; not yet committed/pushed (Josh needs to run git commands locally).

Debugging note for continuity: this notebook had a real structural bug in the k-means loop (the assignment and centroid-update inner loops were not nested inside the outer iteration loop — same category of indentation bug as Chapter 1), plus two typos (`centroid_assigment` → `centroid_assignment`, `centroid[k]` → `centroids[k]`). Josh fixed both after the bug was flagged, not by being handed the fix.

Chapter numbering note: the earlier handoff pegged Chapter 6 as the FFNN-from-scratch chapter (strong resume differentiator). Confirmed with Josh (7/20) that FFNNs come later — course numbering has shifted since the original plan, so "Ch6" in this notebook's own labels (PCA/k-means/softmax) does not correspond to FFNNs. Don't assume FFNN content is covered by anything received so far; it's still upcoming.

Also noted in the same prior session: a separate bigram/language-model project using Moby Dick text (pulled from Project Gutenberg) was being scoped — no notebook for that has been uploaded yet. Treat as a distinct pending chapter, not part of this one.

## Remaining work (task list — see below)
- Chapter 8 README — not started, no notebook received yet.
- Chapter 9 README — not started.
- Bigram/language-model (Moby Dick) chapter — not started, no notebook uploaded yet; unclear which chapter number this maps to.
- FFNN-from-scratch chapter — location/numbering unclear (see discrepancy note above); confirm with Josh.
- Top-level README final pass + resume update — after all chapters done. Resume currently (as of last read) has zero technical/coding content; it's all politics/law internships plus a Beijing language program and one research assistant role (Julis-Rabinowitz Center, cleaning CIP-deviation time series data — this is actually decent quant-adjacent signal, worth keeping). Discussed but NOT decided: how much to trim the political/law section (leaning toward condensing to 1-2 lines each rather than cutting, but Josh deferred this decision — revisit).

## Workflow pattern to continue
Go project by project: Josh sends the finalized Colab notebook (as `.ipynb` upload) plus any relevant context, I read it, draft a README, iterate based on his feedback (he often catches wording/precision issues himself), write the final files via Write/Edit tools, then walk him through git commit/push (he runs commands in his own terminal; I don't have push credentials).

## Task list state (as of handoff)
1. Chapter 1 (Linear Regression) README — completed
2. Chapter 3 (Gradient Descent) — completed (skipped, hand-derivation only)
3. Dimensionality Reduction, Clustering & Classification README — completed, not yet committed/pushed
4. Chapter 8 README — pending
5. Chapter 9 README — pending
6. Bigram/language-model (Moby Dick) chapter — pending, notebook not yet received
7. FFNN-from-scratch chapter — pending, numbering unclear, confirm with Josh
8. Top-level README final pass + resume update — pending

## Resume snapshot (unedited, for reference)
Education: Princeton A.B. Econ candidate, expected May 2028, GPA 3.9/4.0. Coursework: Multivariable Calc, Linear Algebra, Financial Math, Financial Investments.
Experience: Princeton in Beijing (summer 2025 language program), Julis-Rabinowitz Center for Public Policy and Finance (Research Assistant, fall 2024, CIP deviation data cleaning), PA HRCC campaign intern, Dave McCormick for US Senate campaign intern, Keystone Boys State, Brandon J Broderick law firm intern, Congressman Brian Fitzpatrick district office intern.
Awards: Mary W. George Research Conference (household Treasury demand research).
No coding/technical content currently appears anywhere on the resume.
