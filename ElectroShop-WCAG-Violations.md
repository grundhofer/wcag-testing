# ElectroShop - WCAG Focus Violations Analysis

This document identifies the specific WCAG violations found in the ElectroShop e-commerce subpage for educational purposes.

## Overview

The ElectroShop page demonstrates violations against 3 specific WCAG 2.2 Success Criteria related to focus management: 2.4.3 Focus Order, 2.4.7 Focus Visible, and 2.4.11 Focus not Obscured (Minimum). This realistic German e-commerce website contains intentional accessibility barriers specifically targeting keyboard navigation and focus management for educational testing.

---

## WCAG Violations Identified

### **2.4.3 Focus Order (Level A) - 2 Violations**
*"If a web page can be navigated sequentially and the navigation sequences affect meaning or operation, focusable components receive focus in an order that preserves meaning and operability"*

#### Violation 1: Search button appears before search input in tab order
**Location:** Header search functionality
**Issue:** The search button receives focus before the search input field
**Impact:** Keyboard users encounter the search button before they can enter search terms
**Code Example:**
```html
<!-- WCAG VIOLATION 2.4.3: Search button has tabindex before search input -->
<div class="flex items-center gap-2">
    <label for="search-input" class="sr-only">Produktsuche</label>
    <input 
        type="search" 
        id="search-input"
        name="search"
        placeholder="Produkte suchen..."
        class="px-4 py-2 border border-gray-300 rounded-lg w-64 search-field"
        tabindex="2"
        autocomplete="off"
    />
    <button class="bg-blue-600 text-white px-4 py-2 rounded" onclick="searchProducts()" tabindex="1">
        Suchen
    </button>
</div>
```

#### Violation 2: Filter apply button comes before filter options
**Location:** Product filter section
**Issue:** The "Filter anwenden" button appears first in tab order, before users can select filter criteria
**Impact:** Users reach the apply button before they can choose what to filter
**Code Example:**
```html
<!-- VIOLATION 2.4.3: Apply button comes first in tab order -->
<button class="bg-blue-600 text-white px-6 py-2 rounded" onclick="applyFilters()" tabindex="10">
    Filter anwenden
</button>

<div>
    <label for="category-filter" class="block text-sm font-medium mb-1">Kategorie</label>
    <select id="category-filter" class="w-full border border-gray-300 rounded px-3 py-2" tabindex="11">
        <option value="">Alle Kategorien</option>
        <option value="smartphones">Smartphones</option>
        <!-- ... more options ... -->
    </select>
</div>

<div>
    <label for="price-filter" class="block text-sm font-medium mb-1">Preis bis</label>
    <input type="number" id="price-filter" class="w-full border border-gray-300 rounded px-3 py-2" 
           placeholder="Maximaler Preis" tabindex="12">
</div>
```

### **2.4.7 Focus Visible (Level AA) - 2 Violations**
*"Any keyboard operable user interface has a mode of operation where the keyboard focus indicator is visible"*

#### Violation 1: All form inputs have focus indicators removed
**Location:** All input fields, select elements, and text areas throughout the site
**Issue:** CSS removes all focus indicators making it impossible to see which element has focus
**Impact:** Keyboard users cannot see which form field or control they are currently focused on
**Code Example:**
```css
/* VIOLATION 2.4.7: Removing focus indicators */
input:focus, select:focus, textarea:focus, button:focus, a:focus {
    outline: none !important;
    box-shadow: none !important;
}
.search-field:focus {
    border-color: #d1d5db !important;
}
```

#### Violation 2: Interactive buttons have no visible focus
**Location:** All buttons throughout the page including cart, wishlist, and product action buttons
**Issue:** The CSS rule above removes focus indicators from all interactive elements
**Impact:** Users navigating with keyboard cannot identify which button will be activated
**Applied to elements like:**
```html
<button class="btn btn-primary w-full mb-2" onclick="addToCart(1)">
    In den Warenkorb
</button>

<button class="btn btn-outline w-full text-sm" onclick="toggleWishlist(1)">
    <span aria-hidden="true">♥</span> Auf die Wunschliste
</button>

<button class="bg-blue-600 text-white px-4 py-2 rounded" onclick="searchProducts()">
    Suchen
</button>
```

