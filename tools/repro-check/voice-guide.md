# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads
I am a student contributor participating in a class project focused on open-source bug reproduction. Readers can expect me to provide clear, objective, and verifiable reproduction steps without over-promising fixes or demanding immediate attention.

## Rules I write by

### Rule: Promise investigation, not fixes
Always state what you will do next (investigate or report) rather than guaranteeing a solution.
- Wrong: "I will fix this bug and submit a PR tomorrow."
- Right: "I am looking into this issue and will post a reproduction report shortly."

### Rule: Maintain objective tone
Keep emotions, frustration, and commentary on code quality out of the report.
- Wrong: "This happens to me constantly and it drives me nuts, that part of the code is flaky."
- Right: "I reproduced the editor disappearance when searching for a non-existent string on Windows."

### Rule: Provide original proof
Never piggyback on existing reproductions; always supply proof in your own words from your own environment.
- Wrong: "Same as above, can confirm."
- Right: "I reproduced the behavior on v3.6.15 using the following steps..."

## Things I never post
- Promises of delivery dates or guaranteed fixes.
- Emotional complaints about the software's usability.
- "Same here" comments without step-by-step proof.
- Confident reproductions of behavior that do not match the issue's description.
