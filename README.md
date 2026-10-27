# Billedbehandling_projekt

King Domino – scoretæller
Finder scoren for en King Domino-plade ud fra et billede. Bruger kun teknikker fra forelæsningerne: slicing, HSV-farver, template matching og grassfire.

Krav
Python 3
OpenCV og NumPy
pip install opencv-python numpy
Brug
Læg crown_template.png i samme mappe som scriptet, og kør:

python kingdomino.py sti/til/plade.jpg
Uden argument bruges kingdomino.jpg i samme mappe.

Programmet udskriver terrænet for hvert felt, antal kroner pr. felt, områderne med kroner og den samlede score.

Sådan virker det
Opdeling – billedet skæres i 5x5 felter.
Terræn – medianfarven i HSV for hvert felt sammenlignes med grænserne i TERRAINS. Passer intet, bliver feltet Unknown (som regel hjemmefeltet).
Områder – grassfire (4-nabolag) samler naboer med samme terræn til områder.
Kroner – template matching med en maske (kun kronens hvide kant og gule midte) i alle 4 rotationer. Pixels over CROWN_THRESHOLD thresholdes, og hver klat (fundet med grassfire) tælles som én krone.
Score – for hvert område: antal felter × antal kroner i området. Summen er pladens score.
Justering
TERRAINS: HSV-grænserne er fundet ud fra træningspladerne. Rækkefølgen betyder noget, da det første terræn der passer bliver brugt.
CROWN_THRESHOLD (standard 0.5): sæt højere ved falske kroner, lavere hvis kroner bliver overset.
