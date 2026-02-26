# X (Twitter) UI Clone — Step-by-Step Build Guide

Build the X feed page UI from scratch. Each step adds a small piece — paste the snippets in order and watch the UI come together.

---

## Table of Contents

1. [Step 1 — HTML Boilerplate & CSS Reset](#step-1--html-boilerplate--css-reset)
2. [Step 2 — Three-Column Page Layout (Empty Boxes)](#step-2--three-column-page-layout-empty-boxes)
3. [Step 3 — Main Area: Header + Feed Split](#step-3--main-area-header--feed-split)
4. [Step 4 — Navbar: X Logo](#step-4--navbar-x-logo)
5. [Step 5 — Navbar: Navigation Items](#step-5--navbar-navigation-items)
6. [Step 6 — Navbar: Notification Badge](#step-6--navbar-notification-badge)
7. [Step 7 — Navbar: Extra Label (Business "30% off")](#step-7--navbar-extra-label-business-30-off)
8. [Step 8 — Navbar: Post Button](#step-8--navbar-post-button)
9. [Step 9 — Navbar: User Profile Section](#step-9--navbar-user-profile-section)
10. [Step 10 — Header: Logo (Mobile) & Tabs](#step-10--header-logo-mobile--tabs)
11. [Step 11 — Sidebar: Search Bar](#step-11--sidebar-search-bar)
12. [Step 12 — Sidebar: Subscribe to Premium Card](#step-12--sidebar-subscribe-to-premium-card)
13. [Step 13 — Sidebar: Trending Section](#step-13--sidebar-trending-section)
14. [Step 14 — Sidebar: Who to Follow Section](#step-14--sidebar-who-to-follow-section)
15. [Step 15 — Feed: New Post Composer](#step-15--feed-new-post-composer)
16. [Step 16 — Feed: A Single Post (Text Only)](#step-16--feed-a-single-post-text-only)
17. [Step 17 — Feed: Post Images (1 / 2 / 3 / 4 Image Layouts)](#step-17--feed-post-images-1--2--3--4-image-layouts)
18. [Step 18 — Feed: Post Action Buttons](#step-18--feed-post-action-buttons)
19. [Step 19 — Feed: Threads (Reply Chains)](#step-19--feed-threads-reply-chains)
20. [Step 20 — Floating Elements: Grok Button & Message Box](#step-20--floating-elements-grok-button--message-box)
21. [Step 21 — Responsive: Hide Sidebar on Medium Screens](#step-21--responsive-hide-sidebar-on-medium-screens)
22. [Step 22 — Responsive: Mobile Navbar at Bottom](#step-22--responsive-mobile-navbar-at-bottom)
23. [Step 23 — Scrollbar Styling](#step-23--scrollbar-styling)

---

## Step 1 — HTML Boilerplate & CSS Reset

Start with a blank HTML file and a blank CSS file. Link them together and add a global CSS reset.

### `index.html`

```html
<!DOCTYPE html>
<html lang="en-IN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>X UI Clone</title>

    <link rel="stylesheet" href="/styles/index.css">

    <link rel="shortcut icon" href="/assets/icons/x.svg" type="image/x-icon">
</head>
<body>

</body>
</html>
```

### `styles/index.css`

> **What this does:** Resets browser defaults, sets dark background, and defines CSS variables we'll use everywhere.

```css
/* Reset some default browser CSS */
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: sans-serif;

    --border-color: #252525;
    --primary-blue-color: #1DA1F2;
    --hover-background-color: #292929;
    --active-background-color: #3b3b3b;
}

:root {
    background-color: black;
    color: white;
}

img {
    user-select: none;
}
```

**Key takeaways:**
- `box-sizing: border-box` — padding/border are included in width/height calculations.
- CSS Custom Properties (`--border-color`, etc.) — define once, reuse everywhere.

---

## Step 2 — Three-Column Page Layout (Empty Boxes)

This is the most important step — the foundation. X has three columns: **Navbar** (left), **Main feed** (center), **Sidebar** (right).

### `index.html` — Add inside `<body>`

```html
<nav class="navbar">
    Navbar
</nav>

<main class="main">
    Main
</main>

<aside class="aside">
    Sidebar
</aside>
```

### `styles/index.css` — Add below the reset

```css
body {
    /* Make the page responsive for ultra-wide screen sizes. */
    max-width: 85rem;
    margin: auto;
    display: flex;
    justify-content: center;
    height: 100dvh;
}

.navbar {
    flex: none;
    width: 17rem;
    overflow: auto;
}

.main {
    flex: 1;
    display: flex;
    flex-direction: column;
    border-left: 1px solid var(--border-color);
    border-right: 1px solid var(--border-color);
}

.aside {
    flex: none;
    width: 25rem;
    overflow: auto;
}
```

**Key takeaways:**
- `display: flex` on `<body>` — the three children sit side by side.
- `flex: none` on navbar/aside — they keep their fixed widths.
- `flex: 1` on main — it stretches to fill all the remaining space.
- `height: 100dvh` — the layout takes the full viewport height.

---

## Step 3 — Main Area: Header + Feed Split

Inside `<main>`, we have a **sticky header** at the top and a **scrollable feed** below it.

### `index.html` — Replace the text "Main" inside `<main>` with:

```html
<header class="header">
    Header
</header>

<div class="feed">
    Feed
</div>
```

### `styles/index.css` — Add below `.main`

```css
.header {
    flex: none;
    border-bottom: 1px solid var(--border-color);
}

.feed {
    overflow: auto;
}
```

**Key takeaways:**
- `.main` is already `display: flex; flex-direction: column;` — so header sits on top, feed takes the rest.
- `flex: none` on header — prevents it from shrinking.
- `overflow: auto` on `.feed` — only the feed scrolls, header stays pinned.

---

## Step 4 — Navbar: X Logo

Now we go inside the navbar and build it piece by piece. First, add the structure and the logo.

### `index.html` — Replace the text "Navbar" inside `<nav>` with:

```html
<ul>
    <!-- Main Logo of X -->
    <li class="logo">
        <a href="#" role="button">
            <img src="/assets/icons/x.svg" alt="X (formerly Twitter)">
        </a>
    </li>
</ul>
```

### Create `styles/navbar.css` and link it in the `<head>`:

```html
<link rel="stylesheet" href="/styles/navbar.css">
```

### `styles/navbar.css`

```css
.navbar > ul {
    width: 100%;
    height: 100%;
    list-style: none;
    display: flex;
    flex-direction: column;
    align-items: start;
    gap: 0.5rem;
    padding: 0.5rem;
}

/* Main X logo */
.navbar > ul > .logo {
    padding: 1rem;
    border-radius: 100%;
    cursor: pointer;
}

.navbar > ul > .logo:hover {
    background-color: var(--hover-background-color);
}
.navbar > ul > .logo:active {
    background-color: var(--active-background-color);
}

.navbar > ul > .logo img {
    width: 2rem;
    aspect-ratio: 1;
}
```

**Key takeaways:**
- `list-style: none` — removes bullet points from `<ul>`.
- `flex-direction: column` — nav items stack vertically.
- `aspect-ratio: 1` — keeps the image a perfect square.

---

## Step 5 — Navbar: Navigation Items

Add all the navigation links (Home, Explore, Notifications, etc.).

### `styles/navbar.css` — Add CSS variables at the top of the file (before all rules):

```css
/* Set the variables to implement responsive design */
.navbar {
    --navbar-icon-size: 1.6rem;
    --navbar-label-font-size: 1.35rem;
}
```

### `index.html` — Add after the logo `<li>`, still inside `<ul>`:

```html
<!-- Navigation Items -->
<li class="navitem active">
    <a href="#" role="button">
        <img src="/assets/icons/home_active.svg" alt="Home" aria-labelledby="nav-label-home">
        <span id="nav-label-home">Home</span>
    </a>
</li>
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/search.svg" alt="Explore" aria-labelledby="nav-label-explore">
        <span id="nav-label-explore">Explore</span>
    </a>
</li>
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/bell.svg" alt="Notifications" aria-labelledby="nav-label-notifications">
        <span id="nav-label-notifications">Notifications</span>
    </a>
</li>
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/message.svg" alt="Messages" aria-labelledby="nav-label-messages">
        <span id="nav-label-messages">Messages</span>
    </a>
</li>
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/xai.svg" alt="Grok" aria-labelledby="nav-label-grok">
        <span id="nav-label-grok">Grok</span>
    </a>
</li>
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/bookmark.svg" alt="Bookmarks" aria-labelledby="nav-label-bookmarks">
        <span id="nav-label-bookmarks">Bookmarks</span>
    </a>
</li>
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/communities.svg" alt="Communities" aria-labelledby="nav-label-communities">
        <span id="nav-label-communities">Communities</span>
    </a>
</li>
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/x.svg" alt="Premium" aria-labelledby="nav-label-premium">
        <span id="nav-label-premium">Premium</span>
    </a>
</li>
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/lightning.svg" alt="Business" aria-labelledby="nav-label-business">
        <span id="nav-label-business">Business</span>
    </a>
</li>
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/profile.svg" alt="Profile" aria-labelledby="nav-label-profile">
        <span id="nav-label-profile">Profile</span>
    </a>
</li>
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/more.svg" alt="More" aria-labelledby="nav-label-more">
        <span id="nav-label-more">More</span>
    </a>
</li>
```

### `styles/navbar.css` — Add:

```css
/* Navigation Items */
.navbar > ul > .navitem {
    flex: none;
}

.navbar > ul > .navitem > a {
    display: flex;
    justify-content: start;
    align-items: center;
    padding: 0.75rem;
    gap: 0.75rem;
    border-radius: 1rem;
    cursor: pointer;
    text-decoration: none;
    color: white;
}

.navbar > ul > .navitem > a:hover {
    background-color: var(--hover-background-color);
}
.navbar > ul > .navitem > a:active {
    background-color: var(--active-background-color);
}

.navbar > ul > .navitem img {
    width: var(--navbar-icon-size);
    aspect-ratio: 1;
}
.navbar > ul > .navitem.active img {
    scale: 1.2;
}

.navbar > ul > .navitem span {
    font-size: var(--navbar-label-font-size);
    user-select: none;
}
.navbar > ul > .navitem.active span {
    font-weight: bold;
}
```

**Key takeaways:**
- Each nav item is a flex row: icon on the left, label on the right.
- The `active` class makes the current page's icon bigger and label bold.
- `text-decoration: none` — removes the underline from `<a>` tags.
- `aria-labelledby` — connects the icon to its label for accessibility.

---

## Step 6 — Navbar: Notification Badge

The Notifications icon has a small count badge on top of it.

### `index.html` — Replace the Notifications `<li>` with:

```html
<li class="navitem">
    <a href="#" role="button">
        <div class="notifications-img-holder">
            <img src="/assets/icons/bell.svg" alt="Notifications" aria-labelledby="nav-label-notifications">
            <span class="notifications-count">3</span>
        </div>
        <span id="nav-label-notifications">Notifications</span>
    </a>
</li>
```

### `styles/navbar.css` — Add:

```css
.navbar .notifications-img-holder {
    position: relative;
}

.navbar .notifications-img-holder .notifications-count {
    position: absolute;
    top: -25%;
    right: -25%;
    width: 1.2rem;
    height: 1.2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 100%;
    background-color: var(--primary-blue-color);
    font-weight: bold;
    font-size: 0.9rem;
}
```

**Key takeaways:**
- `position: relative` on the parent — creates a positioning context.
- `position: absolute` on the badge — places it relative to the parent, not the page.
- Negative `top` and `right` — pushes the badge to the top-right corner of the icon.

---

## Step 7 — Navbar: Extra Label (Business "30% off")

The Business nav item has a small "30% off" badge next to it.

### `index.html` — Update the Business `<li>` to add the extra label:

```html
<li class="navitem">
    <a href="#" role="button">
        <img src="/assets/icons/lightning.svg" alt="Business" aria-labelledby="nav-label-business">
        <span id="nav-label-business">Business</span>
        <span class="navitem-extra-label">30% off</span>
    </a>
</li>
```

### `styles/navbar.css` — Add:

```css
.navbar .navitem span.navitem-extra-label {
    background-color: var(--primary-blue-color);
    font-size: 0.9rem;
    font-weight: bold;
    padding: 0.15rem;
    padding-left: 0.65rem;
    padding-right: 0.65rem;
    border-radius: 0.25rem;
}
```

---

## Step 8 — Navbar: Post Button

A full-width CTA button to create a new post.

### `index.html` — Add after the last navitem `<li>`, still inside `<ul>`:

```html
<!-- Post Button -->
<li class="post">
    <button>
        Post
    </button>
</li>
```

### `styles/navbar.css` — Add:

```css
/* Post Button */
.navbar > ul > .post {
    width: 100%;
}

.navbar > ul > .post > button {
    width: 100%;
    height: 3rem;
    border: none;
    border-radius: 3rem;
    background-color: white;
    color: black;
    font-size: 1.2rem;
    font-weight: bold;
    cursor: pointer;
    user-select: none;
}

.navbar > ul > .post > button:hover {
    opacity: 0.9;
}
.navbar > ul > .post > button:active {
    opacity: 0.8;
}
```

**Key takeaways:**
- `border-radius: 3rem` on a short element — creates a pill-shaped button.
- `user-select: none` — prevents the button text from being selectable.

---

## Step 9 — Navbar: User Profile Section

A user card pinned to the bottom of the navbar.

### `index.html` — Add after the Post `<li>`, still inside `<ul>`:

```html
<!-- User Profile button -->
<li class="user">
    <img class="user-profilepic" src="/assets/images/profile_pics/default.png" alt="Profile Picture" tabindex="0" role="button">
    <p>
        <span class="name">Dhruv Dhaduk</span>
        <span class="username">@dhruvdhaduk0</span>
    </p>
    <img class="ellipses" src="/assets/icons/ellipses.svg" alt="More about profile" tabindex="0" role="button">
</li>
```

### `styles/navbar.css` — Add:

```css
/* User Profile button */
.navbar > ul > .user {
    width: 100%;
    margin-top: auto;
    display: flex;
    justify-content: start;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem;
}

.navbar > ul > .user > .user-profilepic {
    width: 2.75rem;
    aspect-ratio: 1;
    border-radius: 100%;
    cursor: pointer;
}
.navbar > ul > .user > .user-profilepic:hover {
    opacity: 0.9;
}
.navbar > ul > .user > .user-profilepic:active {
    opacity: 0.8;
}

.navbar > ul > .user > p {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.navbar > ul > .user > p > .name {
    font-weight: bold;
}

.navbar > ul > .user > p > .username {
    font-size: 0.85rem;
    color: #a7a7a7;
}

.navbar > ul > .user > .ellipses {
    margin-left: auto;
    width: 1.5rem;
    aspect-ratio: 1;
    cursor: pointer;
}
.navbar > ul > .user > .ellipses:hover {
    opacity: 0.9;
}
.navbar > ul > .user > .ellipses:active {
    opacity: 0.8;
}
```

**Key takeaways:**
- `margin-top: auto` — this is the magic trick! In a flex column, it pushes this element all the way to the bottom.
- `margin-left: auto` on the ellipsis — pushes it to the far right within its flex row.

---

## Step 10 — Header: Logo (Mobile) & Tabs

The header has a logo (visible only on mobile) and two tabs: "For you" and "Following".

### Create `styles/header.css` and link it in the `<head>`:

```html
<link rel="stylesheet" href="/styles/header.css">
```

### `index.html` — Replace "Header" inside `<header>` with:

```html
<!-- Main Logo of X. Will be shown on small screens only -->
<div class="logo">
    <img src="/assets/icons/x.svg" alt="X (formerly Twitter)">
</div>

<!-- Tabs -->
<div class="tabs" role="tablist">
    <div class="tab-for-you" role="tab" tabindex="0" aria-controls="feed-for-you">For you</div>
    <div class="tab-following" role="tab" tabindex="0" aria-controls="feed-following">Following</div>
</div>
```

### `styles/header.css`

```css
/* Set the variables to control sizes for different screen sizes. */
.header {
    --logo-section-height: 3.5rem;
    --logo-size: 1.65rem;
    --tabs-section-height: 4rem;
    --tabs-font-size: 1.1rem;
}

/* Logo section for smaller screens */
.header > .logo {
    width: 100%;
    height: var(--logo-section-height);
    display: flex;
    justify-content: center;
    align-items: center;
}

.header > .logo > img {
    width: var(--logo-size);
    aspect-ratio: 1;
    cursor: pointer;
}

/* Hide the main logo for larger screens. */
@media (min-width: 600px) {
    .header > .logo {
        display: none;
    }
}

/* Tabs section */
.header > .tabs {
    width: 100%;
    height: var(--tabs-section-height);
    display: flex;
}

.header > .tabs > div {
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: var(--tabs-font-size);
    cursor: pointer;
    user-select: none;
}
.header > .tabs > div:hover {
    background-color: var(--hover-background-color);
}
.header > .tabs > div:active {
    background-color: var(--active-background-color);
}

.header > .tabs > .tab-for-you {
    font-weight: bold;
    position: relative;
}

/* Underline showing currently active tab */
.header > .tabs > .tab-for-you::after {
    content: '';
    width: 8rem;
    max-width: 100%;
    height: 5px;
    border-radius: 5px;
    background-color: var(--primary-blue-color);
    position: absolute;
    bottom: 0;
}

.header > .tabs > .tab-following {
    color: #b1b1b1;
}
```

**Key takeaways:**
- `flex: 1` on each tab — both tabs share equal width.
- `::after` pseudo-element — creates the blue underline without adding extra HTML.
- `position: relative` + `position: absolute` — the underline is positioned at the bottom of the tab.
- The logo is hidden on desktop (`min-width: 600px`) since the navbar logo is visible.

---

## Step 11 — Sidebar: Search Bar

Now let's build the right sidebar, starting with the search input.

### Create `styles/sidebar.css` and link it in the `<head>`:

```html
<link rel="stylesheet" href="/styles/sidebar.css">
```

### `index.html` — Replace "Sidebar" inside `<aside>` with:

```html
<input type="text" class="search-bar" placeholder="Search" aria-label="Search">
```

### `styles/sidebar.css`

```css
.aside {
    padding: 1.5rem;
}

/* Search bar */
.search-bar {
    background-color: black;
    color: white;
    width: 100%;
    height: 2.75rem;
    font-size: 1.1rem;
    border-radius: 2.5rem;
    border: 1px solid #3b3b3b;

    background-image: url('/assets/icons/search_darker.svg');
    background-size: 1.5rem;
    background-repeat: no-repeat;
    background-position: 1rem center;
    padding-left: 3rem;
}

.search-bar:focus {
    outline: none;
    border: 1px solid var(--primary-blue-color);
}
```

**Key takeaways:**
- `background-image` on an `<input>` — a neat trick to add a search icon inside the input without extra HTML.
- `padding-left: 3rem` — makes room for the icon so text doesn't overlap it.
- Custom `:focus` style — replaces the default browser outline with a blue border.

---

## Step 12 — Sidebar: Subscribe to Premium Card

A card with a heading, description, and a button.

### `index.html` — Add after the search input, inside `<aside>`:

```html
<section class="subscribe">
    <p class="heading" role="heading">Subscribe to Premium</p>
    <p class="description">Subscribe to unlock new features and if eligible, receive a share of revenue.</p>
    <button class="subscribe-btn">
        Subscribe
    </button>
</section>
```

### `styles/sidebar.css` — Add:

```css
/* Subscribe to Premium section */
.aside > .subscribe {
    margin-top: 1.5rem;
    padding: 1rem;
    border: 1px solid var(--border-color);
    border-radius: 1rem;
}

.aside > .subscribe > .heading {
    font-size: 1.5rem;
    font-weight: bold;
}

.aside > .subscribe > .description {
    font-size: 1rem;
    line-height: 1.5;
    padding-top: 0.75rem;
    padding-bottom: 0.75rem;
}

.aside > .subscribe > .subscribe-btn {
    background-color: var(--primary-blue-color);
    font-size: 1.1rem;
    font-weight: bold;
    border: none;
    height: 3rem;
    padding-left: 2rem;
    padding-right: 2rem;
    border-radius: 3rem;
    cursor: pointer;
    user-select: none;
}
.aside > .subscribe > .subscribe-btn:hover {
    opacity: 0.9;
}
.aside > .subscribe > .subscribe-btn:active {
    opacity: 0.8;
}
```

**Key takeaways:**
- `line-height: 1.5` — gives the description text comfortable spacing.
- `border-radius: 1rem` — rounds the card's corners.
- `.subscribe-btn` uses the blue color from our CSS variable.

---

## Step 13 — Sidebar: Trending Section

A list of trending topics.

### `index.html` — Add after the subscribe `<section>`, inside `<aside>`:

```html
<section class="trending">
    <p class="heading" role="heading">What's happening</p>
    <ul class="trending-list">
        <li>
            <article>
                <p class="category">Trending in India</p>
                <p class="hashtag" tabindex="0">#Budget2025</p>
                <p class="posts-count">17.2K posts</p>
            </article>
        </li>
        <li>
            <article>
                <p class="category">Politics · Trending</p>
                <p class="hashtag" tabindex="0">BRICS</p>
                <p class="posts-count">43.4K posts</p>
            </article>
        </li>
        <li>
            <article>
                <p class="category">Politics · Trending</p>
                <p class="hashtag" tabindex="0">Maa Lakshmi</p>
                <p class="posts-count">11.9K posts</p>
            </article>
        </li>
        <li>
            <article>
                <p class="category">Trending in India</p>
                <p class="hashtag" tabindex="0">परमवीर चक्र</p>
                <p class="posts-count">2,861 posts</p>
            </article>
        </li>
    </ul>
</section>
```

### `styles/sidebar.css` — Add:

```css
/* Trending section */
.aside > .trending {
    margin-top: 1.5rem;
    padding: 1rem;
    border: 1px solid var(--border-color);
    border-radius: 1rem;
}

.aside > .trending > .heading {
    font-size: 1.5rem;
    font-weight: bold;
}

.aside > .trending > .trending-list {
    list-style-type: none;
}

.aside > .trending > .trending-list > li {
    padding-top: 0.65rem;
    padding-bottom: 0.65rem;
}

.aside > .trending > .trending-list .category {
    font-size: 0.85rem;
    font-weight: 600;
    color: #b1b1b1;
}

.aside > .trending > .trending-list .hashtag {
    font-weight: bold;
    font-size: 0.95rem;
    padding-top: 0.2rem;
    padding-bottom: 0.2rem;
    cursor: pointer;
}

.aside > .trending > .trending-list .posts-count {
    font-size: 0.8rem;
    color: #b1b1b1;
}
```

**Key takeaways:**
- Each trending item has 3 lines: category (grey, small), hashtag (bold), and post count (grey, smallest).
- `list-style-type: none` — removes the default bullets/numbers.

---

## Step 14 — Sidebar: Who to Follow Section

Suggested accounts to follow.

### `index.html` — Add after the trending `<section>`, inside `<aside>`:

```html
<section class="who-to-follow">
    <p class="heading" role="heading">Who to follow</p>
    <ul class="who-to-follow-list">
        <li>
            <img src="https://pbs.twimg.com/profile_images/2828597835/0f1840e9c2fbafa93fe6f0d7ccf64a3e_400x400.jpeg" loading="lazy" alt="Profile picture of @Linus__Torvalds" tabindex="0">
            <p>
                <span class="name">Linus Torvalds</span>
                <span class="username">@Linus__Torvalds</span>
            </p>
            <button>
                Follow
            </button>
        </li>
        <li>
            <img src="https://pbs.twimg.com/profile_images/1613151603564986368/dZoNeRKn_400x400.jpg" loading="lazy" alt="Profile picture of @teej_dv" tabindex="0">
            <p>
                <span class="name">teej dv</span>
                <span class="username">@teej_dv</span>
            </p>
            <button>
                Follow
            </button>
        </li>
    </ul>
</section>
```

### `styles/sidebar.css` — Add:

```css
/* Follow Suggestion section */
.aside > .who-to-follow {
    margin-top: 1.5rem;
    padding: 1rem;
    border: 1px solid var(--border-color);
    border-radius: 1rem;
}

.aside > .who-to-follow > .heading {
    font-size: 1.5rem;
    font-weight: bold;
}

.aside > .who-to-follow > .who-to-follow-list {
    list-style-type: none;
}

.aside > .who-to-follow > .who-to-follow-list > li {
    padding-top: 0.65rem;
    padding-bottom: 0.65rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.aside > .who-to-follow > .who-to-follow-list > li > img {
    width: 2.5rem;
    aspect-ratio: 1;
    border-radius: 100%;
    flex: none;
    cursor: pointer;
}
.aside > .who-to-follow > .who-to-follow-list > li > img:hover {
    opacity: 0.9;
}
.aside > .who-to-follow > .who-to-follow-list > li > img:active {
    opacity: 0.8;
}

.aside > .who-to-follow > .who-to-follow-list > li > p {
    flex: 1;
    display: flex;
    flex-direction: column;
}

.aside > .who-to-follow > .who-to-follow-list > li > p > .name {
    font-weight: bold;
}

.aside > .who-to-follow > .who-to-follow-list > li > p > .username {
    font-size: 0.8rem;
    color: #a0a0a0;
}

.aside > .who-to-follow > .who-to-follow-list > li > button {
    flex: none;
    background-color: white;
    color: black;
    font-size: 1.1rem;
    font-weight: bold;
    height: 2rem;
    border-radius: 2rem;
    border: none;
    padding-left: 1rem;
    padding-right: 1rem;
    user-select: none;
    cursor: pointer;
}
.aside > .who-to-follow > .who-to-follow-list > li > button:hover {
    opacity: 0.9;
}
.aside > .who-to-follow > .who-to-follow-list > li > button:active {
    opacity: 0.8;
}
```

**Key takeaways:**
- Each follow suggestion is a flex row: profile pic, name/username column, follow button.
- `flex: none` on the image and button — they keep their size, the name column stretches (`flex: 1`).
- `loading="lazy"` on images — browser only loads them when they're about to become visible, improving performance.

---

## Step 15 — Feed: New Post Composer

The "What is happening?!" input area at the top of the feed.

### Create `styles/newpost.css` and link it in the `<head>`:

```html
<link rel="stylesheet" href="/styles/newpost.css">
```

### `index.html` — Replace "Feed" inside `<div class="feed">` with:

```html
<!-- Create a new post -->
<div class="newpost">
    <img class="user-profilepic" src="/assets/images/profile_pics/default.png" alt="Profile Picture" tabindex="0" role="button">
    <div class="input-container">
        <textarea name="newpost" placeholder="What is happening?!"></textarea>
        <div class="buttons">
            <img src="/assets/icons/media.svg" alt="Add Media" tabindex="0" role="button" aria-label="Add Media">
            <img src="/assets/icons/gif.svg" alt="Add GIF" tabindex="0" role="button" aria-label="Add GIF">
            <img src="/assets/icons/xai_blue.svg" alt="Ask Grok" tabindex="0" role="button" aria-label="Ask Grok">
            <img src="/assets/icons/poll.svg" alt="Add Poll" tabindex="0" role="button" aria-label="Add Poll">
            <img src="/assets/icons/emoji.svg" alt="Add Emoji" tabindex="0" role="button" aria-label="Add Emoji">
            <img src="/assets/icons/schdule.svg" alt="Schedule Post" tabindex="0" role="button" aria-label="Schedule Post">
            <img src="/assets/icons/location.svg" alt="Add Location" tabindex="0" role="button" aria-label="Add Location">

            <button class="post-btn">
                Post
            </button>
        </div>
    </div>
</div>

<div class="feed-for-you" id="feed-for-you">
</div>
<div class="feed-following" id="feed-following"></div>
```

### `styles/newpost.css`

```css
.newpost {
    display: flex;
    align-items: start;
    max-width: 100%;
    border-bottom: 2px solid var(--border-color);

    --profile-pic-size: 3rem;
    --spacing: 1rem;
}

/* Profile Picture */
.newpost > .user-profilepic {
    flex: none;
    width: var(--profile-pic-size);
    aspect-ratio: 1;
    border-radius: 100%;
    cursor: pointer;
    margin: var(--spacing);
}
.newpost > .user-profilepic:hover {
    opacity: 0.9;
}
.newpost > .user-profilepic:active {
    opacity: 0.8;
}

.newpost > .input-container {
    flex: 1;
    padding: var(--spacing);
    padding-left: 0;
    display: flex;
    flex-direction: column;
}

/* Text Area */
.newpost > .input-container > textarea {
    resize: none;
    width: 100%;
    height: 5rem;
    background-color: black;
    color: white;
    font-size: 1.25rem;
    padding: 0.5rem;
    border: none;
    border-radius: 0.5rem;
}
.newpost > .input-container > textarea:focus {
    outline: none;
    border: 1px solid var(--primary-blue-color);
}

/* Buttons */
.newpost > .input-container > .buttons {
    display: flex;
    align-items: center;
    justify-content: start;
    flex-wrap: wrap;
    gap: 1rem;
    padding-top: 0.5rem;
}

.newpost > .input-container > .buttons > img {
    width: 1.35rem;
    aspect-ratio: 1;
    cursor: pointer;
}

.newpost > .input-container > .buttons > .post-btn {
    margin-left: auto;
    background-color: white;
    color: black;
    font-size: 1.1rem;
    font-weight: bold;
    height: 2rem;
    border-radius: 2rem;
    border: none;
    padding-left: 1rem;
    padding-right: 1rem;
    user-select: none;
    cursor: pointer;
}
.newpost > .input-container > .buttons > .post-btn:hover {
    opacity: 0.9;
}
.newpost > .input-container > .buttons > .post-btn:active {
    opacity: 0.8;
}
```

**Key takeaways:**
- Same flex row pattern: profile pic (fixed) + input area (flexible).
- `resize: none` — prevents users from manually resizing the textarea.
- `margin-left: auto` on the Post button — pushes it to the far right of the toolbar.
- `flex-wrap: wrap` — icon buttons wrap to the next line on small screens instead of overflowing.

---

## Step 16 — Feed: A Single Post (Text Only)

Now the core piece — a tweet/post. We'll start with a text-only post.

### Create `styles/feed.css` and link it in the `<head>`:

```html
<link rel="stylesheet" href="/styles/feed.css">
```

### `index.html` — Add inside `<div class="feed-for-you">`:

```html
<div class="post">
    <div class="post-profile-pic">
        <img
            src="https://pbs.twimg.com/profile_images/1909353910130950147/EeSGdgA5_400x400.jpg"
            alt="Profile Picture of @theo"
            loading="lazy"
            tabindex="0"
            role="button"
        >
    </div>
    <div class="post-body">
        <p>
            <span class="post-profile-name">Theo - t3.gg</span>
            <span class="post-username">@theo</span>
            <span class="post-middle-dot">·</span>
            <span class="post-upload-time">21 Feb 25</span>
        </p>
        <div class="post-content">
            <p>Of the best devs I know, ~50% have CS degrees</p>
            <p>Of the worst devs I know, ~100% have CS degrees</p>
        </div>
    </div>
</div>
```

### `styles/feed.css`

```css
/* Set the variables to control sizes for different screen sizes. */
.feed {
    --profile-pic-size: 3rem;
    --post-padding: 1rem;
}

.feed .post {
    padding-left: var(--post-padding);
    padding-right: var(--post-padding);
    border-bottom: 1px solid var(--border-color);
    display: flex;
    gap: var(--post-padding);
}

/* Profile picture section */
.feed .post-profile-pic,
.feed .post-body {
    padding-top: var(--post-padding);
    padding-bottom: var(--post-padding);
}

.feed .post-profile-pic {
    flex: none;
    width: var(--profile-pic-size);
    display: flex;
    align-items: start;
    justify-content: center;
}

.feed .post-profile-pic > img {
    width: 100%;
    aspect-ratio: 1;
    border-radius: 100%;
    cursor: pointer;
}
.feed .post-profile-pic > img:hover {
    opacity: 0.9;
}
.feed .post-profile-pic > img:active {
    opacity: 0.8;
}

/* Post Body */
.feed .post-body {
    flex: 1;
}

.feed .post-profile-name {
    font-weight: bold;
}

.feed .post-username {
    font-size: 0.95rem;
    color: #b1b1b1;
}

.feed .post-tick {
    width: 1rem;
    aspect-ratio: 1;
}

.feed .post-middle-dot {
    font-weight: bold;
    color: #b1b1b1;
    padding-left: 0.25rem;
    padding-right: 0.25rem;
}

.feed .post-upload-time {
    font-size: 0.95rem;
    color: #b1b1b1;
}

.feed .post-content > p {
    line-height: 1.35;
    padding-top: 0.75rem;
}

.feed .post-content > p .highlight {
    color: var(--primary-blue-color);
    cursor: pointer;
}
```

**Key takeaways:**
- Same familiar flex row: profile pic (fixed width) + post body (flexible).
- The header line of each post (name · time) is styled inline using `<span>` elements.
- `.highlight` class — used for hashtags and @mentions, colored in X blue.
- `border-bottom` on each `.post` — creates the dividing line between posts.

---

## Step 17 — Feed: Post Images (1 / 2 / 3 / 4 Image Layouts)

X supports different image grid layouts depending on how many images a post has.

### Example HTML — Post with a verified tick and 4 images

Add another post inside `<div class="feed-for-you">`:

```html
<div class="post">
    <div class="post-profile-pic">
        <img
            src="https://pbs.twimg.com/profile_images/1799505527229087744/HnyGW4lp_400x400.jpg"
            alt="Profile picture of @cneuralnetwork"
            loading="lazy"
            tabindex="0"
            role="button"
        >
    </div>
    <div class="post-body">
        <p>
            <span class="post-profile-name">neural nets.</span>
            <span class="post-username">@cneuralnetwork</span>
            <img class="post-tick" src="/assets/icons/blue_tick.svg" alt="Blue Tick" loading="lazy">
            <span class="post-middle-dot">·</span>
            <span class="post-upload-time">03 Feb 25</span>
        </p>
        <div class="post-content">
            <p>some really great wallpapers i found today</p>
            <div class="post-images post-images-4">
                <div class="post-img-holder">
                    <img src="https://pbs.twimg.com/media/GizmwY1bAAAGvDL?format=jpg&name=large" alt="Post image 1" loading="lazy" tabindex="0">
                </div>
                <div class="post-img-holder">
                    <img src="https://pbs.twimg.com/media/GizmwYzbgAAnzLm?format=jpg&name=large" alt="Post image 2" loading="lazy" tabindex="0">
                </div>
                <div class="post-img-holder">
                    <img src="https://pbs.twimg.com/media/GizmwY3bAAAyZpB?format=jpg&name=large" alt="Post image 3" loading="lazy" tabindex="0">
                </div>
                <div class="post-img-holder">
                    <img src="https://pbs.twimg.com/media/GizmwY1aMAAlQuW?format=jpg&name=large" alt="Post image 4" loading="lazy" tabindex="0">
                </div>
            </div>
        </div>
    </div>
</div>
```

### Example HTML — Post with 1 image

```html
<div class="post-images post-images-1">
    <img src="https://pbs.twimg.com/media/Gh9Rdxoa0AAeY7M?format=jpg&name=large" alt="Post image 1" loading="lazy" tabindex="0">
</div>
```

### Example HTML — Post with 2 images

```html
<div class="post-images post-images-2">
    <div class="post-img-holder">
        <img src="..." alt="Post image 1" loading="lazy" tabindex="0">
    </div>
    <div class="post-img-holder">
        <img src="..." alt="Post image 2" loading="lazy" tabindex="0">
    </div>
</div>
```

### Example HTML — Post with 3 images (1 tall left + 2 stacked right)

```html
<div class="post-images post-images-3">
    <div class="post-img-container-left">
        <div class="post-img-holder">
            <img src="..." alt="Post image 1" loading="lazy" tabindex="0">
        </div>
    </div>
    <div class="post-img-container-right">
        <div class="post-img-holder">
            <img src="..." alt="Post image 2" loading="lazy" tabindex="0">
        </div>
        <div class="post-img-holder">
            <img src="..." alt="Post image 3" loading="lazy" tabindex="0">
        </div>
    </div>
</div>
```

### `styles/feed.css` — Add:

```css
/* Post images */
.feed .post-images {
    margin-top: 0.75rem;
    width: 100%;
    border: 1px solid var(--border-color);
    border-radius: 1rem;
    overflow: hidden;
}

.feed .post-images img {
    cursor: pointer;
}

/* 1 image: just stretch to full width */
.feed .post-images-1 > img {
    display: block;
    width: 100%;
}

/* 2, 3, 4 images: CSS Grid with 2 columns */
.feed .post-images-2,
.feed .post-images-3,
.feed .post-images-4
{
    display: grid;
    gap: 0.35rem;
    grid-template-columns: 1fr 1fr;
}

.feed .post-images-2 > .post-img-holder {
    aspect-ratio: 8 / 9;
}

.feed .post-images-4 > .post-img-holder {
    aspect-ratio: 16 / 9;
}

/* 3 images: left column is one tall image, right column has 2 stacked images */
.feed .post-images-3 .post-img-container-left {
    aspect-ratio: 8 / 9;
}
.feed .post-images-3 .post-img-container-left .post-img-holder {
    aspect-ratio: 8 / 9;
}

.feed .post-images-3 .post-img-container-right {
    display: grid;
    flex-direction: column;
    gap: 0.35rem;
}
.feed .post-images-3 .post-img-container-right .post-img-holder {
    aspect-ratio: 16 / 9;
}

/* Make all multi-image images cover their containers */
.feed .post-images-2 img,
.feed .post-images-3 img,
.feed .post-images-4 img
{
    display: block;
    width: 100%;
    height: 100%;
    object-fit: cover;
}
```

**Key takeaways:**
- `display: grid; grid-template-columns: 1fr 1fr;` — creates a 2-column grid. Each column takes equal space.
- `aspect-ratio` — controls the shape of image containers (tall vs wide).
- `object-fit: cover` — images fill their container without distortion, cropping if needed.
- `overflow: hidden` on the parent — clips the images to the rounded corners.
- Different classes (`post-images-1`, `-2`, `-3`, `-4`) — allows different layouts without JavaScript.

---

## Step 18 — Feed: Post Action Buttons

Every post has action buttons: Comment, Retweet, Like, Views, Bookmark, Share.

### `index.html` — Add inside a post's `<div class="post-body">`, after `<div class="post-content">`:

```html
<div class="post-buttons">
    <button>
        <img src="/assets/icons/comment.svg" alt="Comment" loading="lazy">
        170
    </button>
    <button>
        <img src="/assets/icons/retweet.svg" alt="Retweet" loading="lazy">
        206
    </button>
    <button>
        <img src="/assets/icons/like.svg" alt="Like" loading="lazy">
        4.4K
    </button>
    <button>
        <img src="/assets/icons/views.svg" alt="Views" loading="lazy">
        205.3K
    </button>
    <div class="last-buttons">
        <button>
            <img src="/assets/icons/bookmark_darker.svg" alt="Bookmark" loading="lazy">
        </button>
        <button>
            <img src="/assets/icons/share.svg" alt="Share" loading="lazy">
        </button>
    </div>
</div>
```

### `styles/feed.css` — Add:

```css
/* Post button panel */
.feed .post-buttons {
    margin-top: 0.75rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.feed .post-buttons button {
    background-color: black;
    color: #a1a1a1;
    border: none;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 0.25rem;
    cursor: pointer;
}

.feed .post-buttons .last-buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
}

.feed .post-buttons img {
    width: 1rem;
    height: 1rem;
}
```

**Key takeaways:**
- `justify-content: space-between` — evenly distributes buttons across the full width.
- The last two buttons (Bookmark, Share) are grouped in a `last-buttons` div so they sit together on the right.
- Each button is a flex container itself — icon and count sit side by side.

---

## Step 19 — Feed: Threads (Reply Chains)

When a post has a reply shown directly below it, X draws a connecting thread line between the profile pictures.

### `index.html` — Add a post with `has-a-reply` class followed by one with `is-a-reply`:

```html
<div class="post has-a-reply">
    <div class="post-profile-pic">
        <img
            src="https://pbs.twimg.com/profile_images/1903120400462249984/OVoMUTgQ_400x400.jpg"
            alt="Profile Picture of @ShachiGambhir"
            loading="lazy"
            tabindex="0"
            role="button"
        >
    </div>
    <div class="post-body">
        <p>
            <span class="post-profile-name">Sachi</span>
            <span class="post-username">@ShachiGambhir</span>
            <span class="post-middle-dot">·</span>
            <span class="post-upload-time">22 Jan 25</span>
        </p>
        <div class="post-content">
            <p>On a lookout for an office hand bag.</p>
            <p>Please drop in suggestions.</p>
        </div>
        <!-- post-buttons here -->
    </div>
</div>

<div class="post is-a-reply">
    <div class="post-profile-pic">
        <img
            src="https://pbs.twimg.com/profile_images/2005698051093180416/TiOcBPWc_400x400.jpg"
            alt="Profile Picture of @adii_kris"
            loading="lazy"
            tabindex="0"
            role="button"
        >
    </div>
    <div class="post-body">
        <p>
            <span class="post-profile-name">Adithiya Krishna</span>
            <span class="post-username">@adii_kris</span>
            <img class="post-tick" src="/assets/icons/blue_tick.svg" alt="Blue Tick" loading="lazy">
            <span class="post-middle-dot">·</span>
            <span class="post-upload-time">22 Jan 25</span>
        </p>
        <div class="post-content">
            <div class="post-images post-images-1">
                <img src="https://pbs.twimg.com/media/Gh5vmvybwAAVwh7?format=jpg&name=large" alt="Post image 1" loading="lazy" tabindex="0">
            </div>
        </div>
        <!-- post-buttons here -->
    </div>
</div>
```

### `styles/feed.css` — Add:

```css
.feed .post.has-a-reply {
    border: none;
}

/* Thread line going DOWN from the original post's profile pic */
.feed .post.has-a-reply .post-profile-pic {
    position: relative;
    --thread-color: #363636;
}
.feed .post.has-a-reply .post-profile-pic::after {
    content: "";
    background-color: var(--thread-color);
    width: 2px;
    height: calc(100% - 3rem);
    position: absolute;
    top: 3rem;
    z-index: -1;
}

/* Thread line going UP to the reply's profile pic */
.feed .post.is-a-reply .post-profile-pic {
    position: relative;
    --thread-color: #363636;
}
.feed .post.is-a-reply .post-profile-pic::before {
    content: "";
    background-color: var(--thread-color);
    width: 2px;
    height: 3rem;
    position: absolute;
    top: 0;
    z-index: -1;
}
```

**Key takeaways:**
- `::after` on the parent post — draws a line from below the profile pic to the bottom of the post.
- `::before` on the reply post — draws a line from the top of the cell down to the profile pic.
- Together they create a continuous vertical thread line connecting the two posts.
- `z-index: -1` — puts the line behind the profile picture so it doesn't overlap.
- `border: none` on `has-a-reply` — removes the divider between connected posts.

---

## Step 20 — Floating Elements: Grok Button & Message Box

These float over the page content using `position: fixed`.

### `index.html` — Add before `</body>`:

```html
<button class="grok-btn">
    <img src="/assets/icons/xai.svg" alt="Grok Icon" loading="lazy">
    <span>GROK</span>
</button>

<div class="message-box">
    <p>Messages</p>
    <img src="/assets/icons/new_message.svg" alt="Send New Message" loading="lazy" tabindex="0" role="button">
    <img src="/assets/icons/up_arrow_double.svg" alt="Expand Message box" loading="lazy" tabindex="0" role="button">
</div>
```

### `styles/index.css` — Add:

```css
.grok-btn {
    position: fixed;
    bottom: 5rem;
    right: 2rem;
    width: 4rem;
    height: 4rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: black;
    color: white;
    border: 1px solid var(--border-color);
    border-radius: 1rem;
    box-shadow: 0 0 20px 1px #ffffff50;
    cursor: pointer;
}
.grok-btn:hover {
    opacity: 0.9;
}
.grok-btn:active {
    opacity: 0.8;
}

.grok-btn > img {
    width: 2rem;
    aspect-ratio: 1;
}
.grok-btn > span {
    font-size: 0.6rem;
    font-weight: 600;
}

.message-box {
    position: fixed;
    bottom: 0;
    right: 2rem;
    width: 25rem;
    height: 3.5rem;
    display: flex;
    justify-content: start;
    align-items: center;
    padding-left: 1rem;
    padding-right: 1rem;
    gap: 1rem;
    background-color: black;
    border: 1px solid var(--border-color);
    border-top-left-radius: 1rem;
    border-top-right-radius: 1rem;
    box-shadow: 0 0 20px 1px #ffffff50;
}

.message-box > p {
    font-size: 1.5rem;
    font-weight: bold;
}

.message-box > img {
    width: 1.5rem;
    aspect-ratio: 1;
    cursor: pointer;
}
.message-box > img:hover {
    opacity: 0.9;
}
.message-box > img:active {
    opacity: 0.8;
}

.message-box > img:nth-child(2) {
    margin-left: auto;
}
```

**Key takeaways:**
- `position: fixed` — these elements stay in place even when the user scrolls.
- `bottom: 0; right: 2rem;` — anchors the message box to the bottom-right corner.
- `box-shadow: 0 0 20px 1px #ffffff50` — a subtle white glow around the elements.
- `#ffffff50` — hex color with alpha (50 = ~31% opacity).
- `nth-child(2)` with `margin-left: auto` — pushes the first icon to the far right, aligning the second icon next to it.

---

## Step 21 — Responsive: Hide Sidebar on Medium Screens

When the screen is narrower than 1100px, hide the sidebar to give the feed more room.

### `styles/index.css` — Add at the bottom:

```css
/*
 * Remove the aside section when screen width is less than 1100px.
 * Therefore, there will be enough space for main content (i.e. feed).
*/
@media (max-width: 1100px) {
    .aside {
        display: none;
    }
}
```

**Key takeaways:**
- `@media (max-width: 1100px)` — this CSS only applies when the viewport is 1100px or narrower.
- `display: none` — completely removes the sidebar from the layout (not just visually hidden).

---

## Step 22 — Responsive: Mobile Navbar at Bottom

On small screens (< 600px), move the navbar to the bottom of the screen like a mobile tab bar.

### `index.html` — Add `hide-on-sm` class to nav items that should be hidden on mobile:

Add the class `hide-on-sm` to these `<li>` elements: Logo, Bookmarks, Premium, Business, Profile, More, Post button, and User profile.

Example:
```html
<li class="logo hide-on-sm">...</li>
<li class="navitem hide-on-sm"><!-- Bookmarks -->...</li>
<li class="navitem hide-on-sm"><!-- Premium -->...</li>
<li class="navitem hide-on-sm"><!-- Business -->...</li>
<li class="navitem hide-on-sm"><!-- Profile -->...</li>
<li class="navitem hide-on-sm"><!-- More -->...</li>
<li class="post hide-on-sm">...</li>
<li class="user hide-on-sm">...</li>
```

### `styles/index.css` — Add at the bottom:

```css
/* Move the Navbar at the bottom when screen width is less than 600px. */
@media (max-width: 600px) {
    .main {
        /* Prevent Navbar from covering content at the bottom. */
        padding-bottom: 3.5rem;
    }

    .navbar {
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        width: 100%;
        height: 3.5rem;
    }

    .grok-btn {
        display: none;
    }

    .message-box {
        display: none;
    }
}
```

### `styles/navbar.css` — Add at the bottom:

```css
/*
 * Navbar moves to bottom when screen width is less than 600px.
 * Therefore, some items in navbar will be hidden and only icons will be shown for rest of the items.
*/
@media (max-width: 600px) {
    .navbar > ul {
        flex-direction: row;
        align-items: center;
        padding: 0;
        gap: 0;
        border-top: 1px solid #252525;
    }

    .navbar > ul > .navitem {
        flex: 1;
    }

    .navbar > ul > .navitem > a {
        justify-content: center;
        align-items: center;
    }

    .navbar > ul > .navitem img {
        width: 1.45rem;
    }

    /* Hide predefined items */
    .navbar > ul > .hide-on-sm {
        display: none;
    }

    /* Hide labels for nav items */
    .navbar > ul > .navitem span {
        display: none;
    }
}
```

### `styles/header.css` — Add at the bottom:

```css
/* Adjust the sizes for smaller screens (mobile devices) */
@media (max-width: 600px) {
    .header > .tabs {
        height: 3rem;
    }

    .header > .tabs > div {
        font-size: 1rem;
    }
}
```

### `styles/feed.css` — Add at the bottom:

```css
/* Adjust the sizes for smaller screens (mobile devices) */
@media (max-width: 600px) {
    .feed .post-profile-pic {
        width: 2.5rem;
    }

    .feed .post {
        padding-left: 0.6rem;
        padding-right: 0.6rem;
        gap: 0.6rem;
    }

    .feed .post-profile-pic,
    .feed .post-body {
        padding-top: 0.6rem;
        padding-bottom: 0.6rem;
    }
}
```

### `styles/newpost.css` — Add at the bottom:

```css
/* Adjust the sizes for smaller screens (mobile devices) */
@media (max-width: 600px) {
    .newpost > .user-profilepic {
        width: 2.5rem;
        margin: 0.6rem;
    }

    .newpost > .input-container {
        padding: 0.6rem;
    }
}
```

**Key takeaways:**
- On mobile, the navbar switches from `flex-direction: column` (vertical) to `flex-direction: row` (horizontal).
- `position: fixed; bottom: 0;` — pins the navbar to the bottom of the screen.
- `padding-bottom: 3.5rem` on main — prevents the fixed navbar from overlapping feed content.
- Items with `hide-on-sm` disappear on mobile, and labels are hidden — only icons remain.
- The Grok button and Message box are hidden on mobile since the navbar takes the bottom space.

---

## Step 23 — Scrollbar Styling

Custom webkit scrollbars to match the dark theme.

### `styles/index.css` — Add anywhere:

```css
*::-webkit-scrollbar {
    width: 5px;
}

.feed::-webkit-scrollbar {
    width: 6px;
}

*::-webkit-scrollbar-thumb {
    background-color: #2c2c2c;
    border-radius: 20px;
    cursor: pointer;
}

*::-webkit-scrollbar-thumb:hover {
    background-color: #999999;
}
```

**Key takeaways:**
- `::-webkit-scrollbar` — targets the scrollbar itself (only works in Webkit/Blink browsers like Chrome, Edge, Safari).
- `::-webkit-scrollbar-thumb` — the draggable part of the scrollbar.
- Thin scrollbars (5-6px) with dark thumbs match the X dark theme.

---

## Square Profile Pictures (Bonus)

Some accounts (like organizations) have square profile pictures instead of round ones.

### `index.html` — Add `square` class to the post-profile-pic div:

```html
<div class="post-profile-pic square">
    <img src="..." alt="..." loading="lazy" tabindex="0" role="button">
</div>
```

### `styles/feed.css` — Add:

```css
.feed .post-profile-pic.square > img {
    border-radius: 0.35rem;
}
```

This overrides the default `border-radius: 100%` (circle) with a small rounding.

---

## Final File Structure

After completing all steps, your project should look like this:

```
index.html
styles/
    index.css      ← Reset, layout, floating elements, responsive, scrollbar
    navbar.css     ← Navigation bar (logo, items, badge, post btn, user)
    header.css     ← Tabs (For you / Following)
    sidebar.css    ← Search, Subscribe, Trending, Who to follow
    feed.css       ← Posts, images, buttons, threads
    newpost.css    ← New post composer
assets/
    icons/         ← SVG icons
    images/        ← Profile pictures and cover images
```

---

## Recap: CSS Concepts Used

| Concept | Where Used |
|---|---|
| **Flexbox** | Page layout, navbar, post rows, buttons |
| **CSS Grid** | Image grids (2/3/4 images) |
| **CSS Variables** | Colors, sizes, spacing |
| **Position: fixed** | Grok button, message box, mobile navbar |
| **Position: absolute** | Notification badge, thread lines |
| **Pseudo-elements (::after, ::before)** | Tab underline, thread lines |
| **Media queries** | Responsive sidebar hiding, mobile navbar |
| **object-fit: cover** | Images fill containers without distortion |
| **margin-left/top: auto** | Push elements to edges within flexbox |
| **aspect-ratio** | Consistent image/icon dimensions |
| **box-sizing: border-box** | Predictable sizing everywhere |
