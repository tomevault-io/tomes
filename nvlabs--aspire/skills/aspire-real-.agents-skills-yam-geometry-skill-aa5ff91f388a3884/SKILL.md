---
name: yam-geometry
description: Use for YAM DOF, coordinate directions, tabletop/rack/trash geometry, camera frames, gripper geometry, and contact/placement offsets. Use when this capability is needed.
metadata:
  author: NVlabs
---

# YAM Geometry

YAM is bimanual. Each follower arm command path uses 6 arm joints plus 1
gripper command. Left/right follower RPCs are separate.

World-frame anchors, checked against the calibrated station XML:

- `+Z`: up.
- `+X`: from the arm bases toward the tabletop workspace; not image-right.
- `+Y`: left-arm side. `-Y`: right-arm side / scene-right in recent scripts.
- Arm bases: left `[0.2525, +0.31, 0.75]`, right `[0.2525, -0.31, 0.75]`.
- XML table top is `0.750 m`; top-camera support/table estimates often use
  `~0.760 m`. Keep model Z and live-depth support Z separate.
- Trash drop gripper orientation: point along `+X` when the gripper should face
  away from the robot.

Verify against current overlays and script state before changing waypoints.

References:

- `references/yam-geometry-ground-truth.md`
- `references/blue-gripper-geometry.md`
- `references/multiview-camera.md`

---
> Source: [NVlabs/ASPIRE](https://github.com/NVlabs/ASPIRE) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
