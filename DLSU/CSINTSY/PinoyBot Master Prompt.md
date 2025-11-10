

### Ang Iyong Comprehensive Prompt (Final Version):

**PAALALA: Basahin at sundin ang LAHAT ng instructions nang maigi.**

**Role:** Ikaw ay isang data generator para sa isang Natural Language Processing (NLP) project.

Ang Iyong Misyon (Ang Pinaka-Importanteng Goal):

Kailangan kong bumuo ng 1,000 karagdagang (additional) unique na data rows na eksaktong sumusunod sa format at lohika (logic) ng data sa [CSINTSY] GRP2_MCO2_DataSet.xlsx.

Ang bawat isang row na iyong ibibigay ay dapat maglaman ng **lahat** ng 12 columns na ito, sa eksaktong pagkakasunod-sunod na ito:

1. `word_id`
    
2. `sentence_id`
    
3. `sentence`
    
4. `context`
    
5. `word`
    
6. `label`
    
7. `special_tags`
    
8. `is_correct`
    
9. `corrected_label`
    
10. `corrected_special_tags`
    
11. `is_dirty`
    
12. `notes`
    

Ang iyong output ay dapat isang **CSV format**.

---

### Mga Hakbang (Steps) na Dapat Mong Sundin:

#### Hakbang 1: Bumuo ng mga Unique na Sentences

Kailangan mo munang lumikha ng isang **unique na sentence**. Huwag mong ulitin ang sentence na ito.

- **Wika (Language):** Dapat ito ay **Taglish** (Code-switched Tagalog at English). Mas maraming Tagalog, pero natural ang pagpasok ng English.
    
- **Tono (Tone):** Dapat ito ay parang isang tunay na sinabi ng tao. Isipin mo ang mga post sa Facebook, mga komento sa Reels, o mga tweet. Dapat casual, conversational, at minsan ay may opinyon.
    
- **Mga Paksa (Topics):** Dapat tungkol sa mga **kasalukuyang pangyayari** (current events), buhay-buhay (daily life), pop culture, teknolohiya, o mga personal na opinyon.
    
- **Gayahin ang Vibe Nito (Use these as your style guide):**
    
    - "Ang sarap nang feeling na may kaibigan ka na mahal."
        
    - "Eh diba kayong mga bumoboto nakasalalay sa inyo kung sino ang ihahalal?"
        
    - "Deko alam bakit gustong gusto ng mga pinoy si cong, as i can see napakakorny nya, de ko ba alam kung natatakpan ng kasikatan ang kakornihan nya o talagang marmi lng talagang jejemon sa pinas?"
        
    - "Grabe 'yung traffic kanina pag-uwi ko, almost 2 hours 'yung byahe na 30 minutes lang dapat."
        
    - "Sino na nakapanood nung bagong series sa Netflix? Worth it ba i-binge watch?"
        

#### Hakbang 2: I-proseso ang Bawat Sentence (Tokenization)

Kapag mayroon ka nang isang (1) unique na sentence, kailangan mong "i-tokenize" ito.

Ibig sabihin, paghihiwalayin mo ang **bawat salita (word)**. Dapat kasama sa "words" ang **punctuation** (e.g., "`,`", "`.`", "`?`", "`!`").

- **Halimbawa:** "Gusto ko 'yan, pre."
    
- **Tokens:** `Gusto`, `ko`, `'yan`, `,`, `pre`, `.`
    

#### Hakbang 3: Bumuo ng `context` para sa BAWAT Token

Para sa **bawat isang token** (salita) na nilikha mo sa Hakbang 2, gagawa ka ng isang row. Ang bawat row ay dapat may `context` (ang "sliding window" ng text sa paligid ng `word`).

Ang Lohika ng Pagbuo ng context (SUNDIN NANG MAIGI):

Ang context ay isang "window" ng mga salita na may 2 salita bago ang word at 2 salita pagkatapos ng word.

- **Halimbawa (Sentence):** "Deko alam bakit gustong gusto ng mga pinoy si cong"
    
- **Para sa word na "Deko"** (nasa simula):
    
    - `context`: "Deko alam bakit" (Walang 2 salita bago, kaya kukuha ito ng +2 salita pagkatapos)
        
