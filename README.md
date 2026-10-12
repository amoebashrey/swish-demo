# Swish prototype (unofficial concept)

A clickable phone prototype of the Swish app with my proposed changes. It's one file, `index.html`, plus food photos in `img/`. There's no build step. The case study lives in the slide deck, not here.

Unofficial concept by Shreyas Jadhav. Not affiliated with Swish. All people and data are made up.

## Run it

From this folder:

```
npx serve .
```

Then open the link it prints. Pick a person on the first screen to try their view:

- **Ananya** (customer): home, menu, dish page, cart, tracking, report a problem, wallet credit, "Your usual"
- **Rohit** (customer): same flows, Noida
- **Meera** (kitchen lead): Swish Station with the lunch forecast, complaints board, paused dish, orders on the line
- **Imran** (rider): order alert that keeps ringing, payday, shifts

Anything with a thin yellow outline and a **NEW** tag is new compared with the real app. Everything else copies the real app.

On a desktop the app sits in an iPhone frame (390 × 844 screen). Under 500 px wide it fills the screen instead.

## Recording links

Each link opens one state directly, so it can be recorded without clicking through. A link with parameters always starts from a clean state. Add `&new=0` to any link to hide the NEW tags.

| State | Link |
| --- | --- |
| Persona picker | `#who` |
| Home (Ananya) | `#home?person=ananya` |
| Home (Rohit) | `#home?person=rohit` |
| Home, account sheet | `#home?person=ananya&sheet=1` |
| Home, feedback after delivery | `#home?person=ananya&feedback=1` |
| Home, busy kitchen | `#home?person=ananya&busy=1` |
| Home, kitchen closed | `#home?person=ananya&closed=1` |
| Home with items in cart | `#home?person=ananya&cart=idli,chai` |
| Menu | `#menu?person=ananya` |
| Menu, one category | `#menu?person=ananya&cat=snacks` |
| Menu, busy kitchen | `#menu?person=ananya&busy=1` |
| Menu, kitchen closed | `#menu?person=ananya&closed=1` |
| Dish page | `#dish?person=ananya&id=idli` |
| Dish page, after adding | `#dish?person=ananya&id=idli&added=1` |
| Cart, one item | `#cart?person=ananya&cart=idli` |
| Cart, three items | `#cart?person=ananya&cart=idli,gulab,chai` |
| Cart, under ₹99 | `#cart?person=ananya&cart=chai` |
| Cart, coupon removed | `#cart?person=ananya&cart=idli&coupon=0` |
| Cart, empty | `#cart?person=ananya&cart=` |
| Tracking, just ordered | `#track?person=ananya&step=0` |
| Tracking, rider on the way | `#track?person=ananya&step=3` |
| Tracking, time slips to 1:15 | `#track?person=ananya&slip=1` |
| Tracking, delivered | `#track?person=ananya&step=4` |
| Orders | `#orders?person=ananya` |
| Report a problem | `#issue?person=ananya&order=4821` |
| Report, food wasn't good | `#issue?person=ananya&order=4821&type=quality&item=rajma` |
| Report, refund done | `#issue?person=ananya&order=4821&type=quality&item=rajma&done=1` |
| Report, something in my food | `#issue?person=ananya&order=4821&type=safety&item=rajma&photo=1` |
| Report, call within 30 minutes | `#issue?person=ananya&order=4821&type=safety&item=rajma&done=1` |
| Wallet | `#wallet?person=ananya` |
| Wallet, late credit arriving | `#wallet?person=ananya&credit=1` |
| Weekday reminder | `#usual?person=ananya` |
| Swish Station | `#kitchen?person=meera` |
| Rider | `#rider?person=imran` |

Add a link to the local address, for example `http://localhost:3000/#track?person=ananya&slip=1`.

Other parameters: `cart=idli:2,chai` sets quantities, `veg=1` turns on the Veg filter, `details=1` opens dish details.

## How the code is laid out

