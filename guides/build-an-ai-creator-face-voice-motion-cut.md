[← Back to the guide directory](../README.md)

# Build an AI Creator: Face, Voice, Motion, Cut

This is the complete four-part workflow behind a fictional presenter who can appear consistently across short-form videos without a camera shoot for every post.

```text
FACE → VOICE → MOTION → CUT
```

Use Midjourney or Higgsfield for the character, ElevenLabs for the voice, Kling or Runway for the performance, and Claude Code with FFmpeg for the final assembly.

> **Last verified:** 30 August 2026
>
> **Important:** Build a fictional character or use a real person's face and voice only with clear permission. Do not imitate a public figure, customer, employee, or creator without authorization. Disclose realistic AI-generated media when you publish it.

## What you will make

By the end, you will have:

- one approved master image that defines the presenter;
- one saved voice preset or authorized voice clone;
- several short, lip-synced presenter clips;
- captions and a repeatable FFmpeg edit; and
- a small character bible so the next video looks and sounds like the same creator.

The tools are interchangeable. The reusable assets—the character bible, master image, voice preset, and editing rules—are the real system.

## Before you generate anything

Create a folder for the project:

```text
ai-creator/
├── 01-character/
├── 02-voice/
├── 03-motion/
├── 04-edit/
├── exports/
└── CHARACTER-BIBLE.md
```

Put these rules at the top of `CHARACTER-BIBLE.md`:

```markdown
# Character bible

Name:
Role and audience:
Age range:
Face and hair:
Wardrobe:
Voice and accent:
Energy and speaking pace:
Default framing:
Default background:
Never change:
AI disclosure text:
```

Keep the character distinctive without asking the model to copy a real person. Record where every reference image, voice sample, font, music track, and stock asset came from.

## 1. Face — create one master reference

Choose **Midjourney** if you want broad art direction and fast visual exploration. Choose **Higgsfield** if you want its creator-focused presets and reusable Soul ID workflow.

Start with a clean presenter portrait. This prompt is a useful baseline:

```text
Photorealistic fictional technology creator, late 20s, warm and trustworthy,
distinctive shoulder-length dark hair, charcoal overshirt over a plain cream tee,
standing in a minimal modern studio, soft daylight, realistic skin texture,
looking directly into camera, relaxed confident expression, waist-up framing,
both shoulders and hands visible, centered composition, vertical 9:16,
natural commercial photography, no text, no logos
```

Change the identity, wardrobe, setting, and mood to fit your channel. Keep the structural details—front-facing, well lit, clearly visible face, simple background, and the intended aspect ratio.

### Midjourney route

1. Generate variations until one face, hairstyle, and wardrobe feel right.
2. Save the strongest result as `01-character/master-reference.png`.
3. Generate a small reference sheet: front-facing neutral, front-facing smiling, three-quarter view, and waist-up with hands visible.
4. Reuse the same master reference for future scenes.

Midjourney V7 uses **Omni Reference** for recurring people or objects. Add the master image to the Omni Reference slot and pair it with a clear text prompt. Midjourney's current documentation directs V8.x users to its Edit Model instead, so check the active model before following a version-specific control.

### Higgsfield route

1. Open **Image → Soul 2.0**.
2. Create or select a Soul ID character.
3. Generate the approved master portrait and a small set of expressions.
4. Reuse that Soul ID inside the same model family.

Higgsfield notes that Soul IDs are model-specific. A character created for Soul 2.0 is not automatically available in Soul or Soul Cinema, so choose one primary model and keep it consistent.

### Face approval checklist

- [ ] It is a fictional identity or you have written permission to use the likeness.
- [ ] The face is clear at phone-screen size.
- [ ] Eyes, teeth, fingers, earrings, and clothing details survive close inspection.
- [ ] The portrait has enough space for captions.
- [ ] The same master image is saved locally instead of relying on generation history.
- [ ] The character bible describes the details that must not drift.

Do not move on until one image is the approved source of truth. Generating each episode from a fresh text prompt is the fastest way to create a different person every time.

## 2. Voice — save one repeatable preset

ElevenLabs gives you three sensible routes:

1. **Voice Design** — create a new synthetic voice from a description.
2. **Voice Library** — select a voice whose permitted use fits the project.
3. **Voice Clone** — clone your own voice or another voice only where the product allows it and you have the required rights and consent.

For a fictional creator, Voice Design is the cleanest starting point. Try:

```text
A warm British technology creator in their late twenties. Clear, conversational
delivery with understated confidence, medium pace, crisp articulation, and a
slight smile. Helpful rather than promotional. Natural pauses between steps.
```

Generate several previews, choose one, and save it with a stable name such as `AI Creator — warm UK v1`.

