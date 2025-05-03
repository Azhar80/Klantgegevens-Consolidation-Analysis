# Klantgegevens-Consolidation-Analysis
Client Data Integration &amp; Analysis
✅ 1. Combine names into a single field
From File A: already in one column (Naam)

From File B: use a formula
=B2 & ", " & A2 → to combine Familienaam and Voornaam into the same format

✅ 2. Standardize address format
In File A:
=E2 & " " & F2 & ", " & G2 → Combine Straat, Nummer, and gemeente

In File B: already in one field

✅ 3. Unify household info
A. Convert File A’s adult/child counts into a list of generic names
You’d need something like:

excel
Copy
Edit
=TEXTJOIN(",", TRUE, REPT("Volwassene,", D2), REPT("Kind,", E2))
…but Excel doesn’t support dynamic repetition without helper columns. You’d need:

A few helper columns with =IF(D2>=1,"Volwassene1",""), =IF(D2>=2,"Volwassene2",""), etc.

B. In File B: count adults/children from gezinsleden
If you assume:

18+ → adult (you’d need birthdates or another method)

or just count all as adults/kids based on name or assumption

Basic count:
=LEN(A2)-LEN(SUBSTITUTE(A2,",",""))+1 → to count number of people in the list

✅ 4. Align satisfaction metrics (reduce multiple yes/no to one score)
Create a numeric score:

excel
Copy
Edit
=AVERAGE(IF(J2="ja",1,0), IF(K2="ja",1,0), IF(L2="ja",1,0), IF(M2="ja",1,0), IF(N2="ja",1,0)) * 10
You may need to use Ctrl+Shift+Enter for array formulas in some Excel versions.

✅ 5. Standardize visit frequency
From A (textual):

Use =SWITCH(A2, "Zelden", 1, "Af en toe", 4, "Regelmatig", 8, "Vaak", 12)

From B (numeric): already good

✅ 6. Ensure consistent columns
Just rearrange columns manually once data is cleaned.

🔧 Summary
Step	Can be done in Excel?	Notes
Combine names	✅	Simple formula
Standardize address	✅	Simple formula
Household info (complex)	✅⚠️	Needs helper columns
Satisfaction score	✅	With formulas
Visit frequency normalization	✅	Simple formula
Merge and reorder	✅	Manual copy/paste or Power Query
