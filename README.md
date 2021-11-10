# helix-design-tokens
Helix Design System

# Intro

Helix is a [themeable design system](https://bradfrost.com/blog/post/creating-themeable-design-systems/) that can be skinned to match any Pfizer brand. Helix theming is accomplished through a robust variable system that maps a brand's variables to UI components. 

There are three tiers of variables:

- Tier 1 - Brand Definitions
- Tier 2 - UI Applications
- Tier 3 - Component Variables

Follow along for the nitty gritty details!

# Tier 1 - Brand Definitions

Tier 1 design tokens define the brand’s core attributes, serving as the raw materials for the UI’s visual design. Think of this tier as translating a brand's style guide into variables.

```css
--color-brand-starbucks-green: #00704a;
--font-family-primary: 'Roboto', sans-serif'
--font-size-xl: 3rem; /* equal to 48px */
--border-radius-pill: 1.25rem; /* equal to 20px */
```

It's important to note that these values are merely *definitions* and never imply any specific UI usage. 

## Tier 1 Syntax

```css
--[category]-[subcategory]-[value]
```

## Tier 1  Variable Specification

- **Animation**
    - Fade durations  (e.g. `--animation-fade-quick`)
    - Movement durations (e.g. `—animation-move-slow` )
    - Ease values e.g.  (e.g. `—anim-ease-out` )
- **Borders**
    - Border widths (e.g. `--border-width-small`)
    - Border radius (e.g. (`—border-radius-pill`)
    - Border style (e.g.`--border-style-dashed`)
- **Breakpoints**
    - Media query values (e.g. `--breakpoint-large`)
- **Colors**
    - Brand colors (e.g. `--color-brand-advil-gold`)
    - Neutral colors (e.g. `—-color-neutral-gray-50`)
    - Utility colors (e.g. `--color-utility-error`)
- **Layout**
    - Maximum widths (e.g. `--layout-max-width`)
    - (Note: grid sizing and gaps are handled in "Sizing")
- **Shadows**
    - Box (drop) shadows (e.g. `--box-shadow-large`)
- **Size**
    - Define base size unit, which is used to size grids, body padding and margins, and typography (e.g. `--size-base-unit: 0.5rem; /* equal to 8px */`)
- **Typography**
    - Font family (e.g. `--font-family-primary`)
    - Font size (e.g. `--font-size-large`)
    - Font weight (e.g. `--font-weight-semibold`)
    - Line height (e.g. `--line-height-small`)

## Tier 1 Considerations

- Tier 1 definitions should match the vernacular of the brand (e.g. if the brand calls their brand blue Sky Blue, declare the variable as `--color-brand-sky-blue`)
- T-shirt sizing tends to work fairly well for attributes like font size (e.g. `--font-size-xl`), border radius (e.g. `--border-radius-large`), border width (e.g. `--border-width-small`), line height (e.g. `--line-height-large`), etc
- Again, Tier 1 variables are UI-independent so there should be no mentions of forms or buttons or any other UI element at this level.

---

# Tier 2 - UI Application

Tier 2 variables takes the first-tier variables and maps them to high-level applications within the UI. Consider the following example:

```css
--button-primary-background: --color-brand-advil-gold;
```

What the above does is takes the Advil Gold brand color (`--color-brand-advil-gold`) defined in Tier 1 and applies it as the primary button's background color. Another example: 

```css
--form-label-text-color: --color-neutral-gray-85;
```

What this does is takes a dark gray color (`—-color-neutral-gray-85`) defined in Tier 1 and applies it as the color for form input labels (`—-form-label-text-color`).

## Tier 2 Syntax

```css
--[category]-[optional-variant]-[optional-theme]-[optional-element]-[css-property]-[optional-state]
```

## Tier 2 Variable Specification

### Typography

Typography is a special case because it bundles up several variables and is delivered as a `@mixin` . Each typography preset contains the following rules:

- Font family
- Font size
- Font weight
- Line height
- Letter spacing (if needed)
- Text transform (if needed)

In addition, typography mixins may contain responsive behavior to render a smaller font size for smaller viewports and larger font size for larger viewport. An example: 

```scss
@mixin typography-preset-1($responsive: true) {
  font-size: --font-size-xl;
  font-weight: --font-weight-bold;
  line-height: --line-height-large;

  @if $responsive == true {
    @media screen and (max-width: $breakpoint-medium) {
      font-size: $font-size-large-2;
      line-height: --line-height-medium;
    }
  }
}
```

### Global

- **Body**
    - Text color (e.g. `--body-text-color`)
    - Background (e.g. `--body-background`)
    - Typography (delivered as a typography preset `@mixin`)
        - Font family (e.g. `--body-font-family`)
        - Font size (e.g. `--body-font-size`)
        - Font weight (e.g. `--body-font-weight`
        - Line height (e.g. `--body-line-height`)
- **Focus ring**
    - Focus ring outline color (e.g. `--focus-ring-color`)
    - Focus ring width (e.g. `--focus-ring-width`)
    - Focus ring offset (e.g. `--focus-ring-offset`)
    

### Buttons

- **Background** (e.g. `--button-background`)
    - All style variants (e.g. `--button-primary-background`)
    - Hover state (e.g. `--button-background-hover`)
    - Focus state (e.g. `—-button-background-focus`)
    - Active state (e.g `--button-background-active`)
    - Disabled state (e.g `--button-background-disabled`)
- T**ext color** (e.g. `--button-text-color`)
    - All style variants (e.g. `--button-primary-text-color`)
    - Hover state (e.g. `--button-text-color-hover`)
    - Focus state (e.g. `—-button-text-color-focus`)
    - Active state (e.g `--button-text-color-active`)
    - Disabled state (e.g `--button-text-color-disabled`)
- **Border properties**
    - Border width (e.g. `--button-border-width`)
    - Border style (e.g. `--button-border-style`)
    - Border color (e.g. `--button-border-color`)
        - All applicable style variants (e.g. `--button-primary-border-color`)
        - Hover state (e.g. `--button-border-color-hover`)
        - Focus state (e.g. `—-button-border-color-focus`)
        - Active state (e.g `--button-border-color-active`)
        - Disabled state (e.g `--button-border-color-disabled`)
    - Border radius
- **Typography**
    - Font family (e.g. `--button-font-family`)
        - All style variants (e.g. `--button-primary-font-family`)
    - Font size (e.g. `--button-font-size`)
        - All style variants (e.g. `--button-primary-font-size`)
        - All size variants (e.g. `--button-large-font-size`)
    - Font weight (e.g. `--button-font-weight`)
        - All style variants (e.g. `--button-primary-font-size`)
    - Letter spacing (e.g. `--button-letter-spacing`)
        - All style variants (e.g. `--button-primary-letter-spacing`)
        - All size variants (e.g. `--button-large-letter-spacing`)
    - Line height (TODO: discuss. Likely buttons should have a hard-coded `line-height: 1;` value)
- **Padding**
    - Long-form padding values (e.g. `--button-padding-top` and `--button-padding-right`)
        - All style variants (e.g. `--button-primary-padding-left`)
        - All size variants (e.g. `--button-large-padding-bottom`)
- **Animation**
    - Transition duration (e.g. `--button-transition-duration`)
        - All style variants (e.g. `--button-primary-transition-duration`)
    - Transition ease (e.g. `--button-transition-ease`)
        - All style variants (e.g. `--button-primary-transition-ease`)

### **Forms**

- **Inputs**
    - Typography
    - Background color
    - Text color
    - Placeholder color
    - Border style
    - Typography
- Labels
    - Typography
    - Color

### Messaging

- Background color
    - Error
    - Success
    - Warning
    - Info
- Text color
    - Error
    - Success
    - Warning
    - Info
- Icon color
    - Error
    - Success
    - Warning
    - Info

## Tier 2 Considerations

- Tier 2 is far and away the hardest tier to understand, and the bulk of the work of creating a new theme involves the Tier 2 layer.
- All interactive UI elements (Buttons, links, form controls, clickable cards/blocks) need to account for the following states:
    - Hover
    - Focus
    - Active
    - Disabled
- All messaging utilities need to account for Info, Error, Warning, and Success
- Typography variables are clustered up and delivered at (TODO: determine how to get typography mixins into individual components

# Tier 3: Component Variables

Tier 3 are component-specific variables, which are found in each Helix component’s style file. These variables surface the themeable CSS properties of a given component, and are mapped to a Tier 2 variable. 

```css
--helix-select-label-text-color: --form-label-text-color:
```

What this does is takes the form label text color (`—-form-label-text-color`) defined in Tier 2 and applies it to the `helix-select` component's label (`--helix-select-label-text-color`). Another example:

```css
--helix-card-border-radius: --card-border-radius;
```

## Tier 3 Syntax

```jsx
--helix-[component-name]-[optional-element-or-modifier]-[css-property]-[optional-state]
```

## Tier 3 variable specification

Helix component variables can be viewed in the [Helix web component codebase](https://github.com/pfizer/helix-web-components/tree/master/src/components) and on the Helix reference site (coming soon)

## Tier 3 Considerations

- All Tier 3 variables provide a fallback value, which defaults to a rather vanilla default theme.
- TODO: the vanilla theme should have some pretty smart defaults when it comes to things like utility colors. I can foresee different brands caring more about button and card styles and leaving the default error, success, warning, and info colors intact. We should be mindful to not provide too much, but if certain theme variables are ommitted
- It is possible to map a Tier 1 variable to a Tier 3 variable and can be done so in certain circumstances

# Creating a New Helix Theme

Done right, creating a new brand theme for Helix involves the following steps: 

1. Define Tier 1 variables for the brand
2. Map Tier 1 variables to Tier 2 UI application values
3. If necessary, create any necessary Tier 3 overrides (which should be few)  
4. If necessary, create other additional styles that Helix theming does not account for (for instance, if for some weird reason you wanted to spin a button 360 degrees on hover, that would need to be manually added since Helix doesn't provide theme support for `translate`)
5. Publish theme (TODO: determine what exactly that entails)
6. TODO: work Sketch workflow in here

# Helix Theming Mechanics

Here's specifically how Helix theme architecture works.

## Theo

[Theo](https://github.com/salesforce-ux/theo) is an open source design token tool that takes abstract design token definitions and converts them into technology-specific variables. Helix uses Theo for a few purposes:

1. To output Tier 1 variables as both CSS custom properties and Sass variables. 
2. To output Tier 1 variables in formats compatible with native iOS and Android apps. 

## Helix Layer Cake

The Helix core library does not contain specific brand themes. The Tier 1 and Tier 2 variables are managed outside of the core library (TODO: discuss and establish this architecture) 

## Theme process

1. Designers and developers collaborate on theme definition (see "Creating a New Helix Theme" above) in the appropriate location (TODO: again define where this work will happen)
2. Pull theme into Helix web components Storybook environment (TODO: figure out how to do that and elegantly switch between different themes)
3. Run Theo to convert the design token YAML files into CSS custom properties and Sass variables (TODO: still undetermined if this will happen at the Helix layer or at the brand layer)
4. Run Storybook to view the theme applied to Helix components
