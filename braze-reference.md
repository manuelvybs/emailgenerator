# braze-reference.md
# VYBS × Braze — Master Reference for Claude

This file is the single source of truth for generating Braze-compatible HTML emails,
Content Blocks with Liquid, and performance analysis for VYBS.
Always follow VYBS brand rules AND Braze technical constraints simultaneously.

---

## 1. VYBS BRAND IDENTITY

### Voice & Tone
- Direct, warm, slightly dry. No hype, no fluff.
- References: Donald Glover, Steph Curry, Tyler the Creator
- Tagline: "Play More. Earn Real."
- Audience split: Players (earn rewards) | Game Studios (grow reach)

### Color Palette
```
PRIMARY
  Blue:         #6F7EFF
  Blue shadow:  #434EF0
  Gold/Yellow:  #FFCA00

SECONDARY
  Green:        #3CD98A
  Green shadow: #2AB36E
  Light blue:   #EAECFF   ← card backgrounds, subtle surfaces

ACCENTS
  Teal:         #3EDEEC   ← info, highlights
  Peach/Coral:  #F7986E   ← warm promos, urgency
  Pink:         #F173A6   ← events, limited-time, special drops
  Gray:         #5C5C5C   ← neutral, secondary text, dividers

LOGO / BACKGROUND / TEXT
  White:        #FFFFFF
  Black:        #000000
```

### Typography (email fallback stack)
```css
font-family: 'Inter', 'Helvetica Neue', Arial, sans-serif;
```

### Common Pairings
- Hero / CTA primary: Blue #6F7EFF bg + White text + Gold #FFCA00 button
- Success / reward confirmed: Green #3CD98A
- Promo / urgency: Peach #F7986E or Pink #F173A6
- Neutral card: Light blue #EAECFF bg + Black text
- Dark theme: Black #000000 bg + White text + Blue #6F7EFF accents

### Naming Convention (Campaigns & Canvases)
```
[Type] | [Audience/Trigger] | [Goal] | [YYYY-MM-DD]

Examples:
  Email | New Registrations | First Earn | 2025-03-01
  Canvas | Inactive 7d | Re-engagement | 2025-04-15
  Email | All Players | Weekly Digest | 2025-05-01
```

---

## 2. BRAZE HTML EMAIL — RULES & CONSTRAINTS

### Non-negotiable technical rules
```
✅ Use INLINE CSS only — no <style> blocks in email body
✅ Max width: 500px (works for both mobile + desktop)
✅ Use nested <table> for layout — NOT <div> tags
✅ Images: PNG, JPEG, or GIF only. Max 5 MB each.
✅ No JavaScript (ignored by all email clients)
✅ No SVG or WebP (poor client support)
✅ No fixed heights/widths on images (causes whitespace issues)
✅ Liquid must go inside <body> only — not in <head>
✅ Always include a plain text version (lowers spam score)
✅ Use straight quotes ' ' in Liquid — never curly quotes ' '
```

### HTML Email Base Structure
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{{campaign.${name}}}</title>
</head>
<body style="margin: 0; padding: 0; background-color: #000000; font-family: 'Inter', 'Helvetica Neue', Arial, sans-serif;">

  <!-- Outer wrapper -->
  <table width="100%" cellpadding="0" cellspacing="0" border="0">
    <tr>
      <td align="center" style="padding: 20px 0;">

        <!-- Email container — max 500px -->
        <table width="500" cellpadding="0" cellspacing="0" border="0"
               style="max-width: 500px; width: 100%; background-color: #FFFFFF;">

          <!-- HEADER BLOCK -->
          <tr>
            <td style="background-color: #6F7EFF; padding: 24px; text-align: center;">
              <img src="{{logo_url}}" alt="VYBS" width="120" style="display: block; margin: 0 auto;">
            </td>
          </tr>

          <!-- HERO / BODY BLOCK -->
          <tr>
            <td style="padding: 32px 24px; background-color: #000000; color: #FFFFFF;">
              <!-- Content goes here -->
            </td>
          </tr>

          <!-- CTA BLOCK -->
          <tr>
            <td style="padding: 0 24px 32px; background-color: #000000; text-align: center;">
              <table cellpadding="0" cellspacing="0" border="0" style="margin: 0 auto;">
                <tr>
                  <td style="background-color: #FFCA00; border-radius: 6px;">
                    <a href="{{cta_url}}" style="display: inline-block; padding: 14px 32px;
                       color: #000000; font-weight: bold; font-size: 16px;
                       text-decoration: none; font-family: 'Inter', Arial, sans-serif;">
                      {{cta_text}}
                    </a>
                  </td>
                </tr>
              </table>
            </td>
          </tr>

          <!-- FOOTER BLOCK -->
          <tr>
            <td style="background-color: #000000; padding: 20px 24px;
                       text-align: center; color: #5C5C5C; font-size: 12px;">
              <p style="margin: 0 0 8px;">VYBS — Play More. Earn Real.</p>
              <p style="margin: 0;">
                <a href="{{${set_user_to_unsubscribed_url}}}"
                   style="color: #5C5C5C; text-decoration: underline;">Unsubscribe</a>
                &nbsp;|&nbsp;
                <a href="{{${email_settings_url}}}"
                   style="color: #5C5C5C; text-decoration: underline;">Email Preferences</a>
              </p>
            </td>
          </tr>

        </table>
      </td>
    </tr>
  </table>

