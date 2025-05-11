
# Data
- [ ] Line 25 from "src/routes/event/\[id]/page.svelte". Find the correct data event data. Instead of "Find true love in Calle Cafe."
- [x] Prevent next button from resetting the scroll in registration form inside /event/
- [x] Implement skeleton loading


**Enforce onboarding flow**
- [ ] After signing in, always redirect users to /onboarding until onboarding is complete (enforce using hooks.server.ts).
- [ ] Block manual navigation to other routes before onboarding is done.
    
**Date logic**
- [x] Disable “End Date” picker when “Till Late” is selected.
- [ ] Enable “End Date” only after “Start Date” is selected.
- [ ] Enable “Add Dates” button only when all required date inputs are valid (Start Date + End Date or Till Late).
    
**Dropzone preview**
- [ ] Show preview of uploaded image.
- [ ] Display filename and file size below or beside the image.

**Editor formatting buttons**
- [ ] Replace bold, italic, and bullet buttons with a ShadCN Toggle Group.

**Location input**
- [ ] Allow users to select a location via a map.
- [ ] Output should include:
	Location name (editable)
    Read-only latitude and longitude fields.

**Payment section**
- [ ] Add an area for collecting payment options/details.

**General form fixes**
- [ ] Ensure form state is synced and submitting properly.
- [ ] Implement full form validation.

**Ticketing issues**
- [ ] Fix ticket creation and editing behavior.
- [ ] Ensure correct currency symbol appears based on selected 3-letter currency code.
- [ ] Placeholder of price input must also reflect selected currency.

**Mobile & device compatibility**
- [ ] Make the “Add Tickets” drawer scrollable for smaller screens (e.g., Nest Hub).

**UI improvements**
- [ ] Fix navigation burger menu toggle.
- [ ] Fix formatting button group styles and behavior.
- [ ] Update visibility icon to reflect current selection (Public vs Private).
- [ ] Use preset color palettes throughout the app.

**DateTime Picker improvements**
- [ ] Make hours and minutes scrollable.
- [ ] Ensure AM/PM selection works properly.

**Chore**
- [ ] Organize components

