# Responsive Design Testing Guide

## Quick Testing Checklist

### Mobile Devices (< 576px)

#### Hero Section
- [ ] Background image displays correctly
- [ ] Hero panel padding is appropriate (16-24px)
- [ ] Title font size is readable (28-40px)
- [ ] Subtitle is properly sized (20-32px)
- [ ] Content text is readable (13-15px)
- [ ] Resume button is 40px height, touch-friendly
- [ ] Social icons are 40px, properly spaced
- [ ] No horizontal scroll
- [ ] Image (if present) scales to 80vw max

#### About Section
- [ ] Content is full width
- [ ] Skills grid shows 1 column
- [ ] Skill items have proper padding (12-16px)
- [ ] Image is hidden on mobile (d-none d-md-block)
- [ ] Text is readable without zooming

#### Projects Section
- [ ] Cards stack vertically (1 column)
- [ ] Card titles are readable (0.95-1rem)
- [ ] Card descriptions are visible
- [ ] Badge language is readable
- [ ] No horizontal scroll
- [ ] Proper spacing between cards

#### Achievements Section
- [ ] Certificate cards stack vertically (1 column)
- [ ] Badge images scale properly (100px max)
- [ ] Card titles are readable
- [ ] Modal opens properly
- [ ] Modal iframe height is 400px
- [ ] Close button is accessible

### Tablet Devices (576px - 991px)

#### Hero Section
- [ ] Hero panel padding: 24-32px
- [ ] Title: 32-52px
- [ ] Subtitle: 22-36px
- [ ] Content: 14-16px
- [ ] Button: 40-44px
- [ ] Proper spacing maintained

#### About Section
- [ ] Skills grid shows 2 columns
- [ ] Image visible on medium+ (d-md-block)
- [ ] Proper spacing between sections
- [ ] Content flows naturally

#### Projects Section
- [ ] Cards show 2 columns (col-sm-6)
- [ ] Proper card sizing
- [ ] Spacing between cards
- [ ] Headers flex properly

#### Achievements Section
- [ ] Cards show 2 columns (col-md-4)
- [ ] Badge images: 120px
- [ ] Modal iframe height: 500px
- [ ] Proper card spacing

### Desktop Devices (992px+)

#### Hero Section
- [ ] Hero panel padding: 32-40px
- [ ] Title: 48-80px
- [ ] Subtitle: 32-48px
- [ ] Content: 16-18px
- [ ] Button: 44px height
- [ ] Background attachment: fixed
- [ ] Smooth parallax effect

#### About Section
- [ ] Image visible on left (col-lg-4)
- [ ] Content on right (col-lg-8)
- [ ] Skills grid: 2 columns
- [ ] Proper spacing and alignment

#### Projects Section
- [ ] Cards show 3 columns (col-lg-4)
- [ ] Hover effects work smoothly
- [ ] Proper card sizing
- [ ] Good visual hierarchy

#### Achievements Section
- [ ] Cards show 4 columns (col-lg-3)
- [ ] Badge images: 150px
- [ ] Modal iframe height: 600px
- [ ] Smooth hover animations

## Browser DevTools Testing

### Chrome/Edge DevTools
1. Press `F12` to open DevTools
2. Click device toggle (Ctrl+Shift+M)
3. Select device from dropdown or custom size
4. Test at these widths:
   - 320px (iPhone SE)
   - 375px (iPhone 12)
   - 480px (Large phone)
   - 768px (iPad)
   - 1024px (iPad Pro)
   - 1440px (Desktop)

### Firefox Developer Tools
1. Press `F12` to open DevTools
2. Click responsive design mode (Ctrl+Shift+M)
3. Select device or enter custom dimensions
4. Test same widths as Chrome

### Safari Developer Tools
1. Enable Developer Menu: Safari → Preferences → Advanced
2. Develop → Enter Responsive Design Mode
3. Select device or custom size
4. Test same widths

## Real Device Testing

### iOS Devices
- iPhone SE (320px)
- iPhone 12/13 (390px)
- iPhone 14 Pro Max (430px)
- iPad (768px)
- iPad Pro (1024px)

### Android Devices
- Small phone (320px)
- Standard phone (375px)
- Large phone (480px)
- Tablet (768px)

## Performance Testing

### Lighthouse Audit
1. Open DevTools (F12)
2. Go to Lighthouse tab
3. Select "Mobile" or "Desktop"
4. Click "Analyze page load"
5. Check scores:
   - Performance: > 90
   - Accessibility: > 90
   - Best Practices: > 90
   - SEO: > 90

### Network Testing
1. Open DevTools Network tab
2. Throttle to "Slow 4G"
3. Reload page
4. Check:
   - CSS files load properly
   - Images load without errors
   - No 404 errors
   - Total load time < 3s

## Accessibility Testing

### Keyboard Navigation
- [ ] Tab through all interactive elements
- [ ] Focus states are visible
- [ ] Buttons are accessible
- [ ] Links are understandable
- [ ] Modal can be closed with Escape

### Screen Reader Testing
- [ ] Use NVDA (Windows) or VoiceOver (Mac)
- [ ] Test heading hierarchy
- [ ] Test image alt text
- [ ] Test button labels
- [ ] Test form labels

### Color Contrast
- [ ] Use WebAIM Contrast Checker
- [ ] Text contrast ratio > 4.5:1
- [ ] Large text contrast ratio > 3:1
- [ ] Test in both light and dark modes

## Common Issues & Solutions

### Issue: Horizontal Scroll on Mobile
**Solution**: Check for fixed widths, use max-width: 100%

### Issue: Text Too Small
**Solution**: Verify clamp() values, check font-size media queries

### Issue: Buttons Not Clickable
**Solution**: Ensure min-height: 44px, min-width: 44px

### Issue: Images Distorted
**Solution**: Use max-width: 100%, height: auto

### Issue: Modal Overflow
**Solution**: Check modal-dialog margin, use responsive padding

## Testing Automation

### Using Playwright/Cypress
```bash
# Test multiple viewports
npx playwright test --headed
```

### Using WebDriver
```bash
# Test responsive behavior
npm test -- --viewport-size 320x568
```

## Reporting Issues

When reporting responsive issues, include:
1. Device/browser used
2. Screen width/height
3. Screenshot or video
4. Expected vs actual behavior
5. Steps to reproduce

## Sign-Off Checklist

- [ ] All breakpoints tested
- [ ] No horizontal scroll
- [ ] Touch targets are 44x44px minimum
- [ ] Text is readable
- [ ] Images scale properly
- [ ] Modals are responsive
- [ ] Accessibility passes
- [ ] Performance is good
- [ ] Dark mode works
- [ ] Print styles work

## Notes

- Test on real devices when possible
- Test in both portrait and landscape
- Test with different zoom levels
- Test with different font sizes
- Test with slow network speeds
- Test with accessibility tools enabled