</body>
</html>
```

### Forbidden HTML tags (Braze blocks these)
```
<script>, <iframe>, <form>, <input>, <object>, <embed>
<meta http-equiv>, <base>, <link rel="stylesheet">
event handlers: onload, onclick, onmouseover, etc. in HTML attributes
```

---

## 3. LIQUID — SYNTAX & RULES

### Core syntax rules
```
{{ variable }}          → outputs a value
{% tag %}               → logic (if, for, assign, capture)
{{ var | filter }}      → apply a filter to a value
Always use straight quotes: 'value'  NOT 'value' or "value"
Every {% if %} needs {% endif %}
Every {% for %} needs {% endfor %}
Liquid must be outside HTML comments <!-- -->
```

### Standard user attributes
```liquid
{{${first_name}}}             → user's first name
{{${last_name}}}              → user's last name
{{${email_address}}}          → user's email
{{${city}}}                   → user's city
{{${country}}}                → user's country
{{${language}}}               → user's language code (e.g. "en")
{{${most_recent_location}}}   → last known location
{{${user_id}}}                → Braze external user ID
{{${braze_id}}}               → Braze internal ID
```

### Always use default fallbacks
```liquid
<!-- CORRECT — always include | default -->
{{${first_name} | default: 'Player'}}
{{${city} | default: 'your city'}}

<!-- WRONG — blank in message if attribute missing -->
{{${first_name}}}
```

### Custom attributes
```liquid
{{custom_attribute.${reward_points} | default: 0}}
{{custom_attribute.${vip_status} | default: 'standard'}}
{{custom_attribute.${last_game_played} | default: 'a game'}}
{{custom_attribute.${games_played_count} | default: 0}}
{{custom_attribute.${total_earned_usd} | default: '0.00'}}
```

### Conditional logic (if / elsif / else / endif)
```liquid
{% if custom_attribute.${vip_status} == 'VIP' %}
  You're a VIP — exclusive rewards are waiting.
{% elsif custom_attribute.${vip_status} == 'new' %}
  Welcome! Your first reward is ready to claim.
{% else %}
  Keep playing to unlock more rewards.
{% endif %}
```

### Conditional with blank check
```liquid
{% if ${first_name} blank %}
  Hey there,
{% else %}
  Hey {{${first_name}}},
{% endif %}
```

### Abort message (don't send if condition not met)
```liquid
{% if custom_attribute.${reward_points} == 0 %}
  {% abort_message('User has no reward points') %}
{% endif %}
```

### Assign a variable
```liquid
{% assign display_name = ${first_name} | default: 'Player' %}
Hi {{display_name}}, here's your update.
```

### Capture (multi-line assign)
```liquid
{% capture reward_message %}
  You've earned {{custom_attribute.${reward_points} | default: 0}} points this week.
{% endcapture %}
{{reward_message | strip}}
```
Note: Use `| strip` after capture to remove whitespace/line breaks.

### For loops (iterating arrays)
```liquid
{% for game in custom_attribute.${recent_games} %}
  {{game}}{% unless forloop.last %}, {% endunless %}
{% endfor %}
```

### Date filters
```liquid
{{'now' | date: '%B %d, %Y'}}        → "March 01, 2025"
{{'now' | date: '%A'}}               → "Saturday"
{{${date_of_birth} | date: '%B %d'}} → "July 04"
```

### String filters
```liquid
{{${first_name} | upcase}}           → "MANUEL"
{{${first_name} | downcase}}         → "manuel"
{{${first_name} | capitalize}}       → "Manuel"
{{'hello world' | replace: 'world', 'VYBS'}} → "hello VYBS"
{{custom_attribute.${bio} | truncate: 100}}  → first 100 chars
```

### Math filters
```liquid
{{custom_attribute.${reward_points} | plus: 50}}
{{custom_attribute.${reward_points} | minus: 10}}
{{custom_attribute.${reward_points} | times: 2}}
{{custom_attribute.${total_earned} | round: 2}}
```

### Canvas / Campaign attributes in Liquid
```liquid
{{campaign.${name}}}               → campaign name
{{campaign.${message_name}}}       → message variant name
{{canvas.${name}}}                 → canvas name
{{canvas.${variation_name}}}       → canvas variation
```

### API-triggered properties
```liquid
{{api_trigger_properties.${promo_code}}}
{{api_trigger_properties.${reward_amount}}}
```

### Connected Content (pull from external API)
```liquid
{% connected_content https://api.vybs.co/user/{{${user_id}}}/rewards
   :save user_rewards %}
