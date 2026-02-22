# Copilot Instructions for this Repository

## Scope and intent
- Keep changes focused on the user request.
- Prefer the smallest possible diff that fully solves the problem.
- Do not refactor unrelated code.

## Code style
- Follow existing file and language conventions in the repository.
- Use descriptive names; avoid one-letter variables.
- Keep functions small and readable.
- Do not add new dependencies unless clearly necessary.

## File and architecture changes
- Preserve existing public APIs unless a change is explicitly requested.
- Avoid renaming/moving files unless required by the task.
- Update documentation when behavior, setup, or interfaces change.

## Safety and quality
- Fix root causes rather than patching symptoms.
- Add or update tests only when there is an appropriate test location/pattern.
- Run the most targeted validation available for changed code.
- Do not fix unrelated failing tests as part of the same task.

## Git and collaboration
- Never commit or create branches unless explicitly asked.
- Keep commit-ready changes clean and scoped.
- Include concise change notes listing what changed and any follow-up actions.

## Secrets and environment
- Never hardcode credentials, tokens, or secrets.
- Use environment variables and documented configuration patterns.

## PI directory release metadata
- Treat any directory matching `PI#` (for example, `PI1`, `PI2`, `PI10`) as a PI directory.
- Each PI directory must contain a `README` file that includes:
	- Target release date
	- Target release version tag
- If any PI directory is missing a `README`, or the `README` is missing either required value, explicitly tell the user which PI directory is non-compliant.
- Suggest a fix by adding/updating the PI `README` with both fields present and set to `TBD` when unknown:
	- Target release date: TBD
	- Target release version tag: TBD

## PI completion update requirement
- When a PI is processed, the final step must be updating the root-level `README.md`.
- Ensure `README.md` contains a section for that PI with:
	- A concise summary of the PI
	- A diagram of the solution as it currently exists ("as it now looks")

## Documentation diagram conventions
- Diagrams must be architecture-focused and show how repositories fit together.
- Do not include `README.md`, other Markdown files, or `LICENSE` files as diagram nodes.
- Use `Solution` as the single top-most node representing this repository.
- When documenting external repository references in diagrams (for example, Mermaid), use bracketed labels so external repos have a visually distinct shape.
- Prefer explicit external repo labeling in the node text (for example, `[WITPAE_Monitor - external repo]`).

## README repository index requirement
- The bottom section of the root-level `README.md` must contain a table of referenced repositories.
- The table must include, at minimum:
	- Repository name
	- Summary of what the repository does
- The summary for each repository must be a concise paraphrase derived from that repository's `README` content (do not copy it verbatim).
- Each repository entry must include a link to that repository's `README`.
- Summary derivation procedure for each referenced repository:
	- Use the repository link to locate that repository's `README` and derive the summary from that source.
	- If direct README page/raw URL retrieval fails, use the GitHub API contents endpoint (`/repos/{owner}/{repo}/contents/README.md`) and decode Base64 content.
	- Paraphrase the README into 1 concise sentence describing purpose and primary function.
	- Keep the repository table `README` link aligned to the source used for the summary.
- Diagrams in `README.md` must include clickable links on repository nodes that navigate to the matching repository entry in that table.
- Use stable anchor IDs for each repository table entry so diagram links remain valid as content evolves.
- Whenever a new repository is referenced in any PI section, add/update both:
	- The diagram node link for that repository
	- The matching repository table row and anchor in the bottom index
