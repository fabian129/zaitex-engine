# Section 2: Services — Future Enhancements

**Status:** Section 2 layout LOCKED. Minor UI enhancements below to be iterated with Gemini.


Change picture box headline and text to only be a neat little text somewhere in the corner or middle of card, has to be different from the other cards, and the text should be very small, not taking up too much space 
---

## 🔄 Click Indicator for Large Image Cards

### **What to Add:**
**Click indicator icon in top-right outer corner** of large image cards (2x1 cards).

### **Visual Spec:**
- **Position:** Top-right corner (inside card, ~24px from edges)
- **Icon:** Small expand/plus icon or "→" arrow
- **Style:**
  - White icon with subtle background (glassmorphism circle or rounded square)
  - ~32px × 32px size
  - Opacity: 0.6 normal, 1.0 on hover
  - Subtle pulse animation to indicate clickability
- **Example code:**
  ```css
  .click-indicator {
    position: absolute;
    top: 24px;
    right: 24px;
    width: 32px;
    height: 32px;
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10;
    opacity: 0.6;
    transition: opacity 300ms;
  }

  .service-card:hover .click-indicator {
    opacity: 1;
  }
  ```

### **Behavior (Future Implementation):**
When large image card is clicked:
1. **Modal/card expands** — Full-screen overlay or centered card
2. **Content shown:**
   - Service name (e.g., "Web Design & Development")
   - Extended description (3-4 paragraphs)
   - Feature list (bulleted benefits)
   - Pricing info (if applicable)
   - **CTAs:**
     - "Book a Discovery Call" (primary, lime green button)
     - "View Portfolio" (secondary, ghost button)
     - "Learn More" (tertiary link)
3. **Close button:** X in top-right of modal
4. **Background:** Dark overlay with backdrop-blur

### **Cards That Need This:**
✅ Service 1: Large image card (PREMIUM SITES)
✅ Service 2: Large image card (YOUR SIGNATURE)
✅ Service 4: Full-width card (EXPERIENCES THAT MOVE)

### **Cards That DON'T Need This:**
❌ Small text cards (already show all info, no expansion needed)

---

## 🎯 Why This Approach:

**Benefits:**
- **Clean homepage:** Keep cards minimal, expand on-demand
- **CTA placement:** Put conversion CTAs inside modal (not cluttering main view)
- **User control:** Click to explore, don't force info overload
- **Mobile-friendly:** Modal works better than cramming info in small cards

**Iterate with Gemini:**
- Visual polish (icon style, animation)
- Modal design and interaction
- CTA button styling inside modal
- Close/escape behavior

---

## 📝 Implementation Notes:

**When building in React (19 Section Prototyper):**
1. Add `<div className="click-indicator">` to large image cards
2. Add `onClick` handler to open modal state
3. Build modal component with service details + CTAs
4. Add close handler (X button + escape key + backdrop click)

**Tech Stack:**
- Framer Motion for modal animation (slide up + fade in)
- Focus trap for accessibility
- Body scroll lock when modal open

---

**Status:** 📌 **NOTE DOCUMENTED** — Ready for Gemini iteration when needed.
