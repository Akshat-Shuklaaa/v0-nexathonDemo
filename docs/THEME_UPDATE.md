# NEXATHON 2026 - Theme Update Documentation

## 📋 Overview

This document provides comprehensive information about the major theme and architecture update implemented for NEXATHON 2026. The website has been transformed from a green-themed design to a modern black-white-blue color scheme with full dark/light mode support, centralized data management, and enhanced animations.

---

## 🎨 Theme Changes

### Color Scheme Transformation

**Previous Theme:** Green-based tech theme (oklch 145-175 hue range)
**New Theme:** Black-White-Blue modern theme (oklch 240-260 hue range)

### Color Variables

#### Light Mode
```css
--primary: oklch(0.55 0.22 250)      /* Vibrant Blue */
--secondary: oklch(0.45 0.15 260)    /* Deep Blue */
--accent: oklch(0.65 0.18 245)       /* Bright Blue */
--background: oklch(0.98 0 0)        /* Pure White */
--foreground: oklch(0.15 0 0)        /* Near Black */
```

#### Dark Mode
```css
--primary: oklch(0.65 0.25 250)      /* Bright Blue */
--secondary: oklch(0.55 0.18 260)    /* Mid Blue */
--accent: oklch(0.7 0.2 245)         /* Light Blue */
--background: oklch(0.08 0.01 250)   /* Deep Black */
--foreground: oklch(0.95 0.01 250)   /* Off White */
```

### Theme Toggle Implementation

A theme toggle button has been added to the navigation bar (both desktop and mobile) that allows users to switch between dark and light modes seamlessly.

**Location:** Navbar component ([components/layout/navbar.tsx](components/layout/navbar.tsx))

**Features:**
- Smooth transitions between themes
- System preference detection
- Persistent theme selection
- Icon-based toggle (Sun/Moon icons)

---

## 📦 Centralized Data Management

### New Data Structure

All static content has been moved to a centralized data file at `lib/data.tsx`. This eliminates the need to hunt through component files to update content.

**File Location:** [lib/data.tsx](lib/data.tsx)

### Data Sections

The data file contains the following structured sections:

#### 1. Event Information
```typescript
export const eventInfo = {
  name: "NEXATHON 2026",
  tagline: "Build. Innovate. Transform.",
  date: "March 15-17, 2026",
  duration: "36 Hours",
  venue: "Tech Innovation Center, Bangalore",
  participantCount: 500,
  mentorCount: 50,
  prizePool: "₹5,00,000",
  // ... more fields
}
```

#### 2. Hero Section Data
```typescript
export const heroData = {
  logo: { text, subtitle, description },
  taglines: [],
  stats: [],
  cta: { primary, secondary }
}
```

#### 3. About Section Data
```typescript
export const aboutData = {
  title,
  subtitle,
  description: [],
  features: [],
  stats: []
}
```

#### 4. Schedule Data
Timeline of events for all 3 days

#### 5. Timeline Data
Registration and major milestone dates

#### 6. Sponsors Data
Organized by tiers (Platinum, Gold, Silver, Community)

#### 7. Rewards Data
Prize information including main prizes and special categories

#### 8. Themes Data
Hackathon tracks and categories

#### 9. FAQ Data
Common questions and answers

#### 10. Gallery Data
Event images and media

#### 11. Contact Data
Organization details and team information

#### 12. Navigation Data
Menu links and branding

#### 13. Footer Data
Footer content and links

### How to Update Content

To update any content on the website:

1. **Open** `lib/data.tsx`
2. **Find** the relevant section (use comments as guide)
3. **Update** the values directly
4. **Save** the file

Changes will automatically reflect across all components that use that data.

**Example:** To change the event date:
```typescript
// In lib/data.tsx
export const eventInfo = {
  // ... other fields
  date: "March 15-17, 2026", // Change this date
  // ... other fields
}
```

---

## ✨ Animation Enhancements

### Smoother Transitions

All animation timings have been increased for smoother, more polished effects:

- **Hero section fade-ins:** 700ms → 1000ms
- **Hover effects:** 300ms → 500ms
- **Scale transformations:** Added easing functions for natural motion
- **3D effects:** Enhanced with preserve-3d and perspective

### New Creative Effects

#### 1. Enhanced Glow Effects
```css
.glow-text {
  text-shadow: multiple layers with blue theme
}
```

#### 2. Improved Holographic Effect
Background gradient animation with blue color spectrum

#### 3. Better Particle Animations
Floating particles with smoother trajectories

#### 4. Neon Flicker
Dynamic flickering effect for accent text

#### 5. Shimmer Effect
Subtle shine animation on hover states

### Animation Classes Available

All animations are defined in [app/globals.css](app/globals.css):

- `.glow-text` - Text glow effect
- `.glow-border` - Border glow effect
- `.holographic` - Holographic gradient
- `.pulse-glow` - Pulsing glow animation
- `.neon-flicker` - Neon flickering effect
- `.float-3d` - 3D floating animation
- `.shimmer` - Shimmer effect
- `.morph` - Morphing shape animation
- `.text-gradient-animated` - Animated text gradient
- And many more...

---

## 🖼️ Placeholder Management

### Logo Placeholders

Logo placeholders have been updated to use structured data:

**Hero Section Logo:**
```typescript
heroData.logo = {
  text: "NEXATHON",
  subtitle: "2026",
  description: "Innovation Starts Here"
}
```

**To Add Real Logos:**

1. Place logo files in `/public/logos/` directory
2. Update the data in `lib/data.tsx`:

```typescript
// For sponsors
{
  name: "TechCorp Global",
  logo: "/logos/techcorp.svg",  // Path to actual logo
  website: "https://techcorp.com"
}
```

3. Components will automatically use the logo paths

### Image Placeholders

**Gallery Images:**
```typescript
export const galleryData = {
  images: [
    {
      src: "/gallery/nexathon-opening.jpg",  // Update with actual path
      alt: "NEXATHON Opening Ceremony",
      category: "ceremony",
      title: "Opening Ceremony 2025"
    }
  ]
}
```

**To Replace Placeholders:**
1. Add images to `/public/gallery/` or `/public/logos/`
2. Update paths in `lib/data.tsx`
3. Images will load automatically

---

## 🏗️ Component Updates

### Components Using Centralized Data

The following components have been updated to use data from `lib/data.tsx`:

✅ **Hero Section** ([components/sections/hero-section.tsx](components/sections/hero-section.tsx))
- Uses: `heroData`, `eventInfo`

✅ **About Section** ([components/sections/about-section.tsx](components/sections/about-section.tsx))
- Uses: `aboutData`

✅ **Navbar** ([components/layout/navbar.tsx](components/layout/navbar.tsx))
- Uses: `navigationData`
- Includes theme toggle

✅ **Layout** ([app/layout.tsx](app/layout.tsx))
- Wrapped with ThemeProvider
- Updated metadata for 2026

### Components Pending Update

The following sections still need to be updated to use centralized data:

- [ ] Schedule Section
- [ ] Timeline Section
- [ ] Sponsors Section
- [ ] Rewards Section
- [ ] Register Section
- [ ] Themes Section
- [ ] FAQ Section
- [ ] Gallery Section
- [ ] Contact Section
- [ ] Footer

**Migration Pattern:**

```typescript
// 1. Import data at top of component
import { sectionData } from "@/lib/data"

// 2. Replace hardcoded arrays/objects with imported data
// Before:
const items = [{ title: "...", description: "..." }]

// After:
const items = sectionData.items
```

---

## 🎯 Key Features Implemented

### 1. Dark/Light Mode Toggle
- Seamless theme switching
- Persistent across sessions
- System preference detection
- Available in navbar (desktop & mobile)

### 2. Centralized Data Management
- Single source of truth for all content
- Easy content updates without touching components
- Type-safe with TypeScript
- Organized by sections

### 3. Modern Color Scheme
- Professional black-white-blue palette
- Excellent contrast in both modes
- Consistent across all components
- WCAG compliant color ratios

