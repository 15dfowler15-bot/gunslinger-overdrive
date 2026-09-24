# Gunslinger Overdrive v32.3 — Initial Revolver Resolution in RNG Math

Changes from v32.2:

- Initial-spin revolvers now resolve their legitimate shot effects before the dead-round decision, even when the raw initial reel stop has no payline.
- A revolver landing by itself still never earns a respin.
- If an initial revolver's Wild / Upgrade / other legitimate effect creates a valid 22-payline win, that resulting payline activates respin mode.
- If an initial Gold/NudgeX shot is pending and no payline otherwise exists, its final-turn drop resolves mathematically before the dead-round check. If that resolved expanded-Wild column creates a legal payline, respin mode activates.
- If all initial revolver/feature effects finish and there is still no valid payline, the round ends dead with no respin.
- This logic runs inside the normal paid-round RNG engine and therefore feeds the same RTP / simulation model rather than being a presentation-only exception.
- The v32.2 hard cap of 3 NudgeX bullets per paid round remains intact.

Regression coverage includes both a dead initial revolver shot and a Gold/NudgeX initial shot that legitimately creates the first payline.

## v32.4 — xNudge authoritative math correction
- Pending xNudge leaves underlying symbols/modifiers mathematically active until drop.
- Resolved xNudge suppresses covered symbol, Split, and cell modifiers for payout.
- xNudge has independent multiplier state and event history.
- +xNudge additions use +2/+3/+10/+100 and are additive.
- xSplit doubles the current multiplier of an xNudge Wild when it legitimately targets that Wild.
- Multiple xNudge Wilds used by one payline contribute additively.
- Final payline evaluation uses an explicit resolved-board representation.
- Paid-round simulation reports xNudge/xSplit-specific statistics.

## v32.5 additive feature math
When a normal surviving Split multiplier and one or more participating resolved xNudge multipliers apply to the same winning line, the independent feature contributions combine additively (e.g. Split x2 + xNudge x8 = feature x10). xSplit applied directly to an xNudge Wild still doubles that Wild's own current multiplier before payline combination.

## v32.6 mobile-safe patch
- No engine/math changes from v32.5.
- Re-encoded embedded artwork at display-appropriate resolutions to reduce standalone HTML memory/payload.
- Added iOS/mobile viewport and touch-action safeguards plus mobile debug-panel sizing.


## v32.7 — matching held symbols continue respins
- During active respins, a newly rolled exact regular symbol matching a symbol type already held from a winning payline counts as progression.
- It grants another respin even if it does not create a new payline or increase the payout.
- Wilds and special symbols do not count as these extra matching-symbol continuations.
- This rule lives in the core RNG paid-round cycle, so simulation/RTP measurement uses the same behavior.
- Simulation reports matchingSymbolContinuationFrequency.
