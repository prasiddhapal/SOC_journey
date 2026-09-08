# 07 | Interview & Lessons

## Core lesson
A successful threat hunt can end with a well-supported benign/normal assessment.

## Interview points
- Why baseline? Because enterprise AD generates high event volumes.
- Why filter `$` accounts? To reduce machine-account noise during human-focused hunts.
- Does rarity prove maliciousness? No.
- Does an unusual IP prove compromise? No.
- Why check 4771 and 4688? They provide additional authentication-failure and endpoint evidence.
- What makes the conclusion defensible? Correlation and explicit confidence.

Analyst language used:
"Observed" -> "Suspicious" -> "Potentially malicious" -> "Confirmed" only as evidence supports.
