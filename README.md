# Mevisto Countdown (docs)
This public repository hosts documentation, screenshots and support links
for the Mevisto Countdown package for Umbraco.  
For issues and questions, see below.

- Install on NuGet: https://www.nuget.org/packages/Mevisto.Countdown/
- Documentation: (this page)
- Issues / Support: mailto:goddag@mevisto.se
- 
# Mevisto Countdown for Umbraco 16

A production-ready, lightweight **countdown banner** for Umbraco 16 (.NET 9).  
Shows a campaign bar at the top of the page with a live timer, CTA, per-device behavior, colors/gradients, and optional dismiss with persistence.
It can also be used without the countdown, for just showing a message at the top of the website.
- Ships as a **Razor Class Library (RCL)** — install, add the ViewComponent call, done.

---

## ✨ Features

- Sticky or non-sticky (with **mobile override**)
- Separate **desktop and mobile text** (mobile can be compact)
- **Compact mobile CTA**
- Background: solid color or **preset gradients** + custom **text color**
- CTA colors with automatic hover contrast
- Optional **dismiss (×)** with **persistence days**
- **No-countdown mode** (message/CTA only)
- Plays nicely with a **sticky header** (auto offset via CSS variable)

---

## 🚀 Quick start

1) **Install NuGet**
```bash
dotnet add package Mevisto.Countdown
```

2) **Composition**  
On application start, the package ensures the composition **“Mevisto Urgency”** and all fields (idempotent).  
Add the composition to your **home/root document type**.

3) **Render the banner**  
Place the ViewComponent near the top of your layout (before header/nav):
```csharp
@await Component.InvokeAsync("MevistoCountdown")
```
This ensures the banner sits above your header and can push it down when sticky.

> **Important:** `Valid from` and `Valid to` use **Date Picker with time**.  
> Editors must select **both date and time** for Umbraco’s editor to treat the value as valid.

---

## 🔧 Fields (aliases and types)

| Group/Tab | Field | Alias | Type | Notes |
|---|---|---|---|---|
| Validity | Valid from | `validFrom` | DateTime (with time) | Campaign start |
|  | Valid to | `validTo` | DateTime (with time) | Countdown target |
| Text | Urgency text (desktop) | `urgencyText` | Textarea | HTML allowed |
|  | Urgency text (mobile) | `urgencyTextMobile` | Textarea | Falls back to desktop text if empty |
| CTA | CTA text | `urgencyCtaText` | Textstring | Button label |
|  | URL (Content Picker) | `urgencyUrl` | Content Picker | If empty → CTA is hidden |
| Behavior | Show urgency | `showUrgency` | Boolean | Turns the banner on |
|  | Sticky | `urgencySticky` | Boolean | Fix the banner |
|  | Sticky on mobile | `urgencyStickyOnMobile` | Boolean | Override for mobile |
|  | No countdown | `urgencyNoCountdown` | Boolean | Show without timer |
| Dismiss | Allow dismiss | `urgencyAllowDismiss` | Boolean | Show close button |
|  | Persist days | `urgencyPersistDays` | Integer | 0 = no memory; >0 stores dismissal |
| Styling | Background mode | `urgencyBackgroundMode` | Dropdown | `none` \| `color` \| `gradient` |
|  | Background color | `urgencyBgColor` | ColorPicker (EyeDropper) | Used when mode=`color` |
|  | Gradient preset | `urgencyGradientPreset` | Dropdown | Named presets |
|  | Text color | `urgencyTextColor` | ColorPicker (EyeDropper) | Optional |
| CTA Styling | CTA background | `urgencyCtaBgColor` | ColorPicker | Optional |
|  | CTA text color | `urgencyCtaTextColor` | ColorPicker | Optional |
| Mobile | Use compact CTA on mobile | `useMobileCompactCta` | Boolean | Small icon-like button |
| Misc | Custom CSS class | `urgencyCss` | Textstring | Additional classes on root element |

Field descriptions can be supplied via `descriptions.csv`. The package reads and applies them idempotently.

---

## 🎨 Styling & theming

Base CSS ships via RCL (`/_content/Mevisto.Countdown/...`).  
Override anything in your site CSS.

**CSS variables**
- `--mevisto-urgency-height` — set dynamically (for header offset)
- `--mc-text-color`
- `--mc-cta-bg`, `--mc-cta-fg`, `--mc-cta-border`
- `--mc-cta-bg-hover`, `--mc-cta-fg-hover`, `--mc-cta-border-hover`

**Body classes when active**
- `body.mevisto-banner-visible`
- `body.mevisto-has-banner`

---

## 🧠 Behavior in short

- **Countdown** runs client-side toward `validTo`. When time passes, the banner is removed.
- **Sticky** fixes the banner; otherwise it hides/shows on scroll (desktop).
- **Dismiss** stores a flag in `localStorage` and cookie if persistence days > 0.
- **CTA** is shown only if both CTA text and a valid URL exist.

---

## 🧪 Tips

- Place the component **before** your header in the layout.
- If you have a custom sticky header, ensure your CSS/JS matches its selector.
- CTA hides if Content Picker is empty or resolves to `#`.
- If you see “Date Picker” instead of “Date Picker with time”, re-select the correct datatype and save.

---

## ✅ Compatibility

- **Umbraco**: 16.x  
- **.NET**: 9.0  
- **uSync**: ships needed datatype configs and is safe to run repeatedly on startup.

---

## 🤝 Support

Issues and feature requests: please open an issue in the repository. PRs welcome.
E-mail: goddag@mevisto.se

## 📄 License

Proprietary EULA — see the [License Info](https://www.nuget.org/packages/Mevisto.Countdown/1.1.0/License) on NuGet.
