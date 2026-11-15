# Lightbulb PCB adapter notes

## Files and confirmed dimensions
- `insertAdapter.kcl`: rebuilt 3bit/nub variant; overall height **55.80 mm**, stem **6.35 mm**. Nub removed; flat insert end retains the supplied *overall* height, not an independently measured original PCB seating height.
- `snapAdapter.kcl`: rebuilt 2bit/twin-seat variant; overall height **55.37 mm**, stem **9.81 mm**.
- Both flanges: **25.90 × 17.80 × 3.26 mm**. `main.kcl` displays the two separate parts 40 mm apart; this is a comparison layout, not an assembled product.
- All driving dimensions and first-fit allowances are in `parameters.kcl`. Intended print material: PETG.

## Insert version
- Selected **Bambu AB011, M2.5 × OD4 × L4 mm**. Bambu's product listing and linked specification agree for AB011; the M2/AB009 listing and specification disagree on OD, so M2 was not retained.
- Axial blind pocket: **3.60 mm diameter × 5.00 mm depth**, with approximately **4.10 mm entry diameter**. This bore is an initial design allowance, not a manufacturer-verified pilot-hole recommendation.
- User's PCB hole: **3.18 mm**. Use an M2.5 screw with a head/washer that spans this hole and clears PCB components. Check screw engagement and bottom clearance before tightening.
- Installed OD4 insert leaves approximately **1.18 mm radial plastic** in the 6.35 mm stem. The user confirmed successful insert installation in the gold part; the pocket, entry and stem dimensions are unchanged in the fit revision.

## Twin PCB seats
- Both boards: **10.85 mm diameter × 1.58 mm thick**, locally **11.10 mm** across the break-off remnant.
- Revised after the user could not snap the PCB into the first PETG print: seat cavities **11.05 → 11.25 mm diameter**; axial capture gap **1.78 → 1.88 mm**; retaining throats **10.49 → 10.71 mm diameter**; nominal radial lip overlap **0.18 → 0.07 mm**.
- Cup wall reduced **1.30 → 1.20 mm** to keep the outside head size unchanged as the seat cavities grow. Overall heights, stem diameters, flange dimensions, seat centers and relief-slot widths are unchanged. Revised insertion/retention force still requires a print test.
- Two equal seats on **13.00 mm centers**. Four spring sectors per seat, with 0.80 mm flex slots and a 3.00 mm-wide longitudinal break-off relief.
- Orient each board's break-off remnant toward a wide longitudinal gap. Remnant tangential width was not supplied; widen `reliefSlotWidth` if its actual width exceeds the gap.
- Support ledges surround a **9.60 mm solder recess**, now about **1.82 mm deep** because the increased axial gap lowers the PCB ledge by 0.10 mm. PCB component/trace keep-outs were not supplied and must be checked.

## Reconstruction assumptions and limits
- This is a native reconstruction using supplied dimensions and rendered STL references, not an exact mesh trace. Unmeasured flange corner clips/radii, cone dimensions, seat spacing, and shoulder blends are editable estimates.
- Modeled screw ends use **1.814 mm pitch**, **10.65 mm crest diameter**, four rounded helical turns and a relieved **9.56 mm core**. Pitch, crest diameter and rounding were checked against IEC 60061-1 sheet 7004-6-1; the relieved root/runout are a simplified first-fit reconstruction, not a gauged standard cap or an exact copy of the source thread.
- Thread handedness was reversed in the first reconstruction. Matched front-view close-ups confirmed the mismatch with the original 3bit STL. Both part files now use `ccw = false` with the +Z helix, and the new front-view winding matches the original. Thread pitch, diameters, rounding and turn count are unchanged. Boolean order was adjusted to execute the corrected winding without changing the intended shape.
- PETG snap force, fatigue, printed-hole shrinkage, corrected socket fit, electrical insulation and operating temperature have not been validated. Test with the fixture unpowered.

## Validation
- Both part entrypoints execute: **9 + 14 sketches, all fully constrained**. Main comparison layout also executes.
- Reviewed whole-part and close-up snapshots, the capsule sketch, insert pocket, paired seat ledges/lips and cut reliefs. Requested cavities are subtractions, not displayed cutter bodies.
- The engine's optional insert-part volume calculation returned an internal error; no volume, mass, mesh-integrity, DFM or production-readiness claim is made.
- Next: test-print the revised twin-seat head and corrected thread. Keep the successful gold insert pocket unchanged. Further blue-fit adjustments are available through `seatDiametralClearance`, `seatAxialClearance`, `lipOverlap` and `reliefSlotWidth`.
