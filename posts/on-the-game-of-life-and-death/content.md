---
title: On [the game of] life (and death!)
author: Mert Gulsun
date: 2025-09-04T02:32:00.000Z
slug: on-the-game-of-life-and-death
cover: https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-the-game-of-life-and-death/images/cover-43a754ee_2648d6e5.png
og_image: https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-the-game-of-life-and-death/images/og-43a754ee_2648d6e5.png
---

I had always found it fascinating how a super tiny set of things that worked can combine into insanely beautiful structures. Take Minecraft, LEGO, or even a deck of 52 for example. They all have an extremely small group of core rules and constituents, yet they are all infinite games (and really fun too!).

Emergent phenomena, differential equations, recursive algorithms, the list goes on… Heck, even Life itself with its 118 element periodic table (and an even more limited sub-atomic particle type count) is a testament perhaps to the brilliant insight by John Gall:

*“A complex system that works is invariably found to have evolved from a simple system that worked. A complex system designed from scratch never works and cannot be patched up to make it work. You have to start over with a working simple system.” — Systemantics (1975)
*

If Gall is right, the safest way to build something real is to start with a small system and let it run. The cleanest one I know is Conway’s Game of Life.

It runs on a grid. Each square is either alive or dead. Time advances in steps. At each step every square updates at once using the same local rules:

- A live square stays alive if it has two or three live neighbors.- A dead square becomes alive if it has exactly three live neighbors.- Otherwise it is dead on the next step.

That is the whole rulebook. You pick a small starting pattern, press play, and watch it evolve. Sometimes the pattern freezes. Sometimes it pulses. Sometimes it sends little shapes drifting across the board. You never touch the board after you start. The only choice you make is the seed.

<figure>![image](https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-the-game-of-life-and-death/images/image-2828d6e5-95bca5a2_2828d6e5.png)</figure>
Watch long enough and your attention shifts forward. You stop looking at the next frame and start thinking five or ten frames out. You learn to shape contact instead of reacting to it. You learn that a small change now can decide a collision later. That habit is the real lesson.

<figure>![image](https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-the-game-of-life-and-death/images/image-2828d6e5-6ae7fa61_2828d6e5.png)</figure>
I wanted to take that habit and add pressure. Could you keep the feel of Life, but give the player reasons to act and a clock that will not wait? That is what became my little game project **Seed to Void**.

You control a green colony. Red threats appear near you and try to wipe you out. When red and green touch, the larger cluster flips the smaller. You survive as long as at least one green cell remains. You do not paint cells by hand. You stamp small patterns from a dock, then you let the world run. Each stamp is a bet on what the board will look like a few beats from now.

<figure>![image](https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-the-game-of-life-and-death/images/image-2708d6e5-d2ecc0fd_2708d6e5.png)</figure>
The actions (the patterns you can place on the board) are intentionally small. A block plugs a leak. A blinker trims noise. A glider projects force across a lane. Because each pattern has a cooldown, you cannot lean on one trick. Cooldowns also respect time in a way that keeps the game honest. If you pause, they freeze. If you speed the sim to clean up stragglers, real time cooldown shortens so the tempo still feels right.

Tension comes from three simple levers. Scarcity, randomness, and irreversibility. Scarcity is the cooldowns. Randomness is a spawner that drops threats close enough to matter. Irreversibility is the rule that once the world runs, you do not edit cells by hand. As you survive, an internal level rises. That level increases spawn rate and the cap on simultaneous threats. You can feel the tide coming in. The satisfying runs are the ones where you stay one beat ahead of that tide.

<figure>![image](https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-the-game-of-life-and-death/images/image-2708d6e5-30c34d93_2708d6e5.png)</figure>
Most of the strategy lives at the point of contact. When two fronts meet, the bigger side flips the smaller. That sounds obvious. In play it rewards shape and timing. You can split a big red blob into two smaller pieces, then flip them one by one. You can bait a collision so your green wave arrives slightly larger at the exact place where it matters. Long runs usually trace back to one or two such choices made ten seconds earlier.

Under the hood it stays small on purpose. The client is React with Vite, rendering to Canvas 2D. A single store, built with Zustand, owns the loop, the spawner, and the cooldowns. One step computes the next grid, applies the conversion rule, updates stats, and checks defeat. The grid renderer uses a resize observer and pixel aligned cell sizes so lines look crisp, and it only draws borders when they help at a given zoom. The server is Express. In development it runs Vite as middleware. In production it serves the static client and a tiny API. High scores live in memory by default, which is fine for local play. If you want leaderboards, switch to Postgres through Drizzle ORM and set `DATABASE_URL`. The API is two routes, get the top ten for a difficulty and post a score. Validation is shared so the client and server agree on shape.

Check out the repo at: [https://github.com/setrf/seedtovoid](https://github.com/setrf/seedtovoid)

`npm run dev` starts a local build with the API under `/api`. `npm run build` then `npm start` serves a production bundle. Turn on Postgres if you want persistent leaderboards. 

Details like these do not make the idea, but they decide the feel. If pause is not real pause, players sense it. If speed ignores cooldowns, the rhythm breaks. If the dock hides or the grid sits under the HUD, the phone feels cramped. The game is a set of small promises kept, which is how you preserve the calm center of Life while adding pressure around it.

What surprised me most is that the threats did not drown the original charm. They gave it a reason. The thing that still decides a run is the tiny rulebook. You win by knowing where a glider will be a few steps from now. You win by knowing when a stabilizer will save space and when it will create noise. You win by leaving yourself a place to stamp again two beats later.

<figure>![image](https://raw.githubusercontent.com/setrf/blog-assets/main/posts/on-the-game-of-life-and-death/images/image-2828d6e5-4d4c5c91_2828d6e5.png)</figure>
If you want to see the point rather than read about it, play a few runs at [seedtovoid.com](http://seedtovoid.com/) or [https://apps.apple.com/us/app/game-of-life-survival/id6752623085](https://apps.apple.com/us/app/game-of-life-survival/id6752623085)

Start on an easier setting and stamp less than you think you should. Treat patterns like tools, not bombs. Try to make contact on your terms. When you lose, rewind the last ten seconds in your head and you will usually see the exact stamp that set the ending in motion.

Plant something small, then watch what it becomes. Sometimes you carve a highway of green. Sometimes you fall into the void. Either way you learn what simple rules can do, which is the same lesson Gall was pointing at when he said to start with a small system that works and let it teach you.