### 4. Enhanced Animations
- Smoother transitions (1000ms standard)
- Creative 3D effects
- Improved hover states
- Performance-optimized

### 5. Improved User Experience
- Faster content updates
- Better visual hierarchy
- Smoother interactions
- More engaging animations

---

## 🚀 Development Workflow

### Adding New Content

1. **Define data structure** in `lib/data.tsx`:
```typescript
export const newSectionData = {
  title: "Section Title",
  items: [...]
}
```

2. **Import in component**:
```typescript
import { newSectionData } from "@/lib/data"
```

3. **Use in JSX**:
```typescript
<h2>{newSectionData.title}</h2>
{newSectionData.items.map(...)}
```

### Updating Themes

To modify the color scheme:

1. **Edit CSS variables** in [app/globals.css](app/globals.css)
2. **Update both `:root` and `.dark` sections**
3. **Test in both light and dark modes**

### Customizing Animations

1. **Find animation classes** in [app/globals.css](app/globals.css)
2. **Modify keyframes or durations**
3. **Apply to elements** via className

---

## 📝 Content Update Guide

### Quick Reference for Common Updates

#### Change Event Date
```typescript
// lib/data.tsx
eventInfo.date = "March 15-17, 2026"
```

#### Update Prize Amount
```typescript
// lib/data.tsx
rewardsData.mainPrizes[0].prize = "₹2,00,000"
```

#### Add New Sponsor
```typescript
// lib/data.tsx
sponsorsData.tiers[0].sponsors.push({
  name: "New Company",
  logo: "/logos/newcompany.svg",
  website: "https://newcompany.com"
})
```

#### Modify FAQ
```typescript
// lib/data.tsx
faqData.questions.push({
  question: "New Question?",
  answer: "Detailed answer..."
})
```

#### Update Contact Info
```typescript
// lib/data.tsx
contactData.email = "newemail@nexathon.com"
contactData.phone = "+91 98765 43210"
```

---

## 🔧 Technical Implementation

### File Structure

```
/workspaces/Nexathon-26/
├── app/
│   ├── globals.css          # Updated with blue theme
│   ├── layout.tsx            # ThemeProvider integration
│   └── page.tsx              # Main page structure
├── components/
│   ├── layout/
│   │   ├── navbar.tsx        # Theme toggle + data integration
│   │   ├── footer.tsx        # Pending update
│   │   └── theme-provider.tsx # Theme context
│   └── sections/
│       ├── hero-section.tsx  # ✅ Updated
│       ├── about-section.tsx # ✅ Updated
│       └── ...               # Pending updates
├── lib/
│   └── data.tsx              # ⭐ NEW - Centralized data
└── docs/
    └── THEME_UPDATE.md       # This file
```

### Dependencies

**Theme Management:**
```json
{
  "next-themes": "^0.x.x"
}
```

**Icons:**
```json
{
  "lucide-react": "^0.x.x"
}
```

### Browser Support

- Modern browsers (Chrome, Firefox, Safari, Edge)
- CSS custom properties (CSS variables)
- oklch color space
- Backdrop filter support

---

## 🐛 Troubleshooting

### Theme Not Switching

**Issue:** Theme toggle doesn't work
**Solution:** Ensure ThemeProvider is wrapping the app in `layout.tsx`

### Colors Look Wrong

**Issue:** Colors don't match the theme
**Solution:** Check for hardcoded green colors in component files, replace with CSS variables

### Data Not Updating

**Issue:** Changes to `lib/data.tsx` not reflecting
**Solution:** Restart dev server (`npm run dev`) to clear cache

### Animations Too Fast/Slow

**Issue:** Animations feel off
**Solution:** Adjust duration values in component transition classes

---

## 📊 Performance Considerations

### Optimizations Implemented

1. **CSS Variables** - Faster theme switching
2. **Centralized Data** - Single source reduces bundle size
3. **Lazy Loading** - Components load on demand
4. **Optimized Animations** - Hardware-accelerated transforms
5. **Reduced Motion** - Respects user preferences

### Best Practices

- Keep data objects lean
- Use memo for expensive computations
- Lazy load images
- Minimize re-renders

