# Meta-Operator Blueprint (Session 1)

## Ausgangslage
Dieses Projekt startet als Planungs- und Entscheidungsframework für eine einzelne Person mit Ingenieur-/MATLAB-Hintergrund.
Der Fokus liegt zunächst **nicht** auf sofortiger Implementierung, sondern auf einer reproduzierbaren Routine, die Entscheidungen für agentisches Coding handhabbar macht.

## Projektziel (v0)
Ein lokal nutzbares "Meta Prompting UI" bzw. Workflow, mit dem der Nutzer mit einer handlungsfähigen Coding-Persona arbeitet.
Das System soll:
1. unklare Anforderungen in klare Arbeitspakete übersetzen,
2. Implementierungsentscheidungen mit wenig Vorwissen strukturieren,
3. den Kontext für Agent-Calls kuratieren (statt alles auf einmal zu laden),
4. als persistentes "Gedächtnis" zwischen Sessions funktionieren.

## Nicht-Ziele (für Startphase)
- Keine skalierbare Multi-User-Plattform.
- Keine frühe Festlegung auf komplexes Cloud-/DevOps-Setup.
- Kein sofortiger Vollbau einer produktionsreifen Anwendung.

## Entscheidungsroutine für "Ich weiß es nicht"-Momente
Wenn eine technische Frage auftaucht (z. B. OAuth, Tunnel, Hosting), nutzen wir immer dieselbe 5-Schritt-Routine:

1. **Frage klassifizieren**
   - Sicherheit, Betrieb, Architektur, UX oder Kosten?
2. **Relevanz prüfen**
   - Ist die Entscheidung jetzt nötig oder später?
3. **Optionen auf 2-3 reduzieren**
   - Je Option: Nutzen, Risiko, Komplexität, Standard-Empfehlung.
4. **Default wählen**
   - "Sicherer, einfacher Standard" falls keine starke Präferenz vorliegt.
5. **Entscheidung dokumentieren**
   - Kurz in `memory/decisions.md` mit Datum, Begründung, Revisit-Trigger.

## Arbeitsmodus (Meta Operator)
Solange nicht anders beschlossen, bleibt der Modus auf Meta-Ebene:
- Problemverständnis
- Scope-Klärung
- Entscheidungsrahmen
- Roadmap statt Tiefenimplementierung

## Vorschlag für Artefakt-Struktur

```text
memory/
  project-brief.md          # Ziel, Nutzer, Constraints
  decisions.md              # getroffene Entscheidungen + offene Punkte
  architecture-map.md       # grobe Systemübersicht
  session-log.md            # Fortschritt je Sitzung
  next-actions.md           # konkrete nächste Schritte

context/
  call-profile-meta.md      # Kontext für Meta-Planungs-Calls
  call-profile-build.md     # Kontext für Implementierungs-Calls
  call-profile-test.md      # Kontext für Test/Debug-Calls

prompts/
  decision-template.md      # Template für Technikentscheidungen
  task-template.md          # Template zum Zerlegen in Tasks
```

## Kontext-Kuratierung (wichtig für Agent-Qualität)
Pro Call soll nur relevanter Kontext geladen werden:
- **Meta-Call:** Ziel, Entscheidungen, offene Fragen.
- **Build-Call:** nur betroffene Komponenten + API-Schnittstellen.
- **Test-Call:** nur Testziele, Fehlerbild, relevante Logs.

Faustregel: lieber 1 fokussierter Call mit kleinem Kontext als 1 großer Call mit Rauschen.

## Erste Milestones (Planungsorientiert)
1. **M1 - Projektgedächtnis aufsetzen**
   - Verzeichnisstruktur und Templates anlegen.
2. **M2 - Entscheidungs-Workflow festlegen**
   - Standardfragen + Defaults definieren.
3. **M3 - Minimaler Laufweg**
   - "Idee -> Plan -> Taskliste -> (optional) Implementierung" als wiederholbare Schleife.
4. **M4 - Erste kleine Referenzumsetzung**
   - Ein kleines, lokal laufendes Beispiel verwenden, um die Schleife zu validieren.

## Leitplanken-Entscheidungen (Session 2)
Basierend auf Nutzerfeedback sind folgende Leitplanken vorläufig gesetzt:

1. **Oberfläche / MVP:**
   - Start mit **CLI-first im Terminal** (geringster Aufwand, direkte Logs, schneller MVP).
   - Web-UI ist optionaler späterer Ausbau, falls konkreter Mehrwert entsteht.
2. **Local-first mit pragmatischer Cloud-Option:**
   - Standard: lokal und einfach.
   - Cloud/SaaS nur bei klarem Aufwandsvorteil (z. B. RAG/Indexing), bevorzugt mit Free Tier oder sehr niedrigen Kosten.
   - Keine langfristigen Bindungen und kein schwergewichtiges Setup als Default (z. B. umfangreiche AWS-Konfiguration).
3. **Automatisierungsgrad:**
   - Standard: hohe Automatisierung bei klaren Entscheidungen.
   - Fallback auf Best Practices, wenn keine explizite Präferenz vorliegt.
   - Rückfragen nur bei wirklichen Richtungsentscheidungen (Kosten, Sicherheit, irreversible Architekturwahl).

## Entscheidungs-Matrix für "Build vs Buy" (leichtgewichtig)
Wenn die Frage auftaucht, ob lokale Eigenimplementierung oder externer Service besser ist:

1. **Nutzwert jetzt** (erhöht es in dieser Woche die Lieferfähigkeit?)
2. **Einmalkosten** (Implementierungszeit + Setup-Aufwand)
3. **Laufende Kosten** (Abo/Usage im Zielrahmen: ideal Free Tier bis wenige Euro)
4. **Betriebsrisiko** (Ausfall, Vendor-Lock-in, Datensensitivität)
5. **Ausstiegsoption** (wie leicht kann später migriert werden?)

Daumenregel:
- Für Prototyping: bevorzugt die Option mit dem geringsten Gesamtaufwand in den nächsten 2-4 Wochen.
- Für Kernfunktionen mit hoher Bindung: eher lokal oder mit klarer Exit-Strategie.

## Anti-Overengineering-Guardrails
- Vor jeder neuen Komponente prüfen: "Löst das jetzt ein konkretes Problem oder nur ein mögliches zukünftiges?"
- Nur eine neue technische Schicht pro Iteration einführen.
- Jede Iteration soll ein sichtbares, prüfbares Ergebnis liefern (z. B. lauffähiger CLI-Workflow).

## Nächster konkreter Schritt (empfohlen)
Für die nächste Sitzung reicht ein sehr kleiner Scope:
1. `memory/` + `context/` + `prompts/` als echte Verzeichnisse anlegen.
2. Pro Bereich jeweils 1 minimales Template erstellen.
3. Einen "Meta-Call -> Taskliste" Beispielablauf dokumentieren.
Damit entsteht sofort ein nutzbarer Kern ohne vorzeitige Architekturentscheidung.

## Kurzantwort auf die Subagenten-Frage
Ja, konzeptuell arbeiten moderne Coding-Agenten oft mit Aufgabenzerlegung in Teilkontexte.
Wichtiger als "wie intern genau" ist für dieses Projekt:
- klare Aufgabenabgrenzung,
- kontrollierte Kontextgröße,
- dokumentierte Entscheidungen zwischen den Schritten.
Diese drei Punkte geben dir praktisch denselben Vorteil, ohne von internen Implementierungsdetails abhängig zu sein.
