# NOTES

## Six observations on the live PKHosting pricing section (https://www.pkhosting.com)

1. **Billing toggle, "Annually Save up to 16%" and "2 years Save up to 16%".** Annual and 2-year show the same saving, so a buyer sees no reason to commit for two years. "Up to" also hides the real per-plan saving. Consequence: the longer term looks pointless and the badge is not trustworthy.
2. **Card price line, "Rs699/mo" with small print "Rs 6,990/yr (10x monthly) if billed annually".** In monthly view the annual price is a formula in small grey text under the price. Consequence: the annual saving is easy to miss, and "10x monthly" is jargon for non-technical buyers.
3. **Currency switcher in the top bar (PKR flag button).** The copy above the cards says to switch currency "in the top bar", so the control is far from the cards it changes. Consequence: on a phone the user must scroll away from the plans to change currency, and many will not find it.
4. **Badges "Economical", "Most Popular", "Best Value" on three cards.** Three competing labels, and "Best Value" sits on the most expensive plan with no per-GB or per-site number behind it. Consequence: no single recommended path, and an unsupported claim.
5. **Feature lists: "Unmetered bandwidth - fair-use policy applies" repeated on every card; Professional says "No fixed LVE allocation - fair-use CPU, RAM and I/O".** Nothing states CPU or RAM numbers. Consequence: buyers cannot compare real resources between plans, only sites, storage and email counts.
6. **"Order Now" buttons (checkout/?product=2, 3, 4).** Identical link text on all three cards. Consequence: a screen reader user listing links hears three "Order Now" with no plan name unless an aria-label exists (I did not confirm this in DevTools, check before relying on it).

## Trade-offs

- **State persistence:** period and currency are saved in `localStorage` (key `pkvps`) inside try/catch. I chose it over cookies or URL params because it needs no server and no request. Cost: it is per browser, and the saved state is applied by script after load, so a returning user on annual/USD sees the monthly PKR HTML for a split second before the script runs (the layout does not move, only the text changes). Without JS, or if storage is blocked, the page stays on monthly PKR, which is also what the HTML source contains.
- **Fixed rates:** 1 USD = 278.50 PKR, 1 GBP = 355.00 PKR, hard-coded as required.
- **Payment methods:** the brief says PKHosting lists eight. The live footer I looked at showed five (Stripe, PayPal, JazzCash, Easypaisa, bank account). I would offer four: bank transfer (IBFT/Raast), JazzCash, Easypaisa and Visa/Mastercard. Dropped: PayPal and Stripe as separate entries, because card payment is already covered by Visa/Mastercard and I would rather not promise brand-specific processors I cannot verify for Pakistani buyers. They are shown as text chips, not logos, so there are no hotlinked or extra image requests.
- **No framework, no build step:** one HTML file opens offline.
- **CTA buttons** are demo links back to the top, since nothing ships.
