
# References
---
https://www.pragmaticcoding.ca/javafx/MVC_In_JavaFX


---


Great work so far—it sounds like you've built a solid foundation for the Enhanced Pokédex GUI, especially with import/export, searchable and editable tables, and good UI feedback! Based on the **CCPROG3 Machine Project specs**, here’s a checklist to see what might still be missing or incomplete in your implementation:

---

## ✅ Features You Already Mentioned:

-  Add Pokémon, Moves, Items, Trainers
    
-  Import/Export support
    
-  View tables (probably satisfying "View All ___" features)
    
-  Search functionality for all modules
    
-  Validation in input dialogs
    
-  Context menu for editing/deleting rows (nice UX touch)
    

---

## ❗ Critical Missing Features (Based on Specs)

### 1. **Pokémon Cry**

- You **must** implement a `cry()` method that plays a Pokémon's cry sound. This means:
    
    - Audio integration (e.g., `.wav` or `.mp3` files)
        
    - Calling `cry()` when needed (e.g., a button in the Pokémon table row?)
        
    - Sounds can be placeholder if real ones are unavailable—but **must be present**.
        

---

### 2. **Trainer Functionality**

Make sure the following Trainer methods are implemented **with full logic**, not just table entries:

-  **Buy Item**: Deduct money and add to bag (respecting the 50-limit and 10-unique-item rules).
    
-  **Use Item**: Apply stat effects to selected Pokémon.
    
-  **Add Pokémon to Lineup**: Max 6 in lineup, the rest go to storage.
    
-  **Switch Pokémon from Storage**
    
-  **Release Pokémon**
    
-  **Teach Moves**:
    
    - Max 4 moves
        
    - Must match at least one type
        
    - HM moves cannot be forgotten
        

> These need GUI controls and backend logic (updating trainer + Pokémon objects).

---

### 3. **Pokémon Evolution Logic**

-  **Level-based evolution via Rare Candy**:
    
    - Level up increases stats by 10%
        
    - Evolves if the evolution level is reached
        
-  **Evolution Stone logic**:
    
    - Only evolve if compatible
        
    - New stats = max(current, evolved base)
        
-  Retain all moves, held items, stats
    

---

### 4. **Held Items (1 at a time)**

-  GUI and logic for:
    
    - Assigning a held item
        
    - Replacing the held item discards the current one
        

---

### 5. **Bag Limits and Item Constraints**

-  Each trainer:
    
    - Max 10 **unique** item types
        
    - Max 50 **total** items
        
-  Discard prompt if limits are exceeded
    

---

### 6. **Move Compatibility Checks**

-  Cannot teach move if Pokémon type does **not** match **any** of the move's types
    

---

### 7. **HM Move Rules**

-  HM moves:
    
    - Can be added without replacing an existing move (can exceed 4 temporarily?)
        
    - Cannot be forgotten
        

---

### 8. **Final MVC Structure**

-  Clear separation of:
    
    - **Model**: Pokémon, Move, Item, Trainer, etc.
        
    - **View**: JavaFX UI (TableView, dialogs)
        
    - **Controller**: Manages actions/events and business logic
        

---

### 9. **Updated UML**

-  Reflect any added relationships, particularly:
    
    - Pokémon → Move (learned)
        
    - Pokémon → Held Item
        
    - Trainer → Pokémon (lineup & storage)
        
    - Trainer → Bag
        

---

## 📎 Other Deliverables to Check:

-  Javadoc comments for all proponent-defined classes
    
-  Test scripts (at least 3 test cases per method, except getters/setters)
    
-  Updated UML (in PNG/PDF)
    
-  Declaration of Original Work
    
-  Demo-readiness: Should run from terminal, clean structure, and proper code documentation
    

---

## 🔥 Bonus Ideas (for extra credit in MCO2)

Once required features are done:

-  Evolution animation
    
-  Stat graphs or visual Pokémon team layout
    
-  Held item icons
    
-  Audio feedback (e.g., menu click sounds)
    
-  Version control (GitHub + commit history)
    

---

If you’re unsure whether a specific feature counts as “done,” feel free to describe how you implemented it and I can verify it against the spec. Want help building any of the missing mechanics (like evolution logic, move compatibility, or item use)?


---


# Trainer
- Max 10 unique item types
- Max 50 total items

**Personal Info**
- Birthdate
- Sex
- Hometown
- Money

**Pokemon Lineups (Max of 6)**
- Pikachu
- Charizard
- Bulbasaur

**Storage (No Cap)**
- These are the **extra Pokémon** a trainer owns but doesn't currently carry.
- No fixed limit in most systems, but you can implement a logical cap (e.g., 100).
- Stored Pokémon can be **moved to the lineup** or **viewed only**.
- Think of it as a **"Pokémon bank"**.



# TODO
- [x] "In Lineup By" column must be updated with a trainer name when a pokemon is added to a trainers lineup.
- [ ] Add edit functionality
- [x] Remove "Add to Lineup" and "Edit" menu items for Pokemon Table in Pokemon Lineup Tab under Trainers
- [ ] Remove "In Lineup By" column in Pokemon Lineup Table 
- [ ] Update pokemon lineup in dashboard
- [x] When adding pokemon to pokemon lineup, it should be the same instance.
- [x] Implement `useItem()`
- [x] Implement `addPokemonToLineup(Pokemon pokemon)`
- [ ] Implement `switchPokemonFromStorage()`
- [ ] Implement `releasePokemon()`
- [ ] Implement `teachMoves()`
- [ ] Initialize fields in instance level and not under constructor for every class for consistency
- [ ] Put background color to the types cells in the table
- [ ] Also add color coding to the stats cells pls
- [ ] Also when adding moves, make it a label component with design instead of string
- [ ] Allow pokemon to add images when adding pokemon
- [ ] Allow pokemon to have autocomplete for names showing all the pokemon names and when selected it will auto-fill when adding pokemon
- [ ] Implement evolution animation
- [ ] Add trainer photo (Ref: https://x.com/mattyoukhana_/status/1230541915055149063)
- [ ] Other trainers must not overwrite taken pokemens! (BUG)
- [x] EVs are not implemented just use raw +10 if 10 or -1 if -1
- [ ] Each level up  of rare candy increases base stats by 10%
- [ ] Make all items are holdable
- [ ] Move type and pokemon type must match
- [x] Minimum money is 1,000,000
- [x] Icon maven (ikonli) is allowed / libraries are allowed
- [x] Remove adding and deleting custom items
- [x] Items are not deletable
- [x] Moves are single typed only
