# Lightbulb PCB adapter notes

## Files and confirmed dimensions
- `insertAdapter.kcl`: rebuilt 3bit/nub variant; overall height **55.80 mm**, stem **6.35 mm**. Nub removed; flat insert end retains the supplied *overall* height, not an independently measured original PCB seating height.
- `snapAdapter.kcl`: rebuilt 2bit/twin-seat variant; overall height **55.37 mm**, stem **9.81 mm**.
- The initially reconstructed flanges used **25.90 × 17.80 × 3.26 mm** as plan-axis dimensions. After the user reported they were too wide and lacked the original diamond-like shape, both were changed to a clipped-square profile with **18.30 × 17.80 mm** unrounded plan bounds and **3.26 mm** thickness. The original STLs' rendered outlines informed this estimate; exact mesh tracing/fit verification is outstanding. `main.kcl` displays the two separate parts 40 mm apart, as a comparison layout.
- All driving dimensions and first-fit allowances are in `parameters.kcl`. Intended print material: PETG.

## Insert version
- Selected **Bambu AB011, M2.5 × OD4 × L4 mm**. Bambu's product listing and linked specification agree for AB011; the M2/AB009 listing and specification disagree on OD, so M2 was not retained.
- Axial blind pocket: **3.60 mm diameter × 5.00 mm depth**, with approximately **4.10 mm entry diameter**. This bore is an initial design allowance, not a manufacturer-verified pilot-hole recommendation.
- User's PCB hole: **3.18 mm**. Use an M2.5 screw with a head/washer that spans this hole and clears PCB components. Check screw engagement and bottom clearance before tightening.
- Installed OD4 insert leaves approximately **1.18 mm radial plastic** in the 6.35 mm stem. The user confirmed successful insert installation in the gold part; the pocket, entry and stem dimensions are unchanged in the fit revision.

## Twin PCB seats
- Both boards: **10.85 mm diameter × 1.58 mm thick**, locally **11.10 mm** across the break-off remnant.
- Revised after the user could not snap the PCB into the first PETG print: seat cavities **11.05 → 11.25 mm diameter**; axial capture gap **1.78 → 1.88 mm**; retaining throats **10.49 → 10.71 mm diameter**; nominal radial lip overlap **0.18 → 0.07 mm**.
- Cup wall reduced **1.30 → 1.20 mm** to keep the outside head size unchanged as the seat cavities grow. Overall heights, stem diameters, seat centers and relief-slot widths were unchanged in that revision. Revised insertion/retention force still requires a print test.
- Two equal seats on **13.00 mm centers**. Four spring sectors per seat, with 0.80 mm flex slots and a 3.00 mm-wide longitudinal break-off relief.
- Orient each board's break-off remnant toward a wide longitudinal gap. Remnant tangential width was not supplied; widen `reliefSlotWidth` if its actual width exceeds the gap.
- Wiring-access revision: both **9.60 mm solder recesses now open through the underside**, rather than ending at a solid cup floor. Cutters start at Z **46.87 mm**, below the head/flare, leaving a central **3.40 mm-wide bridge** between the two circular cuts and approximately **0.825 mm radial PCB ledges**. The stem partially occupies the inboard underside; wire entry is from the open outboard portions. Overall size, PCB seating heights, snap fits, slots, flange and thread are unchanged; the gold part and shared parameters were not edited.
- These openings are intended for the user's three wires and solder access. Wire insulation diameter and PCB pad/component locations were not supplied; actual routing clearance and revised head strength need a physical check.

## Reconstruction assumptions and limits
- This is a native reconstruction using supplied dimensions and rendered STL references, not an exact mesh trace. Unmeasured flange corner clips/radii, cone dimensions, seat spacing, and shoulder blends are editable estimates.
- The user reported a threaded end snapped during insertion; the fracture location and printing settings are not yet known. Both parts now use an earlier-starting 3-section shoulder: it begins at Z **8.50 mm**, has **5.10 mm radius** at Z **10.00 mm**, and transitions to **7.50 mm radius** at the upper section. This adds material around the unthreaded neck while retaining the existing helical pitch, crest and root dimensions. It is a proposed local reinforcement, not a demonstrated strength improvement or a repair to breaks within the thread itself; check socket clearance and test the printed connection.
- Modeled screw ends use **1.814 mm pitch**, **10.65 mm crest diameter**, four rounded helical turns and a relieved **9.56 mm core**. Pitch, crest diameter and rounding were checked against IEC 60061-1 sheet 7004-6-1; the relieved root/runout are a simplified first-fit reconstruction, not a gauged standard cap or an exact copy of the source thread.
- Thread handedness was reversed in the first reconstruction. Matched front-view close-ups confirmed the mismatch with the original 3bit STL. Both part files now use `ccw = false` with the +Z helix, and the new front-view winding matches the original. Thread pitch, diameters, rounding and turn count are unchanged. Boolean order was adjusted to execute the corrected winding without changing the intended shape.
- PETG snap force, fatigue, printed-hole shrinkage, corrected socket fit, electrical insulation and operating temperature have not been validated. Test with the fixture unpowered.

## Validation
- Both revised part entrypoints execute: **10 + 15 sketches, all fully constrained**. Main comparison layout also executes.
- Reviewed whole-part and close-up snapshots, the capsule sketch, insert pocket, paired seat ledges/lips and cut reliefs. Requested cavities are subtractions, not displayed cutter bodies.
- On the latest revised part exports, FDM mesh-integrity checks completed on one component per part without an integrity finding; sampled thickness/gap coverage was partial and no minimum requirements were provided. The 0.16 mm +Z screening flagged downward-facing regions on flange, thread/neck, and blue head/lips. It does not validate supports, fit, torque, layer bonding, heat or electrical safety. An earlier whole-project mesh check failed before this revision.
- Next: establish where the printed thread failed and test the revised neck, socket fit and narrowed flange without power. Keep the successful gold insert pocket unchanged. Further blue-fit adjustments remain available through `seatDiametralClearance`, `seatAxialClearance`, `lipOverlap` and `reliefSlotWidth`.