- **Para sa word na "alam"** (pangalawa):
    
    - `context`: "Deko alam bakit gustong" (1 salita bago, 2 salita pagkatapos)
        
- **Para sa word na "bakit"** (nasa gitna):
    
    - `context`: "Deko alam bakit gustong gusto" (2 salita bago, 2 salita pagkatapos)
        
- **Para sa word na "gustong"** (nasa gitna):
    
    - `context`: "alam bakit gustong gusto ng" (2 salita bago, 2 salita pagkatapos)
        
- ...at iba pa...
    

#### Hakbang 4: Punan ang Bawat Row (Ang Final Structure)

Para sa **bawat isang token**, lumikha ng isang row sa iyong CSV. Gamitin ang mga numerong ito bilang panimula (batay sa huling data sa file):

- **`sentence_id`**: Magsimula sa `105` (dahil ang huling ID sa file ay 104). Ang _lahat_ ng tokens/words mula sa parehong sentence ay dapat may parehong `sentence_id`. Para sa susunod na _unique_ na sentence, gamitin ang `106`, tapos `107`, at iba pa.
    
- **`word_id`**: Magsimula sa `1850` (dahil ang huling ID sa file ay 1849). Ang bawat row (bawat word) ay dapat may unique na `word_id`. Ituloy-tuloy lang ang pag-increment para sa bawat bagong word (`1851`, `1852`, `1853`...).
    
- **`sentence`**: Ilagay ang _buong_ unique Taglish sentence (ulit-ulit ito para sa bawat word).
    
- **`context`**: Ilagay ang "sliding window" context na binuo mo sa Hakbang 3.
    
- **`word`**: Ilagay ang _isang_ token/word para sa row na 'yon.
    

**PARA SA MGA SUMUSUNOD NA COLUMNS, HAYAAN MONG BLANGKO.** Ito ang mga columns na kami na ang maglalagay ng data (annotations) pagkatapos:

- `label`: (BLANGKO)
    
- `special_tags`: (BLANGKO)
    
- `is_correct`: (BLANGKO)
    
- `corrected_label`: (BLANGKO)
    
- `corrected_special_tags`: (BLANGKO)
    
- `is_dirty`: (BLANGKO)
    
- `notes`: (BLANGKO)
    

#### Hakbang 5: Ulitin hanggang 1,000 Rows

Ulit-ulitin ang Hakbang 1, 2, 3, at 4. Gawa ng bagong unique na sentence, i-proseso ang bawat salita, at gawing row, hanggang sa makaabot ka sa **1,000 na bagong rows**.

**Format ng Output (Example):**

Code snippet

```
word_id,sentence_id,sentence,context,word,label,special_tags,is_correct,corrected_label,corrected_special_tags,is_dirty,notes
1850,105,"Grabe ang traffic, 1 hour na ako dito.","Grabe ang traffic ,",Grabe,,,,,,,,
1851,105,"Grabe ang traffic, 1 hour na ako dito.","Grabe ang traffic , 1",ang,,,,,,,,
1852,105,"Grabe ang traffic, 1 hour na ako dito.","Grabe ang traffic , 1 hour",traffic,,,,,,,,
1853,105,"Grabe ang traffic, 1 hour na ako dito.","ang traffic , 1 hour na",",",,,,,,,,
1854,105,"Grabe ang traffic, 1 hour na ako dito.","traffic , 1 hour na ako",1,,,,,,,,
1855,105,"Grabe ang traffic, 1 hour na ako dito.","traffic , 1 hour na ako dito",hour,,,,,,,,
1856,105,"Grabe ang traffic, 1 hour na ako dito.",", 1 hour na ako dito .",na,,,,,,,,
1857,105,"Grabe ang traffic, 1 hour na ako dito.","1 hour na ako dito .",ako,,,,,,,,
1858,105,"Grabe ang traffic, 1 hour na ako dito.","hour na ako dito .",dito,,,,,,,,
1859,105,"Grabe ang traffic, 1 hour na ako dito.","na ako dito .",".",,,,,,,,
1860,106,"Sino na naka-try nung bagong update sa IG?","Sino na naka-try",Sino,,,,,,,,
1861,106,"Sino na naka-try nung bagong update sa IG?","Sino na naka-try nung",na,,,,,,,,
1862,106,"Sino na naka-try nung bagong update sa IG?","Sino na naka-try nung bagong",naka-try,,,,,,,,
...
```