You have {{user_rewards.points}} points available.
```

---

## 4. CONTENT BLOCKS

### How Content Blocks work in Braze
- Created in: Templates > Content Blocks
- Two types: HTML Content Block | Drag-and-drop Content Block
- Don't mix types — HTML blocks in DnD editors cause rendering issues
- Content Blocks update live in all messages that reference them via Liquid
- Size limit: 5 MB per block

### Reference a Content Block via Liquid
```liquid
{{content_blocks.${block_name}}}
```
Example:
```liquid
{{content_blocks.${vybs_header}}}
{{content_blocks.${vybs_footer}}}
{{content_blocks.${reward_points_banner}}}
```

### Whitespace fix for Content Blocks
When a Content Block includes line breaks that cause rendering issues:
```liquid
{% capture clean_block %}{{content_blocks.${block_name}}}{% endcapture %}
{{clean_block | strip}}
```

### Recommended VYBS Content Blocks to build
```
vybs_header          → Logo + nav bar (blue #6F7EFF bg)
vybs_footer          → Unsubscribe + legal + social links
vybs_reward_banner   → "You've earned X" dynamic banner
vybs_cta_gold        → Standard gold CTA button
vybs_cta_blue        → Blue CTA button variant
vybs_divider         → Thin gold rule divider
vybs_game_card       → Single game promo card (image + title + CTA)
```

---

## 5. UNSUBSCRIBE & COMPLIANCE (required)

### Always include in every email footer
```liquid
<!-- Required unsubscribe link -->
<a href="{{${set_user_to_unsubscribed_url}}}">Unsubscribe</a>

<!-- Optional: email preferences center -->
<a href="{{${email_settings_url}}}">Email Preferences</a>
```

### One-click list-unsubscribe
Configured in Braze dashboard under Sending Settings per campaign/Canvas.
Options: workspace default | unsubscribe globally | unsubscribe from specific group.

### Subscription group check (don't send to unsubscribed users)
```liquid
{% if ${email_unsubscribed} == true %}
  {% abort_message('User is unsubscribed') %}
{% endif %}
```

---

## 6. EMAIL PERFORMANCE — BENCHMARKS & METRICS

### Industry benchmarks (gaming / rewards vertical)
```
Open rate:          20–30%  (good), 30%+ (excellent)
Click-through rate: 2–5%    (good), 5%+ (excellent)
Click-to-open rate: 10–20%  (good)
Unsubscribe rate:   <0.5%   (healthy), >1% (investigate)
Bounce rate:        <2%     (healthy), >5% (deliverability risk)
Spam complaint:     <0.08%  (safe), >0.1% (critical — fix immediately)
```

### Braze email analytics glossary
```
Sends              → total messages sent
Deliveries         → sends minus bounces
Unique Opens       → first open per user
Total Opens        → includes repeated opens (inflated by MPP)
Unique Clicks      → first click per user per link
Total Clicks       → all clicks including repeat
Click-to-Open (CTOR) → unique clicks / unique opens
Revenue            → attributed purchase value post-click
Unsubscribes       → users who clicked unsubscribe link
Hard Bounce        → permanent delivery failure (bad address)
Soft Bounce        → temporary failure (mailbox full, server down)
Spam Reports       → user marked as spam (critical signal)
```

### Apple Mail Privacy Protection (MPP) note
MPP pre-fetches open tracking pixels, inflating open rates.
Use Click-to-Open Rate (CTOR) and click data as more reliable engagement signals.
Segment: `{{${email_open_tracking_pixel}}}` is unreliable for Apple Mail users.

### Analysis prompts for Claude
When analyzing Braze performance data, always:
1. Compare against the benchmarks table above
2. Flag anything above healthy thresholds (bounce, spam, unsub)
3. Identify top-performing subject lines + send times
4. Segment analysis: new vs returning, VIP vs standard
5. Recommend A/B test hypotheses based on gaps

---

## 7. CANVAS BEST PRACTICES

### Canvas naming convention
```
[Type] | [Audience/Trigger] | [Goal] | [YYYY-MM-DD]

Types: Onboarding | Re-engagement | Transactional | Promotional | Lifecycle
```

### One-sentence Canvas description format
```
[Trigger condition] → [journey summary] → [primary goal]

Example:
"Triggered when user registers → 5-step onboarding sequence over 7 days → first reward claim."
"Triggered when user inactive 7d → 3-email re-engagement flow → return to app + earn."
```

### Canvas step delay best practices
```
Day 0:  Welcome / confirmation (immediate)
Day 1:  First value delivery (what can they earn?)
Day 3:  Activation nudge (have they earned yet?)
Day 7:  Social proof / FOMO (others are earning)
Day 14: Escalate or exit (win-back or suppress)
```

---

## 8. SEGMENTATION — COMMON LIQUID FILTERS FOR VYBS

```liquid
<!-- High-value users -->
{% if custom_attribute.${reward_points} >= 1000 %}

<!-- Inactive users (no session in 7+ days — use Braze segment, not Liquid) -->

<!-- New users (registered < 7 days ago) -->
{% assign days_since_signup = 'now' | date: '%s' | minus: ${date_of_first_session} | date: '%s' | divided_by: 86400 %}
{% if days_since_signup <= 7 %}

<!-- Has earned at least once -->
{% if custom_attribute.${total_earned_usd} > 0 %}

<!-- Never earned -->
{% if custom_attribute.${total_earned_usd} == 0 or custom_attribute.${total_earned_usd} blank %}
```

---

## 9. QUICK REFERENCE — COMMON PATTERNS

### Personalized subject line
```
Hey {{${first_name} | default: 'Gamer'}}, your rewards are waiting 🎮
```

### Dynamic reward points in body
```liquid
You have <strong>{{custom_attribute.${reward_points} | default: 0}} points</strong>
— enough to redeem for a ${{custom_attribute.${reward_points} | divided_by: 100 | floor}} gift card.
```

### Conditional CTA based on user status
```liquid
{% if custom_attribute.${vip_status} == 'VIP' %}
  <a href="https://vybs.co/vip-rewards">Claim VIP Rewards →</a>
{% else %}
  <a href="https://vybs.co/rewards">Start Earning →</a>
{% endif %}
```

### Dynamic game recommendation
```liquid
{% if custom_attribute.${last_game_played} blank %}
  Check out today's top games on VYBS.
{% else %}
  Continue where you left off in {{custom_attribute.${last_game_played}}}.
{% endif %}
```

### Birthday / anniversary message
```liquid
{% assign bday_month = ${date_of_birth} | date: '%m' %}
{% assign current_month = 'now' | date: '%m' %}
{% if bday_month == current_month %}
  Happy birthday month, {{${first_name} | default: 'Player'}}! 🎂 Here's a bonus.
{% endif %}
```

---

## 10. THINGS TO NEVER DO IN BRAZE EMAIL

```
❌ Never put <style> blocks in the email body
❌ Never use <div> for layout — use <table>
❌ Never use JavaScript
❌ Never use SVG or WebP images
❌ Never hardcode heights/widths on images
❌ Never use curly quotes in Liquid: ' ' " "  → use straight: ' "
❌ Never leave Liquid variables without | default fallback
❌ Never put Liquid inside HTML comments <!-- -->
❌ Never use HTML Content Blocks inside Drag-and-Drop editor (and vice versa)
❌ Never forget {% endif %} or {% endfor %} — will break rendering
❌ Never omit the unsubscribe link — required by law (CAN-SPAM, GDPR)
```

---

*Last updated: 2025 | VYBS platform | For use in Claude Project: Braze Email System*
