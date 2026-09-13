# Video Repair Tool

Windows batch diagnosis and repair for videos that import, play, or render
unreliably. Automatic repair tries validated container and timestamp corrections
without re-encoding before using decoded recovery when necessary.

![Video Repair Tool showing scan results and a proposed repair](https://raw.githubusercontent.com/skv89/video-repair-tool/v1.9.1/docs/images/video-repair-tool.png)

## Download and start

Download **Video-Repair-Tool-v1.9.2-Windows-x64.zip** from the
[v1.9.2 release](https://github.com/skv89/video-repair-tool/releases/tag/v1.9.2).
Extract the entire ZIP to a writable folder and run **Video Repair Tool.exe**.
The executable includes its GUI runtime; a separate Python installation is not
required. This repository distributes the portable application, not its source.

- Intended for 64-bit Windows 10 and Windows 11. Windows ARM emulation has not
  been validated.
- A matching FFmpeg/FFprobe 9.0-or-newer stable pair, or an accepted matching Git
  build, is required for scanning and repair. These tools are not bundled.
  **Tools → Dependency Doctor and local installer** can install/update them in
  the application-local runtime with your consent, without changing system PATH.
- NVIDIA hardware is optional. CPU repair paths work without it. NVIDIA decode
  and encode options depend on the active FFmpeg build, driver, GPU, and source.
- VapourSynth and QTGMC are not required. This application does not deinterlace.
- The executable is unsigned; Windows may display a SmartScreen warning.
  Verify the ZIP checksum in the release notes before running it.

## What's new in v1.9.2

- Corrects frame counting during **Deep Verify** and repaired-output validation
  for videos with uneven or closely spaced timestamps.
- Counts the pictures actually decoded without forcing them onto a fixed-rate
  clock. Corruption checks remain strict.
- Detects FFV1 checksum errors even when the decoder keeps running. Automatic
  repair confirms damage and attempts a separate, validated recovery copy.
- Handles cancellation during final repair checks more reliably and preserves
  any previous completed output when replacement is canceled.
- Keeps Automatic repair no-reencoding-first. Quality settings and field
  preservation are unchanged. These fixes add no extra routine full-file scan.

## Batch workflow

1. Drag files into the window, or use **Add Files** / **Add Folder**. The queue
   holds up to 99 media files.
2. Use **Delete** to remove selected rows from the queue, or drag rows to change
   their order. Neither operation deletes source files.
3. Click **Repair Selected** or **Repair All**. Required probes, timestamp
   checks, and deeper picture checks run automatically before repair.
4. Read **Problems detected** and **Proposed / actual repair**. Select a row to
   inspect stream metadata, timestamps, decode evidence, and the proposed plan.
5. The defaults prioritize preservation. Change the repair strategy, output
   profile, and source decoder before starting if you want different options.
6. **Probe / Quick Scan** and **Deep Verify Selected** remain available when
   you want to inspect files without starting a repair.

In Automatic mode, quick-healthy or inconclusive results receive a full video
check before the app decides whether repair is needed. Healthy files report
**No repair needed** without creating a duplicate. Timestamp-only candidates
skip that extra source decode because their repaired outputs receive complete
validation. Confirmed checks are reused while file identity and toolchain match.

**Cancel** stops checks and prevents the pending repair from starting. Files
that cannot be checked or repaired report **Needs attention** while eligible
files continue. Missing dependencies open setup guidance; installation still
requires your action. Lossy-profile and existing-output confirmations remain.

**Open Output Folder**, including its row right-click command, opens the actual
completed output directory with the repaired file selected in File Explorer.
It is disabled for unfinished, failed, canceled,
moved, deleted, or otherwise missing outputs.

## Repair strategy and quality

**Automatic** tries the least destructive applicable method first: an ordinary
stream-copy remux, then guarded packet-level timestamp normalization when
eligible. These methods preserve compressed video without re-encoding. The
selected encoder is only a fallback for necessary decoded repair.

**Stream-copy remux only** never re-encodes or falls back. **Force decoded
repair** deliberately uses the selected encoder even if a remux could suffice.

Available decoded-repair profiles include source-matched lossless FFV1 Intra,
FFV1 RGB 16-bit, FFV1 10-bit 4:4:4, ProRes 4444 XQ, DNxHR 444 10-bit,
capability-gated DNxHR 444 12-bit, HEVC NVIDIA 10-bit P6/P7, and AV1 NVIDIA
10-bit P7. FFV1 uses level 3, coder 2, context 1, slice CRCs, and intra-only
frames. Converting pixel format cannot restore missing source detail. ProRes,
DNxHR, HEVC, and AV1 are lossy.

NVIDIA HEVC/AV1 profiles request HQ tuning, full-resolution multipass, lookahead,
temporal AQ, and CQ 10. Source decoding and output encoding are separate
choices. Software decoding is the safest damaged-frame recovery default;
optional CUDA decoding can reduce CPU load, but may recover corrupt pictures
differently. The speed/quality popup explains the tradeoffs. Validation, hashing,
and disk access do not receive an NVENC speedup.

Field-order checks remain part of scanning and validation. Missing field
metadata triggers distributed decoded-frame-flag sampling; inconclusive evidence
blocks decoded repair. This is not an exhaustive image-content analysis.
The app preserves field dominance and nominal cadence and never deinterlaces.
Interlaced sources require a compatible FFV1 or ProRes profile; incompatible
DNxHR/HEVC/AV1 profiles are blocked.

## Safety and limitations

Original media is opened read-only and never overwritten. Repairs are created
at separate partial paths and promoted only after strict validation. Checks
cover picture decoding, packet timing, duration, geometry, field dominance,
color metadata, tracks, relative stream timing, hashes, and final reopen.
Existing completed outputs require replacement confirmation.

A quick scan is not a full-file decode guarantee. Repair cannot reconstruct
missing or undecodable original pictures. Some damage, such as a missing
MP4/MOV index requiring a matching reference recording, cannot be repaired
automatically. Large lossless outputs require substantial disk space.
Codec/container acceptance varies by target editor, including DaVinci Resolve;
a structurally valid output is not a guarantee of support by every application.
Keep originals and review repaired output.

Compatibility checks cover CPU-only operation, missing dependencies, batch
scanning, long and non-English paths, cancellation, field preservation, and
NVIDIA encoding. Testing is limited to one physical Windows x64 host plus
controlled compatibility configurations; it does not cover every computer,
GPU, driver, or damaged file.

## Diagnostics and notices

**Export Diagnostic Bundle** creates a ZIP of logs, scan/plan/validation data,
and toolchain information; it does not include source media payloads. Diagnostics
can contain local paths, filenames, and media tags. Review them before sharing.

The portable ZIP includes **Video Repair Tool Third-Party Notices.md** and the
runtime license texts in **Licenses**. FFmpeg and other separately downloaded
dependencies retain their own upstream licenses.
