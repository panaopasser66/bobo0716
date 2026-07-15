# Stage A data2 audit report

## Scope

- Stage A only: recursive audit, physical-location mapping, difference eligibility, and known-coordinate review.
- No model, detector, training set, threshold, or candidate injection was created.
- `data2/` was read-only; `outputs/waveform_v2/` and `outputs/waveform_v3/` were not modified.

## Session inventory

| session_id | view_count | target_00_count | target_01_count | target_02_count | complete_triplets | shapes | dtypes | exposure_ms | requested_average_frames |
|---|---|---|---|---|---|---|---|---|---|
| auto_capture_20260701_165437 | 105 | 105 | 105 | 105 | 105 | 1544x2048 | uint16 | 100.0 | 300 |
| auto_capture_20260702_092708 | 49 | 49 | 49 | 49 | 49 | 1544x2048 | uint16 | 100.0 | 300 |
| auto_capture_20260702_111834 | 44 | 44 | 44 | 44 | 44 | 1544x2048 | uint16 | 100.0 | 300 |
| auto_capture_20260702_133311 | 154 | 154 | 154 | 154 | 154 | 1544x2048 | uint16 | 100.0 | 300 |
| auto_capture_20260702_173319 | 44 | 44 | 44 | 44 | 44 | 1544x2048 | uint16 | 100.0 | 300 |

- All images are 1544x2048 uint16 TIFF files named `view_NNNN_target_XX.tif`.
- All sessions request 100 ms exposure and 300-frame averaging.
- kV and μA are not recorded in the audited metadata, config, or searched run-log fields.
- Run logs contain 35 early-sequence warnings; those acquisitions averaged 299/300 frames.

## Real-difference teacher availability

- Complete triplets: **396/396 views**.
- D01: **396**; D12: **396**; D02: **396**.
- Every discovered view can form all three offline teachers using float arithmetic: D01=T00-T01, D12=T01-T02, D02=T00-T02.

## Physical-location mapping

- Unique stage-coordinate groups: **154**; repeated across sessions: **144**.
- Map by `(base_x_mm, base_y_mm)`, not by view ID.
- 4 overlapping session pairs have sampled median target_00 correlation below 0.9. Coordinates provide candidate correspondence, but label transfer still requires registration or visual confirmation.

## Known-coordinate review pack

- Generated **9** items: five for view_0030 and four for view_0054.
- Each item includes T00/T01/T02, D01/D12/D02, and horizontal waveforms.
- Interpretation and corrected p0 fields remain blank for human review; coordinates were not inserted into any detector or training set.

## Stage A conclusion

- All 396 views support real-difference teacher construction.
- The nine coordinates are review anchors, not nine confirmed target_00 positives.
- Stage B should wait for completed coordinate review and additional authoritative/blind labels across independent sessions.
