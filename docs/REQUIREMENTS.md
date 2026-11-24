# MyRoboDriver requirements

This document records what the public site is today, the ride-request flow Darrell has approved for a later release, and the rule for updating copy if driverless rides ever become available. It does not change the live site.

Version 1 of the marketing site is approved and live on GitHub Pages from `main` at [myrobodriver.com](https://myrobodriver.com/).

## 1. Current state (v1, approved and live)

v1 is a static marketing site. There is no build step and no backend. The contact form opens the visitor’s email app. It does not store or send the message itself.

### Sections and brand

Single page with a sticky header, footer, and anchor navigation:

- Hero
- Features
- How it works
- Safety
- FAQ
- About
- Contact

The tagline, used as the hero headline and in the meta description and Open Graph text, is **The chauffeur everyone can afford.**

The palette is red, white, black, and grey, with red as the accent. The logo set is MyRoboDriver’s own artwork: the robot chauffeur mascot, the wordmark (“My” in red script, “Robo” outlined, “Driver” in black), a horizontal lockup, and favicon and circle icons. The car in the art has no badge. The site does not use Tesla logos or Tesla press assets.

Photographs are committed copies licensed for commercial use. Credits are in `CREDITS.md`.

### Service area and contact

- Service area named on the site: **Middle Georgia** (Middle GA). It appears in the hero, About, Contact, the footer, the meta description, and LocalBusiness structured data.
- Email: [myrobodriver@gmail.com](mailto:myrobodriver@gmail.com)
- Phone: [(478) 578-1169](tel:+14785781169)

A street address and a legal entity name are not published. Structured data names Middle Georgia as the area served, with the email, the telephone number, and Georgia, USA. It does not invent a street address.

### Supervision copy

Today, every ride has a safety driver in the car. Vehicles run Tesla’s FSD (Supervised), a driver-assistance system that needs active human supervision. The site does not call current rides driverless, fully autonomous, or unsupervised, and it does not overstate safety or capability.

Every line about the safety driver, supervision, or driverless plans is marked in `index.html` with `<!-- SUPERVISION-COPY -->`. The same lines are listed in the README section “Copy to update when driverless launches.”

Driverless rides (no one in the driver’s seat) are mentioned once, in Safety, and only as a possible later step. That sentence has no date and no guarantee, and it says the step depends on regulatory approval and on Tesla’s software. It is not in the hero, and it is not described as available now.

The Open Graph image also says “A safety driver on every ride.” That image is part of the same copy set.

### Hard rules

- MyRoboDriver is an independent company. The footer, About, and Safety say it is not affiliated with, endorsed by, or sponsored by Tesla, Inc., and that Tesla and FSD are trademarks of Tesla, Inc.
- FSD (Supervised) is described as driver assistance that needs active human supervision. A safety driver is on board for every ride offered today.
- Driverless operation is a future plan only, with no date. See section 3.
- Hosting is GitHub Pages from `main`, custom domain `myrobodriver.com` (`CNAME`).
- These paths stay as they are and stay served: `/auth/callback/`, `/.well-known/appspecific/` (including `com.tesla.3p.public-key.pem`), `CNAME`, and `.nojekyll`. There is no `_headers` file in this repo.
- The public site does not call, link to, or embed private dashboard pages. See ownership in section 2.

## 2. Planned: ride request flow

Darrell approved the flow below as-is. Improvements are expected later. Rates and pricing rules are not decided.

The intended flow:

1. The Contact / ride request form verifies the pickup and drop-off addresses (address validation and autocomplete).
2. It works out the route, distance, and estimated travel time.
3. It sends the request to Darrell’s private dashboard, where it shows up as a new ride request.
4. Darrell responds from the dashboard with a price. Rates and pricing rules are TBD and will be decided later.
5. The rider gets the price and can confirm or reject the ride.
6. When the rider confirms, the ride is added to Darrell’s calendar.

### Who owns what

| Part | Owner |
| --- | --- |
| Public ride-request form (the page the rider sees) | Marketing site (this repo, GitHub Pages) |
| Request API, storage, and calendar integration | MyRoboDriver backend |
| Request inbox and the price response Darrell sends | Private dashboard at dash.myrobodriver.com |

The marketing site must never call or embed private dashboard pages directly. The form talks only to a public backend endpoint. The dashboard is for Darrell, not for the rider’s browser.

v1 cannot do this flow. A static GitHub Pages site has nowhere to validate addresses, compute a route, store a request, or wait for a price. That work needs a backend endpoint. Until that exists, Contact stays the mailto form described in section 1.

### User stories

**Request a ride with checked addresses.** As a rider in Middle Georgia, I want the form to check my pickup and drop-off as I type, so I submit real places rather than a free-text guess.

**See the trip before I send it.** As a rider, I want the distance and estimated travel time for the route between those addresses, so I know what I am asking for. The page does not show a price at this step, because rates are not set yet.

**Send the request to Darrell.** As a rider, I want to submit that checked request so it appears as a new ride request in Darrell’s private dashboard.

**Answer with a price.** As Darrell, I want each new request in the dashboard inbox, and I want to reply with a price from there. The price is Darrell’s decision for that request until a rate model exists.

**Accept or decline.** As a rider, I want to receive the price and confirm or reject the ride.

**Book it when I confirm.** As a rider, when I confirm, I want the ride added to Darrell’s calendar. If I reject it, it is not added.

### Acceptance criteria

- The public form is part of the marketing site. It does not load, iframe, or link the rider to dash.myrobodriver.com or any other private dashboard URL.
- Pickup and drop-off use address validation and autocomplete. A request cannot be sent with an address the validator has not accepted.
- After both addresses are accepted, the rider sees a route summary with distance and estimated travel time before they send the request.
- Submitting creates a ride request that shows up as new in the dashboard inbox. The marketing site does not write to the dashboard itself. It calls the backend API. The backend stores the request and makes it visible on the dashboard.
- The stored request includes the validated addresses, the route summary, and the rider’s contact details from the form. It does not include a price until Darrell sets one.
- From the dashboard, Darrell can send one price for that request. There is no automatic fare in this release. Rates and pricing rules stay TBD.
- The rider can confirm or reject that price. Confirming adds the ride to Darrell’s calendar. Rejecting does not.
- A failed address check, route lookup, or submit shows an error on the form and does not create a dashboard request or a calendar event.
- v1 mailto behavior is replaced only when this flow is actually available. Until then, the live form stays the email form.

### Open questions

These are undecided. They should be answered before the flow is built.

- **Pricing and rate model.** How Darrell chooses a price, and whether any rules (minimum, per mile, per minute, area) will exist later. Not in this approved flow.
- **How the rider is notified.** Email, SMS, or both, for the price and for confirm or reject. The v1 address and phone number are myrobodriver@gmail.com and (478) 578-1169. Those are Darrell’s public contacts, not a decision about rider notifications.
- **Calendar provider.** Which calendar receives a confirmed ride, and who connects it.
- **Maps or geocoding provider, and API key handling.** Which service validates addresses and returns distance and travel time. Keys stay on the backend. They are not shipped in the GitHub Pages site.
- **Spam and abuse protection.** What stops scripted or repeated submissions. Not chosen yet.
- **Data privacy and retention.** What is stored, for how long, and who can see a request on the dashboard.
- **Backend endpoint.** GitHub Pages cannot run this flow. The public form needs a backend URL it is allowed to call. That endpoint is not dash.myrobodriver.com.

## 3. Future: driverless operation

Driverless rides are not offered. They remain a possible later step only, and only if regulators approve them and Tesla’s software supports them. There is no date and no guarantee.

When that changes, update every `<!-- SUPERVISION-COPY -->` line in `index.html`, the matching list in the README section “Copy to update when driverless launches,” and the “A safety driver on every ride” line on `images/og.jpg`. Do not describe driverless service as available in the hero before those lines are updated together.
