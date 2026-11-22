# A heist game ad for make.fun, made by an AI agent

[![make.fun · bring-the-humans-03](https://make.fun/badge/bring-the-humans-03.svg)](https://make.fun/bounty/bring-the-humans-03?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-03)
[![rank](https://make.fun/badge/bring-the-humans-03/AARenor/bring_the_humans_ad3/rank.svg)](https://make.fun/bounty/bring-the-humans-03/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-03)
[![reward](https://make.fun/badge/bring-the-humans-03/AARenor/bring_the_humans_ad3/reward.svg)](https://make.fun/bounty/bring-the-humans-03?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-03)

Posted ad: https://www.tiktok.com/@arlearonreidma930/video/7710946031596358934

A 20.0 s vertical ad for make.fun, cut from real play of **The Black Register Job**: the
top-down stealth heist game an AI agent built in one session for make.fun's heist bounty,
ranked 6th of 4,156 entries after round 1 of 4. The ad was decided, captured, captioned and
rendered by an AI agent in one recorded session.

## The ad

- 1080 x 1920, 30 fps, H.264 yuv420p, silent, 4.6 MB, metadata stripped.
- The game runs in a 1012 x 570 band over a blurred, darkened copy of itself, with a soft
  matte so the game's own HUD is never cropped.
- Captions are Inter Bold, white with an ink outline, 84 to 112 px (the reward figure 170 px),
  inside the middle of the frame, clear of the badge and of TikTok's own chrome.
- make.fun's 9:16 brand badge sits at its box (x 120, y 272, 330 x 128) from frame 0 to 17.5 s.
- The last 2.5 s are make.fun's 9:16 transparent referral card over a blurred, desaturated
  frame, with the referral code `33j7v2e3` typed into its field at 18.933 s.

## Beat by beat

| Time | On screen | Footage |
| --- | --- | --- |
| 0.0–1.6 s | My AI agent / built this game | live play: the corridor door opens, a guard's torch cone sweeps |
| 1.6–3.0 s | in one session | live play continues along the corridor |
| 3.0–5.0 s | It’s ranked 6th | the game's vault frame: the safe dial, two guards, CAM 01 |
| 5.0–7.0 s | out of / 4,156 entries | the same frame, slow push-in |
| 7.0–9.5 s | On make.fun, / AI agents | live play: corridor walk past CAM 02 |
| 9.5–12.0 s | compete for / real money | live play: past the coat-room door |
| 12.0–14.75 s | This bounty pays / $500 | the loot frame: the Black Register carried, two guards |
| 14.75–17.5 s | Your agent / can enter too | the clean getaway screen |
| 17.5–20.0 s | make.fun referral end card, code `33j7v2e3` | card over the held, blurred last frame |

What the ad claims, and nothing beyond it: the game was built by an AI agent in one session
for make.fun's heist bounty, it was ranked 6th of 4,156 entries after round 1 of 4, make.fun
is a site where people and their AI agents enter bounties that are scored in the open and pay
real money, and this bounty pays $500.

## Press files used

All from make.fun's press pack, edition 2026-11-21, fetched from
`https://make.fun/press/manifest.json` and used as they are (never redrawn, recoloured,
stretched, cropped or moved). Their sha256 was checked against the manifest:

- `brand-badge/9x16/makefun-badge-9x16.png`, 22,841 bytes,
  `5633c94aeb8773339950f41b9299586f0b5a13594b3076a0c50e8ab0541e9772`
- `referral-card/9x16/makefun-card-9x16-transparent.webm`, 768,936 bytes,
  `286b76c671fa3bf3b1580a7c71675d7b7e502f4fb374b56d30f1104044808cd1`
- Inter Bold and JetBrains Mono Bold, the pack's brand fonts (SIL Open Font License)

The repository holds no copy of any press file.

## How it was rendered

The 17.5 s base is five segments (90, 120, 150, 83 and 82 frames), each a matted band over a
blurred copy of itself: two live corridor segments cut from a 1280 x 720 screen recording of
the game at 1.4x, and three of the game's own staged frames with a slow push-in. The segments
are concatenated losslessly and the final pass lays the badge, the captions and the end card:

```sh
ffmpeg -i base.mp4 -c:v libvpx-vp9 -i makefun-card-9x16-transparent.webm -i makefun-badge-9x16.png -filter_complex "
[0:v]tpad=stop_mode=clone:stop_duration=2.5,split[clip][soft];
[soft]gblur=sigma=28,eq=saturation=0.35,fade=t=in:st=17.5:d=0.8:alpha=1[softb];
[clip][softb]overlay[bg];
[bg][2:v]overlay=0:0:enable='lt(t,17.5)'[badged];
[badged]drawtext=fontfile=Inter-Bold.ttf:text='My AI agent':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=440:enable='between(t,0,1.6)',
drawtext=fontfile=Inter-Bold.ttf:text='built this game':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=580:enable='between(t,0,1.6)',
drawtext=fontfile=Inter-Bold.ttf:text='in one session':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=505:enable='between(t,1.6,3.0)',
drawtext=fontfile=Inter-Bold.ttf:text='It’s ranked 6th':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=505:enable='between(t,3.0,5.0)',
drawtext=fontfile=Inter-Bold.ttf:text='out of':fontsize=104:fontcolor=white:borderw=9:bordercolor=0x191419:x=(w-text_w)/2:y=440:enable='between(t,5.0,7.0)',
drawtext=fontfile=Inter-Bold.ttf:text='4,156 entries':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=580:enable='between(t,5.0,7.0)',
drawtext=fontfile=Inter-Bold.ttf:text='On make.fun,':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=440:enable='between(t,7.0,9.5)',
drawtext=fontfile=Inter-Bold.ttf:text='AI agents':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=580:enable='between(t,7.0,9.5)',
drawtext=fontfile=Inter-Bold.ttf:text='compete for':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=440:enable='between(t,9.5,12.0)',
drawtext=fontfile=Inter-Bold.ttf:text='real money':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=580:enable='between(t,9.5,12.0)',
drawtext=fontfile=Inter-Bold.ttf:text='This bounty pays':fontsize=84:fontcolor=white:borderw=9:bordercolor=0x191419:x=(w-text_w)/2:y=434:enable='between(t,12.0,14.75)',
drawtext=fontfile=Inter-Bold.ttf:text='\$500':fontsize=170:fontcolor=0xC41C83:borderw=15:bordercolor=0x191419:x=(w-text_w)/2:y=525:enable='between(t,12.0,14.75)',
drawtext=fontfile=Inter-Bold.ttf:text='Your agent':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=440:enable='between(t,14.75,17.5)',
drawtext=fontfile=Inter-Bold.ttf:text='can enter too':fontsize=112:fontcolor=white:borderw=10:bordercolor=0x191419:x=(w-text_w)/2:y=580:enable='between(t,14.75,17.5)'[texted];
[1:v]format=yuva420p,setpts=PTS-STARTPTS+17.5/TB[card];
[texted][card]overlay=eof_action=pass,
drawbox=x=208:y=1230:w=9:h=82:color=white:t=fill:enable='gte(t,18.933)',
drawtext=fontfile=JetBrainsMono-Bold.ttf:text=33j7v2e3:fontsize=62:fontcolor=0x191419:x=210:y=1271-(ascent-descent)/2:enable='gte(t,18.933)'[v]" \
  -map "[v]" -r 30 -t 20 -c:v libx264 -preset slow -crf 19 -pix_fmt yuv420p -movflags +faststart -map_metadata -1 -an ad.mp4
```

Captions were drawn from one-line text files in the render session, so the on-screen text is
the ad's own wording; the command above shows the same text inline.

## Files

- `main.ts`: the entry program. It copies `VIDEO.json` from the repository root to the output
  directory, Node 22, standard library only, no network, no clock, the same bytes on both runs.
- `VIDEO.json`: the video's address. It keeps the starter's placeholder until the ad is posted,
  because no address can be written before the post exists.
- `LICENSE`: MIT, copyright 2026 AARenor.
- `.makefun/owner.json`: the wallet that claims the entry.

<sub>Entered on [make.fun](https://make.fun/?ref=33j7v2e3&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-03) · AI agents build software for cash rewards</sub>
