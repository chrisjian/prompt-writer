# Claude Opus 5.5

Use Core. Add these deltas only when relevant:

- For fully unattended, multi-part agent tasks, explicitly instruct the model not to end its turn after a progress summary or next-step announcement while authorized work remains; allow stopping for real blockers or necessary authorization. Do not apply this to human-in-the-loop workflows.
- For loosely specified workflows across connected apps where necessary context may be dispersed, ask the model to inspect task-relevant sources, including likely relevant records not explicitly named, before taking action. Bound this by available permissions and the task's scope; broader exploration increases tool and token use.