Umpisahan mo na.


---

# CONTINUATION


**PAALALA: Basahin at sundin ang LAHAT ng instructions nang maigi.**

**Role:** Ikaw ay isang advanced data generator para sa isang Natural Language Processing (NLP) project.

Ang Iyong Misyon (Ang Pinaka-Importanteng Goal):

Ang iyong misyon ay ipagpatuloy ang pag-generate ng data para sa aking existing na [CSINTSY] GRP2_MCO2_DataSet.xlsx file.

Ang layunin ay **magdagdag ng mga bagong unique na rows** sa ilalim ng huling entry, na perpektong sumusunod sa 12-column format. Ang pinaka-kritikal na patakaran ay: **WALANG REPETISYON**. Ang mga bagong `sentence` ay dapat 100% unique, na magreresulta sa mga `context` na bago at hindi duplikado sa buong dataset, kahit na ang _istilo_ nila ay _katulad_ (similar) sa mga nauna.

Ang bawat row na iyong ibibigay ay dapat maglaman ng lahat ng 12 columns na ito, sa eksaktong pagkakasunod-sunod:

word_id, sentence_id, sentence, context, word, label, special_tags, is_correct, corrected_label, corrected_special_tags, is_dirty, notes

---

### Mga Hakbang (Steps) na Dapat Mong Sundin:

#### Hakbang 0: Alamin ang Iyong Starting Point (Simula)

Dahil **ipagpapatuloy** mo ang isang existing na sheet, kailangan nating malaman kung saan ka magsisimula.

Bago ka mag-umpisa, **ITANONG MO MUNA SA AKIN** kung ano ang:

1. **Huling `sentence_id`** na ginamit?
    
2. **Huling `word_id`** na ginamit?
    

Kapag binigay ko na sa iyo ang mga numerong iyon (halimbawa: huling `sentence_id` = 104, huling `word_id` = 1849), ang _unang_ row na iyong bubuuin ay magsisimula sa `sentence_id` 105 at `word_id` 1850.

#### Hakbang 1: Bumuo ng mga 100% UNIQUE na Sentences

KRITIKAL NA RULE PARA SA UNIQUENESS:

Ang bawat sentence na iyong bubuuin ay dapat 100% UNIQUE. Huwag kailanman ulitin ang isang sentence na nagamit na, o kahit isang sentence na halos kapareho. Ito ang pinakamahalagang paraan para masiguro na ang mga context na mabubuo ay bago at hindi duplikado, kahit na magkamukha (similar) sila sa istilo. Mag-focus sa iba't ibang paksa.

- **Wika (Language):** Taglish (Mas maraming Tagalog, pero natural ang pagpasok ng English).
    
- **Tono (Tone):** Conversational, casual, parang tunay na post o komento.
    
- **Mga Paksa (Topics):** Iba-ibahin ang paksa: mga bagong balita, personal na "rants," tanong tungkol sa teknolohiya, komento sa pagkain, usapang-trapik, atbp.
    
- **Gayahin ang Vibe Nito (Style Guide):**
    
    - "Ang sarap nang feeling na may kaibigan ka na mahal."
        
    - "Eh diba kayong mga bumoboto nakasalalay sa inyo kung sino ang ihahalal?"
        
    - "Deko alam bakit gustong gusto ng mga pinoy si cong, as i can see napakakorny nya..."
        
    - "Grabe 'yung traffic kanina pag-uwi ko, almost 2 hours 'yung byahe."
        

#### Hakbang 2: I-proseso ang Bawat Sentence (Tokenization)

Kapag mayroon ka nang isang (1) unique na sentence, i-tokenize ito (paghiwalayin ang bawat salita at punctuation).

- **Halimbawa:** "Gusto ko 'yan, pre."
    
- **Tokens:** `Gusto`, `ko`, `'yan`, `,`, `pre`, `.`
    

#### Hakbang 3: Bumuo ng `context` para sa BAWAT Token

Para sa **bawat isang token**, bumuo ng `context` gamit ang "sliding window" logic.

Ang Lohika ng Pagbuo ng context (SUNDIN NANG MAIGI):

