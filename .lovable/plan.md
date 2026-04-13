

# LazyShip — "Talk about it. Ship it." 🚀

## Overview
A bold, Gen Z-targeted web app where friends chat about an idea and deploy a live landing page with one button. Dark theme with electric lime, hot pink, and cyan accents. Space Grotesk font throughout.

## Phase 1: Homepage
- **Design system**: Set up Space Grotesk font, custom colors (#0a0a0b bg, #7fff00 lime, #ff3cac pink, #00d4ff cyan), glassmorphism card styles, 20px/16px border radius
- **Nav**: "LazyShip 🚀" logo in lime + "Launch a Room" CTA button
- **Hero section**: Massive gradient text (lime→cyan) "Talk about it. Ship it. 🛸", subline, glowing "Start a Room →" button, "no sign up. no download. just vibes." tagline
- **Animated background**: Floating emoji (🚀💡🔥⚡️✨) drifting with CSS keyframes at low opacity + dot grid overlay
- **Demo section**: Animated fake chat conversation with messages appearing one-by-one with typing animation, ending with a pulsing SHIP IT button and a deployed URL
- **Feature cards**: 3 glassmorphism cards with hover glow — "💬 Just Chat", "⚡ 30 Seconds", "🔗 Share the Link"
- **Footer**: "made for people with more ideas than time 😴"

## Phase 2: Room System & Realtime Chat (Lovable Cloud)
- **Database tables**: `rooms` (id, created_at, shipped, deployed_url) and `messages` (id, room_id, sender_name, sender_emoji, content, type, created_at) with appropriate RLS
- **Room creation**: Generate random 6-char room ID, redirect to `/room/:id`
- **User setup**: Pick display name + emoji avatar from 12 options, stored in localStorage
- **Chat UI**: Full-screen dark layout, top bar with room ID + copy/share link, chat bubbles (lime for self, white/10 for others), emoji avatar + name + timestamp
- **Realtime**: Supabase Realtime subscription on messages filtered by room_id
- **Input bar**: Glassmorphism bottom bar with text input + send button
- **System messages**: Centered, muted, no bubble (join notifications, shipping status)
- **SHIP IT button**: Fixed bottom-right, gradient lime→cyan, 64px rounded-full, pulsing glow animation

## Phase 3: Ship Flow — AI Generation & Deploy
- **Edge function `generate-site`**: Fetches last 50 messages, calls Lovable AI (Gemini) to extract product info and generate a complete single-file HTML landing page with Tailwind CDN
- **Vercel deployment**: Use Vercel Deploy API to publish the generated HTML as a live site (you'll need to provide a Vercel API token)
- **Ship flow UX**: System message "🚀 Shipping in progress...", on success: confetti animation (lime+pink+cyan), system message with live URL, preview card with "Visit Site 🔗" and disabled "Edit ✏️" button
- **Error handling**: Fun error message if no product idea detected in chat
- **Room update**: After shipping, show live URL with green dot "Live" badge in top bar