### **2.4.11 Focus not Obscured (Minimum) (Level AA) - 2 Violations**
*"When a user interface component receives keyboard focus, the component is not entirely hidden due to author-created content"*

#### Violation 1: Newsletter popup can obscure focused content
**Location:** Newsletter signup popup that appears in bottom-right corner
**Issue:** The popup can cover content that users are trying to focus on, especially footer links
**Impact:** When users tab through page content, focused elements may be hidden behind the popup
**Code Example:**
```html
<!-- WCAG VIOLATION 2.4.11: Newsletter popup that can obscure focused content -->
<div id="newsletter-popup" class="fixed bottom-20 right-4 bg-white rounded-lg shadow-2xl p-6 z-50" 
     style="display: none; width: 320px;">
    <h3 class="text-lg font-bold mb-3">Newsletter Anmeldung</h3>
    <p class="text-sm mb-3">Erhalten Sie 10% Rabatt auf Ihre erste Bestellung!</p>
    <form onsubmit="return subscribeNewsletter(event);">
        <label for="newsletter-email" class="block text-sm font-medium mb-1">E-Mail-Adresse</label>
        <input type="email" id="newsletter-email" name="email" autocomplete="email" required 
               class="w-full p-2 border rounded mb-3">
        <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded w-full">Jetzt anmelden</button>
        <button type="button" onclick="closeNewsletter()" class="text-gray-500 text-sm mt-2">Später erinnern</button>
    </form>
</div>
```

#### Violation 2: Cookie banner obscures footer content when focused
**Location:** Fixed cookie banner at bottom of page
**Issue:** The banner covers footer links and other bottom page content when users try to focus on them
**Impact:** Users cannot access footer navigation or legal links that are positioned behind the banner
**Code Example:**
```html
<!-- WCAG VIOLATION 2.4.11: Cookie banner that obscures footer content when focused -->
<div id="cookie-banner" class="fixed bottom-0 left-0 right-0 bg-gray-900 text-white p-4 z-40" 
     style="display: block;">
    <div class="container mx-auto flex items-center justify-between">
        <p class="text-sm">Wir verwenden Cookies, um Ihre Erfahrung zu verbessern. Mit der Nutzung unserer Website stimmen Sie unserer Cookie-Richtlinie zu.</p>
        <div class="flex gap-2">
            <button onclick="acceptCookies()" class="bg-white text-gray-900 px-4 py-2 rounded text-sm">Alle akzeptieren</button>
            <button onclick="rejectCookies()" class="border border-white px-4 py-2 rounded text-sm">Nur notwendige</button>
        </div>
    </div>
</div>
```

---

## Summary

**Total Violations Found:** 6 distinct violations across 3 WCAG Success Criteria

**Severity Levels:**
- **Level A violations:** 2 (2.4.3 Focus Order)
- **Level AA violations:** 4 (2.4.7 Focus Visible, 2.4.11 Focus not Obscured)

**Focus Management Categories:**
1. **Focus Order (2.4.3)** - Logical tab sequence issues
2. **Focus Visibility (2.4.7)** - Missing visual focus indicators
3. **Focus Obscured (2.4.11)** - Content overlaying focused elements

**Impact Areas:**
- **Keyboard Users** - Cannot navigate efficiently or see current focus position
- **Users with Motor Disabilities** - Difficulty determining interaction state and sequence
- **Screen Reader Users** - Lose orientation when focus indicators are not visible
- **Cognitive Accessibility** - Confusion about navigation flow and current position

**E-commerce Features Demonstrated:**
- Professional German product catalog with proper accessibility
- Shopping cart functionality with labeled controls
- Product filtering with proper form labels
- User account features with semantic structure
- All content properly translated to German
- Proper alt text for all images
- Semantic HTML structure throughout
- ARIA labels where appropriate
- Proper form validation and error handling

**Educational Value:** This focused implementation demonstrates how keyboard navigation and focus management issues can severely impact user experience in e-commerce contexts, while maintaining all other accessibility best practices. The violations specifically target the most critical aspects of keyboard operability without introducing unnecessary barriers in other areas.

---

*This analysis focuses specifically on WCAG 2.2 Success Criteria 2.4.3, 2.4.7, and 2.4.11 violations for targeted keyboard navigation and focus management testing in a realistic German e-commerce context.*