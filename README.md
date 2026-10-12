# Swish prototype (unofficial concept)

A clickable phone prototype of the Swish app with my proposed changes. It's one file, `index.html`, with no build step. The case study lives in the slide deck, not here.

Unofficial concept by Shreyas Jadhav. Not affiliated with Swish. All people and data are made up.

## Run it

Double-click `index.html`, or from this folder:

```
npx serve .
```

Then open the link it prints. Pick a person on the first screen to try their view:

- **Ananya** (customer): home with "Your usual", menu, cart, tracking, report a problem, wallet credit
- **Rohit** (customer): same flows, Noida
- **Meera** (kitchen lead): Swish Station complaints board, pause a dish, stop an order
- **Imran** (rider): order alert that keeps ringing, payday, shifts

Anything glowing yellow is new compared with the real app.

## How the code is laid out

- `<style>` at the top: colours are CSS variables in `:root` (Swish green is `--green`).
- `PEOPLE`: the four personas.
- `MENU`: dishes and prices.
- `S`: app state (cart, wallet, orders, paused dishes).
- `SCREENS`: one function per screen, keyed by route (`#home`, `#menu`, `#cart`, `#track`, `#orders`, `#issue`, `#wallet`, `#usual`, `#kitchen`, `#rider`, `#who`).
- `route()` draws the current screen; `bind()` wires the buttons.

## Visual fixes to make (12 Oct)

1. Replace the letter circles ("S", "CB", "RC") with food images on the category row and in the dish lists.
2. Make the offer card look like Swish's real "50% OFF UNLOCKED" banner.
3. Experiment A: add the moment the time slips, from "Arriving by 1:08" to "New time 1:15. Lunch rush, your food is being packed."
4. Experiment D: add a customer screen ("This kitchen is busy right now. Notify me when it's back", with fast dishes still orderable) and a Swish Station card before lunch with the forecast and prep list.
5. Decide whether the rider screens stay. The deck doesn't mention them.
6. Bug: with an empty cart, the banner reads "You saved ₹29 (₹0 with TRY50 + ₹29 delivery)". Hide the banner when the cart is empty.

## Put it on GitHub and Vercel (with Claude Code)

```
git init && git add . && git commit -m "Swish prototype"
gh repo create swish-prototype --public --source=. --push
npx vercel --prod
```
