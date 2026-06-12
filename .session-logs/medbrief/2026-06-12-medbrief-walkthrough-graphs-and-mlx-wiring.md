---
date: 2026-06-12
project: /Users/Rowan.Reid/claude_code/medbrief-onboarding
domain: medbrief
session: Fetched and meeting-graphed two MedBrief product walkthroughs, then wired MLX Whisper into meeting-graph plus fetch-video/diarisation skill notes
type: wrap-up
tags: [meeting-graph, fetch-video, mlx-whisper, sharepoint, diarisation, medbrief, onboarding, skill-improvement, workflow]
repos:
  - path: /Users/Rowan.Reid/.claude
    commit: c862107
  - path: /Users/Rowan.Reid/claude_code/medbrief-onboarding
    commit: f304ded
---

## Session Summary

Fetched Chantel's two MedBrief product walkthroughs from SharePoint (yt-dlp + Chrome cookies, after the M365 CLI proved a 401/404 dead end) and built two meeting-graphs (219 nodes/529 edges and 306/749) covering the full feature surface and the matter-creation flow, transcribed with MLX large-v3-turbo on the GPU. Applied three skill learnings to ~/.claude and verified them with a four-lens adversarial workflow: wired MLX into meeting-graph (transcribe.sh prefers it on Apple Silicon, preflight.sh installs it on arm64), added SharePoint fetch notes to fetch-video, and a diarisation over-clustering note; committed and pushed (5961eb3, c862107). Logged an idea to fold the two graphs into the project notes/ via /graph-to-notes, and saved a MedBrief-people memory (Dion, Anna, Chantel).
