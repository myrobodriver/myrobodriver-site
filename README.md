# MyRoboDriver

Public marketing site for [myrobodriver.com](https://myrobodriver.com/). Static HTML and CSS, published with GitHub Pages from `main`. There is no build step.

Open `index.html` in a browser, or from this folder run:

```bash
python3 -m http.server 4173
```

Darrell approves changes before anything is merged to `main`. Do not publish from a feature branch.

## What the site says

MyRoboDriver is an independent ride service in Tesla vehicles, now serving Middle Georgia. The tagline is “The chauffeur everyone can afford.”

Today, every ride has a safety driver in the car. Vehicles run Tesla’s FSD (Supervised), a driver-assistance system that needs active human supervision. The site does not call current rides driverless, fully autonomous, or unsupervised.

The only mention of driverless rides is one paragraph in Safety. It describes a possible later step, with no date and no guarantee, and says it depends on regulatory approval and on Tesla’s software.

The footer, About, and Safety state that MyRoboDriver is not affiliated with, endorsed by, or sponsored by Tesla, Inc., and that Tesla and FSD are trademarks of Tesla, Inc.

Contact is a `mailto:` form to myrobodriver@gmail.com, plus the phone number (478) 578-1169. The form is not connected to a server. The site does not link to any private app or backend.

## Copy to update when driverless launches

Search the page for `SUPERVISION-COPY` and update every marked line in one pass. The only future-plan sentence is the Safety paragraph that begins “Driverless rides, with no one in the driver’s seat”. Do not put that plan in the hero.

Marked copy, in page order:

- Meta description, Open Graph description, Open Graph image alt, and Twitter description: a safety driver is on every trip.
- JSON-LD `LocalBusiness` description: a safety driver is on every trip, and vehicles run FSD (Supervised).
- Hero: “A trained safety driver is in the car for every ride. Vehicles run Tesla’s FSD (Supervised) software, a driver-assistance system that needs active human supervision.”
- Hero badge: “The robot is our mascot. A safety driver is in the driver’s seat on every ride today.”
- Features intro: “a person responsible for the car”.
- Feature title “Safety driver on every ride” and “A person is in the driver’s seat for the whole trip.”
- Feature title “FSD (Supervised)” and “The car can assist with driving. FSD (Supervised) is driver assistance, and the safety driver supervises it.”
- How it works: “A Tesla arrives with a safety driver on board.”
- How it works: “FSD (Supervised) may assist with the drive. The safety driver supervises the trip and is responsible for the vehicle.”
- Safety heading “A person is responsible for the car” and “Every ride today has a safety driver in the car.”
- Safety: “The safety driver stays with the vehicle for the trip and can take over the controls.”
- Safety: “FSD (Supervised) is Tesla’s driver-assistance system. It needs active human supervision.”
- Safety, the only driverless-plan sentence: “Driverless rides, with no one in the driver’s seat, are only a possible later step. They are not available today. That step depends on regulatory approval and on Tesla’s software. There is no date and no guarantee.”
- FAQ: “Is a person in the driver’s seat?” and “Yes. Every ride includes a safety driver. The vehicle runs FSD (Supervised), which needs active human supervision.”
- FAQ: “What does FSD (Supervised) mean?” and “It is driver-assistance software from Tesla. It can help with the drive, and it needs a person supervising. The safety driver is responsible for the vehicle.”
- About: “A safety driver is in the car for every ride we offer today. The mascot is the brand mark. It is not a claim that the car operates without a person.”

`images/og.jpg` also reads “A safety driver on every ride.” Replace that image if that line changes.

## Notes for Darrell

- Public email: myrobodriver@gmail.com
- Public phone: (478) 578-1169
- Service area named on the site: Middle Georgia (Middle GA)
- A street address and a legal entity name were not provided, so the page does not invent them. The structured data names Georgia, USA, and Middle Georgia as the area served.
- Protected paths were left as they were: `auth/callback/`, `.well-known/appspecific/com.tesla.3p.public-key.pem`, `CNAME`, and `.nojekyll`. This repo has no `_headers` file, so none was added.

Photo and logo credits are in [CREDITS.md](CREDITS.md).