---

## 🎓 Learning Resources

### Understanding the Stack

- **Next.js 14+** - React framework
- **Tailwind CSS** - Utility-first CSS
- **next-themes** - Theme management
- **TypeScript** - Type safety

### Color System

- **oklch()** - Modern color space with better perceptual uniformity
- **CSS Custom Properties** - Dynamic theming
- **Color Contrast** - WCAG compliance

---

## 📈 Future Enhancements

### Recommended Next Steps

1. **Complete Data Migration**
   - Update remaining sections to use `lib/data.tsx`
   - Remove all hardcoded content from components

2. **Add Real Media**
   - Replace logo placeholders with actual logos
   - Add real event photos to gallery
   - Update sponsor logos

3. **Advanced Features**
   - Implement registration form backend
   - Add email notification system
   - Create admin panel for content management

4. **Performance**
   - Image optimization
   - Code splitting
   - Caching strategies

5. **Accessibility**
   - Keyboard navigation improvements
   - Screen reader optimizations
   - Focus management

---

## 🤝 Contributing

### Making Changes

1. **Content Changes:** Edit `lib/data.tsx`
2. **Theme Changes:** Edit `app/globals.css`
3. **Component Updates:** Follow existing patterns in updated components
4. **Testing:** Check both light and dark modes

### Code Style

- Use TypeScript for type safety
- Follow existing naming conventions
- Comment complex logic
- Keep components focused and reusable

---

## 📞 Support

### Getting Help

- **Documentation:** This file and other docs in `/docs`
- **Code Examples:** Check updated components (hero, about, navbar)
- **Issues:** Create an issue in the repository

---

## 📜 Changelog

### Version 2.0.0 - December 2025

**Major Changes:**
- ✅ Theme changed from green to black-white-blue
- ✅ Added dark/light mode toggle
- ✅ Created centralized data management system (`lib/data.tsx`)
- ✅ Enhanced all animations (smoother, longer durations)
- ✅ Updated hero section with centralized data
- ✅ Updated about section with centralized data
- ✅ Updated navbar with theme toggle and centralized data
- ✅ Improved color scheme with better contrast
- ✅ Added comprehensive documentation

**Pending:**
- ⏳ Update remaining sections with centralized data
- ⏳ Replace all logo and image placeholders
- ⏳ Add real sponsor logos
- ⏳ Implement backend for registration form

---

## 🎯 Quick Start Guide

### For Content Editors

1. Open `lib/data.tsx`
2. Find your section using comments
3. Edit the values
4. Save and refresh

### For Developers

1. Check this documentation
2. Review updated components (hero, about, navbar)
3. Follow the same pattern for other sections
4. Test in both themes

### For Designers

1. Theme colors in `app/globals.css`
2. Animation classes documented in this file
3. Component structure in `/components`

---

## 📋 Checklist for Complete Migration

- [x] Create `lib/data.tsx` with all data structures
- [x] Update theme colors to black-white-blue
- [x] Add theme toggle to navbar
- [x] Update hero section
- [x] Update about section
- [x] Update navbar
- [x] Enhance animations
- [x] Write documentation
- [ ] Update schedule section
- [ ] Update timeline section
- [ ] Update sponsors section
- [ ] Update rewards section
- [ ] Update themes section
- [ ] Update FAQ section
- [ ] Update gallery section
- [ ] Update contact section
- [ ] Update footer
- [ ] Replace all logo placeholders
- [ ] Add real images to gallery
- [ ] Test thoroughly in both modes

---

## 🌟 Summary

This update transforms NEXATHON into a modern, maintainable, and visually stunning website with:

1. **Professional Theme** - Black-white-blue with dark/light modes
2. **Easy Management** - All content in one place
3. **Better UX** - Smoother animations and transitions
4. **Future-Ready** - Easy to update and extend

The centralized data approach means anyone can update content without touching code, making the website much more maintainable long-term.

---

**Last Updated:** December 22, 2025
**Version:** 2.0.0
**Author:** GitHub Copilot
**Status:** In Progress - Core features complete, remaining sections need migration