Ang context ay ang window na may 2 salita bago ang word at 2 salita pagkatapos ng word. I-adjust para sa mga salita sa simula at dulo.

- **Halimbawa (Sentence):** "Check mo yung bagong update, pre."
    
- **Para sa "Check"** (simula): `context`: "Check mo yung"
    
- **Para sa "mo"** (pangalawa): `context`: "Check mo yung bagong"
    
- **Para sa "yung"** (gitna): `context`: "Check mo yung bagong update"
    
- **Para sa "bagong"** (gitna): `context`: "mo yung bagong update ,"
    
- ...at iba pa...
    

#### Hakbang 4: Punan ang Bawat Row (Ang Final Structure)

Para sa **bawat isang token**, lumikha ng isang row sa iyong CSV.

- **`sentence_id`**: Gamitin ang bagong `sentence_id` (e.g., `105`). Ang _lahat_ ng tokens mula sa iisang sentence na ito ay dapat may parehong `sentence_id`.
    
- **`word_id`**: Gamitin ang bagong `word_id` (e.g., `1850`). Mag-increment para sa bawat bagong word (`1851`, `1852`...).
    
- **`sentence`**: Ilagay ang _buong_ unique Taglish sentence.
    
- **`context`**: Ilagay ang "sliding window" context na binuo mo.
    
- **`word`**: Ilagay ang _isang_ token/word para sa row na 'yon.
    

**PARA SA MGA SUMUSUNOD NA COLUMNS, HAYAAN MONG BLANGKO.** Ito ang mga columns na kami na ang maglalagay ng annotations:

- `label`: (BLANGKO)
    
- `special_tags`: (BLANGKO)
    
- `is_correct`: (BLANGKO)
    
- `corrected_label`: (BLANGKO)
    
- `corrected_special_tags`: (BLANGKO)
    
- `is_dirty`: (BLANGKO)
    
- `notes`: (BLANGKO)
    

#### Hakbang 5: Ulitin ang Proseso

Kapag tapos na ang lahat ng tokens para sa isang sentence (e.g., natapos sa `word_id` 1862), simulan muli ang **Hakbang 1**gamit ang susunod na `sentence_id` (e.g., `106`).

1. Bumuo ng **BAGONG UNIQUE SENTENCE**.
    
2. I-tokenize ito.
    
3. Bumuo ng `context` at `word` para sa bawat token.
    
4. Punan ang bawat row, sisimulan sa `word_id` 1863.
    
5. Ulit-ulitin ito.
    

### Ang Iyong Final Output

Ibigay mo ang data sa **CSV format**. Ang unang row ay dapat ang header. Gumamit ng `"` (double quotes) para i-wrap ang text para maiwasan ang error.

**Format ng Output (Example kung ang huling ID ko ay 1849 at 104):**

Code snippet

```
word_id,sentence_id,sentence,context,word,label,special_tags,is_correct,corrected_label,corrected_special_tags,is_dirty,notes
1850,105,"Ang init na naman today, 'di ba?","Ang init na",Ang,,,,,,,,
1851,105,"Ang init na naman today, 'di ba?","Ang init na naman",init,,,,,,,,
1852,105,"Ang init na naman today, 'di ba?","Ang init na naman today",na,,,,,,,,
1853,105,"Ang init na naman today, 'di ba?","init na naman today ,",naman,,,,,,,,
1854,105,"Ang init na naman today, 'di ba?","na naman today , 'di",today,,,,,,,,
1855,105,"Ang init na naman today, 'di ba?","naman today , 'di ba",",",,,,,,,,
1856,105,"Ang init na naman today, 'di ba?","today , 'di ba ?",'di,,,,,,,,
1857,105,"Ang init na naman today, 'di ba?","today , 'di ba ?",ba,,,,,,,,
1858,105,"Ang init na naman today, 'di ba?","today , 'di ba ?",?",",,,,,,,,
1859,106,"Sana all may 13th month pay na.","Sana all may",Sana,,,,,,,,
1860,106,"Sana all may 13th month pay na.","Sana all may 13th",all,,,,,,,,
1861,106,"Sana all may 13th month pay na.","Sana all may 13th month",may,,,,,,,,
...
```

**Magsimula tayo.** Pakitanong muna ang huling `sentence_id` at `word_id` sa aking sheet.