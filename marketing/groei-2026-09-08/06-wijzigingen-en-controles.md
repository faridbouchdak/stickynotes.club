# Wijzigingen en controles

8 september 2026.

## Aangepast in de marketingrepository

- `docs/index.md`: vier doelgerichte ingangen voor persoonlijk gebruik, samenwerken, workshops leiden en deelnemen.
- `docs/getting-started.md`: concrete gratis boardroute, correcte registratievelden en uitleg van de publicatielimiet.
- `docs/private-boards.md`: gratis persoonlijke instap en voorwaarden voor het delen van eigen boards vroeg zichtbaar.
- `docs/plans-and-subscriptions.md`: drie maandplannen in de hoofdvergelijking; dagelijks publiceren onderscheiden van privénotities; Chosen Few in een eigen sectie met behouden rechten.
- `docs/faq.md`: antwoorden over persoonlijk gebruik, twee publicaties per dag, privéworkshops en plankeuze.
- `docs/_config.yml` en `docs/llms.txt`: bredere omschrijving en verwijzingen naar nieuwe gidsen.
- Nieuw: `docs/use-sticky-notes-for-yourself.md` en `docs/public-wall-private-board-workshop.md`.
- Nieuw: `marketing/groei-2026-09-08/`, met dit complete pakket.
- `marketing/00_README.md` en `marketing/01_MARKETINGPLAN.md`: gedateerde verwijzing naar het actuele uitvoeringsplan; oude inhoud bewaard.

## Uitgevoerde controles

- Bestaande gevolgde applicatiebestanden vergeleken met SHA-256-momentopname: geen wijzigingen. Applicatie-gitstatus bleef schoon.
- Eerdere bewerkingen aan socialmediabestanden vergeleken met de momentopname: behouden.
- Omzetberekeningen en beide uitvalscenario’s opnieuw berekend.
- Interne absolute paginalinks van het Help Centre gecontroleerd tegen de bestaande en nieuwe permalinks: geen ontbrekende doelen.
- Bestaande permalinks behouden; nieuwe gidsen hebben eigen permalinks.
- Planparameters gecontroleerd in de applicatie: Host gebruikt premium; Facilitator pro; Chosen Few chosen_few.
- Bronnen onderscheiden: lokale code, live helpteksten, uitspraken van Farid en hypothetische marketingberekeningen.
- Afzonderlijke FAQ/Chosen Few-ankerlinks en structuur gecontroleerd; geen onbeantwoorde beslissingen over Chosen Few of de gekozen acquisitierichting blijven in de briefing staan.

## Grenzen van deze controle

De homepage en pricing gaven automatische requests een 403. De native browsercontrole kon door een lokale omgevingsfout niet starten. Er is daarom geen visuele productieaudit, volledige registratie- of betaaltest uitgevoerd. Farid bevestigt de betaalbaarheid van beide maandplannen; dat is als gebruikersbevestiging genoteerd.

De marketingexpert heeft zelf een tijdelijke lokale Jekyll 3.10.0-omgeving ingericht en de bestaande helpwebsite succesvol gebouwd met de bestaande remote theme-configuratie. Alle 22 gegenereerde pagina’s zijn gecontroleerd op interne paginalinks en ankers: geen ontbrekende doelen.

Zes kernpagina’s zijn in Chrome gecontroleerd op 1440px desktop en 375px mobiel: alle twaalf controles gaven HTTP 200, geen horizontale pagina-overloop, geen ontbrekende afbeeldingen en geen JavaScript-fouten. Screenshots van de homepage, abonnementengids en nieuwe gidsen zijn visueel bekeken. Zoeken op “yourself” vindt de nieuwe persoonlijke startgids; het Chosen Few-anker bestaat en opent correct.

Deze controles betreffen de lokale build, geen publicatie. Het helpcentrum blijft volledig in scope van de marketingexpert, inclusief inhoud, navigatie, bouwcontrole, zoeken, weergave en publicatieafstemming. De applicatiedeveloper wijzigt alleen de applicatie en de verwijzingen naar de helpgidsen. Er is momenteel geen extra productinformatie nodig van de developer.

Beleids-/juridische teksten zijn niet veranderd. De historische marketing-PDF is alleen als achtergrond gelezen; niet alle externe verwijzingen daarin zijn heronderzocht en die zijn niet als bewijs voor nieuwe claims gebruikt.

## In de overdrachtskopie

De outputs bevatten het bijgewerkte marketingpakket, volledige kopieën van de negen gewijzigde/nieuwe helpbestanden, een patch uitsluitend voor `docs/` en desktop-/mobielpreviews van de help-homepage. Breng de patch niet bovenop de reeds aangepaste lokale marketingrepository aan: die wijzigingen staan daar al. De patch is bedoeld voor een andere checkout van dezelfde uitgangsversie. Controleer altijd eerst de diff en bestaande lokale wijzigingen.