- `<style>` at the top: colours are CSS variables in `:root` (Swish green is `--green`). `.nw` and `.ntag` draw the NEW marker.
- `PEOPLE`: the four personas.
- `MENU`: dishes, prices, photos, and `prep` minutes. Dishes with 6 minutes or less count as fast when the kitchen is busy.
- `CATS`: the category row on home and the sub-tabs on the menu.
- `S`: app state (cart, coupon, wallet, orders, tracking, busy kitchen, feedback, paused dishes).
- `bill()`: TRY50 maths. 50% off up to ₹150 on orders of ₹99 or more, plus free delivery (₹29) and packaging (₹9). "You saved" is the sum of all three.
- `SCREENS`: one function per screen, keyed by route (`#who`, `#home`, `#menu`, `#dish`, `#cart`, `#track`, `#orders`, `#issue`, `#wallet`, `#usual`, `#kitchen`, `#rider`).
- `applyParams()`: reads the recording-link parameters.
- `render()` draws the current screen and runs the transition; `bind()` wires the buttons.

## Photo credits

Food photos are from [Unsplash](https://unsplash.com) under the Unsplash License, resized to 400 px.

- `img/bestseller.jpg`: Nizar Zulmi, https://unsplash.com/photos/UgckYUoc0tM
- `img/biryani.jpg`: Shreyak Singh, https://unsplash.com/photos/0j4bisyPo3M
- `img/brownie.jpg`: Umesh Soni, https://unsplash.com/photos/LDnmyOaA-ew
- `img/chaat.jpg`: Kalyani Akella, https://unsplash.com/photos/vQwXqWR4Q_E
- `img/chai.jpg`: Ananthan Chithiraikani, https://unsplash.com/photos/7-PQGUrIGOc
- `img/coffee.jpg`: Indra Projects, https://unsplash.com/photos/ma90umjzwT4
- `img/coldcoffee.jpg`: Jarek Ceborski, https://unsplash.com/photos/IhqDpFz7I8Q
- `img/fries.jpg`: Markus Winkler, https://unsplash.com/photos/9DEggBoY8CY
- `img/gourmet.jpg`: Rupa venketa vardhan, https://unsplash.com/photos/85gaOsWNsHo
- `img/gulab.jpg`: jaikishan patel, https://unsplash.com/photos/uwu2ZLDmX8k
- `img/idli.jpg`: Shreyak Singh, https://unsplash.com/photos/gFB1IPmH6RE
- `img/lassi.jpg`: Sebastian Coman Photography, https://unsplash.com/photos/rwBJaJdesGg
- `img/maggi.jpg`: ikhsan baihaqi, https://unsplash.com/photos/RwAXb8Hv_sU
- `img/momos.jpg`: shiv singh, https://unsplash.com/photos/Vj-J5xNjnxA
- `img/paneer.jpg`: La La, https://unsplash.com/photos/qYtfN2109Wg
- `img/pasta.jpg`: Ben Lei, https://unsplash.com/photos/flFd8L7_B3g
- `img/poha.jpg`: Zoshua Colah, https://unsplash.com/photos/_yxndM0wO8c
- `img/popcorn.jpg`: personalgraphic.com, https://unsplash.com/photos/CkgqmxCRh5g
- `img/protein.jpg`: Sam Moghadam, https://unsplash.com/photos/VpOpy6QrDrs
- `img/rajma.jpg`: Paul, https://unsplash.com/photos/93L024xGEUM
- `img/salad.jpg`: Andrew Relf, https://unsplash.com/photos/iku1zhSNRU8
- `img/samosa.jpg`: kabir cheema, https://unsplash.com/photos/8T9AVksyt7s
- `img/sandwich.jpg`: Mustafa Fatemi, https://unsplash.com/photos/Iy63wBayBhQ
- `img/vadapav.jpg`: Zoshua Colah, https://unsplash.com/photos/ohRSE3kUdNc

Screenshots of the real app used as reference live in `ref/`, which is git-ignored and never committed.