If you use ElevenLabs Instant Voice Cloning, its current guidance recommends roughly one to two minutes of clean, consistent speech without background noise or reverb. The dashboard requires you to confirm that you have the right and consent to clone the voice. Professional Voice Cloning is designed for the account owner's own verified voice; someone else must create and verify their own professional clone before sharing it with you.

### Prepare each script for speech

Write for the ear:

- one idea per sentence;
- contractions instead of formal phrasing;
- short paragraphs for natural pauses;
- phonetic spelling for unusual product names; and
- no URLs, emoji, or visual formatting in the spoken copy.

Export a clean voiceover to `02-voice/voiceover.wav` or `voiceover.mp3`. Listen once without looking at the script. Fix pronunciation and pacing before generating video—every motion retry costs more time and credits.

### Voice approval checklist

- [ ] The voice is synthetic, licensed, your own, or explicitly authorized.
- [ ] The pace and energy match the character bible.
- [ ] Product names are pronounced correctly.
- [ ] There is no clipped audio, background noise, or accidental room tone.
- [ ] The final voiceover file and exact script are saved together.

## 3. Motion — animate the image with the voice

For a talking presenter, use a character-performance or avatar workflow rather than generic image-to-video. Generic image-to-video is useful for visual shots, but it does not automatically guarantee accurate speech synchronization.

### Kling route: Avatar 2.0

Kling Avatar 2.0 accepts a character image, a voiceover, and performance direction.

1. Upload `master-reference.png`.
2. Add the approved voiceover.
3. Describe the expression, gestures, and camera behavior.
4. Generate one short section at a time and inspect the face and hands.

Performance prompt:

```text
The presenter speaks directly to camera with calm confidence. Natural blinking,
subtle head movement, relaxed shoulders, and small open-hand gestures on the key
points. Friendly expression with a slight smile. Locked camera, no zoom, no cuts,
soft studio background motion only.
```

Kling's separate Lip Sync tool is designed for supported character videos that already exist. For a still image plus a voiceover, use the Avatar workflow.

### Runway route: Character Script to Video

Runway's **Character Script to Video** app accepts a character image plus either typed dialogue and a selected voice or your own uploaded audio file.

1. Open **Apps → Character Script to Video**.
2. Upload the approved master image.
3. Switch the script input to **Audio** and add the ElevenLabs voiceover.
4. Generate and review the synced performance.

For more deliberate body movement, use **Act-Two**. It needs a driving performance video as well as the character image or video. The driving clip supplies the movement, expression, gestures, speech, and audio; it is not a still-image-plus-audio shortcut.

### Generate in short sections

Split a 30-second script into three to six clips at sentence boundaries. Short clips are easier to regenerate when one word, blink, hand, or facial detail fails.

Use this shot manifest:

| Clip | Dialogue | Framing | Gesture | Status |
|---|---|---|---|---|
| 01-hook | Opening line | Tight waist-up | Still, direct eye contact | Draft |
| 02-step | First explanation | Medium waist-up | One small hand gesture | Draft |
| 03-payoff | Result | Tight waist-up | Slight smile | Draft |
| 04-cta | Call to action | Tight waist-up | Open palm | Draft |

Save approved clips as `03-motion/clip-01.mp4`, `clip-02.mp4`, and so on. Do not overwrite failed generations; the comparison helps you identify which prompt change worked.

### Motion approval checklist

- [ ] Lip movement matches consonants and sentence endings.
- [ ] Eye direction remains stable.
- [ ] The face, hair, wardrobe, and background do not morph.
- [ ] Hands do not merge, multiply, or cross the face.
- [ ] The camera does not drift unless the shot calls for it.
- [ ] Every spoken claim matches the approved script.

## 4. Cut — assemble with Claude Code and FFmpeg

Claude Code can inspect the asset folder, write a repeatable edit script, run FFmpeg, and verify the export. Keep it supervised: ask for a plan first, preserve the original files, and inspect the final result yourself.

Start Claude Code inside the project folder and use this prompt:

```text
Build a repeatable vertical-video edit from the assets in this folder.

Requirements:
- Inspect the media with ffprobe before proposing the edit.
- Do not overwrite or rename source files.
- Show me the proposed clip order and durations before editing.
- Normalize approved clips to 1080x1920, 30 fps, H.264 video, AAC audio.
- Join them in numerical order.
- Burn in captions from 04-edit/captions.srt with generous mobile-safe margins.
- Keep dialogue clear; do not add music unless a licensed track is present.
- Write the commands to 04-edit/assemble.sh so the export is reproducible.
- Export to exports/ai-creator-final.mp4.
- Verify resolution, duration, frame rate, codecs, and audio after rendering.
- Stop and report any missing input, unsupported filter, or sync problem.
```

Review the proposed plan before allowing the commands to run.

### FFmpeg building blocks

First normalize each approved clip. Change the input and output names for each file:

```bash
ffmpeg -i 03-motion/clip-01.mp4 \
  -vf "scale=1080:1920:force_original_aspect_ratio=decrease,pad=1080:1920:(ow-iw)/2:(oh-ih)/2:black,fps=30" \
  -c:v libx264 -preset medium -crf 18 -pix_fmt yuv420p \
  -c:a aac -b:a 192k -ar 48000 \
  04-edit/clip-01-normalized.mp4
```

Create `04-edit/concat.txt`:

```text
file 'clip-01-normalized.mp4'
file 'clip-02-normalized.mp4'
file 'clip-03-normalized.mp4'
file 'clip-04-normalized.mp4'
```

Join the matching normalized files without another encode:

```bash
ffmpeg -f concat -safe 0 -i 04-edit/concat.txt -c copy 04-edit/joined.mp4
```

Burn in SRT captions and create the delivery export:

```bash
ffmpeg -i 04-edit/joined.mp4 \
  -vf "subtitles=04-edit/captions.srt:force_style='Alignment=2,MarginV=180,FontSize=18,Outline=3'" \
  -c:v libx264 -preset medium -crf 18 -pix_fmt yuv420p \
  -c:a copy -movflags +faststart \
  exports/ai-creator-final.mp4
```

The concat demuxer expects compatible streams, which is why the clips are normalized first. FFmpeg builds differ; if the `subtitles` filter is unavailable, install a build with libass support or export captions as a separate track from your editor.

Verify the output:

```bash
ffprobe -v error \
  -show_entries format=duration:stream=index,codec_name,codec_type,width,height,r_frame_rate \
  -of default=noprint_wrappers=1 \
  exports/ai-creator-final.mp4
```

## Final quality-control pass

Watch the export three times:

1. **Muted** — check the hook, face consistency, framing, captions, and visual glitches.
2. **Eyes closed** — check pacing, pronunciation, noise, levels, and hard audio cuts.
3. **Normally on a phone** — check whether the presenter feels coherent at real viewing size.

Then confirm:

- [ ] The presenter is fictional or fully authorized.
- [ ] The voice is licensed or consented.
- [ ] The first frame makes sense before audio starts.
- [ ] Captions match the spoken words and stay inside mobile-safe areas.
- [ ] No generation contains extra fingers, changing teeth, warped logos, or unreadable text.
- [ ] Music, fonts, footage, and images have recorded sources and usable licences.
- [ ] The caption says the presenter or media is AI-generated.
- [ ] The platform's AI-content label is enabled where available or required.
- [ ] A human has approved the exact final video and caption.

TikTok currently requires creators to label realistic AI-generated images, audio, and video. Meta also uses AI-content transparency measures across Facebook and Instagram. Platform controls and regional rules change, so check the current upload screen and policy before each campaign.

Suggested disclosure:

```text
This presenter and parts of this video were generated with AI.
```

## Make the next episode faster

Do not rebuild the identity every time. Reuse:

- the same master image or character ID;
- the same voice preset and settings;
- the same default framing and background;
- the same performance prompt;
- the same caption style; and
- the same verified FFmpeg script.

Only the script, expressions, gestures, and supporting visuals should need to change. Version intentional changes in the character bible instead of allowing gradual drift.

## Official sources

- [Midjourney Omni Reference](https://docs.midjourney.com/hc/en-us/articles/36285124473997-Omni-Reference)
- [Higgsfield Soul image workflow](https://higgsfield.ai/creator-hub/help-center/ai-models/how-do-i-use-soul-to-generate-images)
- [ElevenLabs Voice Design](https://elevenlabs.io/docs/eleven-creative/voices/voice-design/)
- [ElevenLabs Instant Voice Cloning](https://elevenlabs.io/docs/eleven-creative/voices/voice-cloning/instant-voice-cloning)
- [Kling Avatar 2.0](https://kling.ai/quickstart/kling-ai-avatar-2-user-guide)
- [Kling Lip Sync](https://kling.ai/quickstart/ai-lip-sync-guide)
- [Runway Character Script to Video](https://help.runwayml.com/hc/en-us/articles/51285026291219-Character-Script-to-Video)
- [Runway Act-Two performance capture](https://help.runwayml.com/hc/en-us/articles/42311337895827-Performance-Capture-with-Act-Two)
- [Claude Code setup](https://docs.anthropic.com/en/docs/claude-code/getting-started)
- [FFmpeg documentation](https://ffmpeg.org/ffmpeg.html)
- [TikTok AI-generated content guidance](https://support.tiktok.com/en/using-tiktok/creating-videos/ai-generated-content)
- [Meta's AI-generated content transparency update](https://about.fb.com/news/2026/07/meta-is-signing-the-eu-ai-act-code-of-practice-on-transparency-of-ai-generated-content/)

---

If this guide helped, star the repository and share it with another creator.

Created by [Grayson Ho](https://github.com/graysonhyc).
