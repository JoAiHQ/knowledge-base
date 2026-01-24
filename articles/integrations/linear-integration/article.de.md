---
title: 'Linear Integration Guide für JoAi'
description: 'Richte die Linear-Integration mit JoAi in 5 Minuten ein. Erstelle Issues, verwalte Teams, aktualisiere States und automatisiere Projekt-Workflows mit der Linear GraphQL API. Komplette Anleitung.'
category: 'integrations'
tags: ['linear', 'integration', 'api', 'projektmanagement', 'graphql']
author: 'JoAi Team'
publishedAt: '2024-01-20'
updatedAt: '2024-01-20'
draft: true
featured: false
difficulty: 'intermediate'
readTime: 12
keywords:
  ['linear integration', 'linear integration einrichten', 'linear mit joai verbinden', 'linear api integration', 'linear projektmanagement', 'linear workflow automatisierung', 'linear graphql api', 'linear api key', 'linear issues api', 'linear teams']
relatedArticles: []
faqs:
  - question: 'Wie lange dauert die Einrichtung der Linear-Integration?'
    answer: 'Die Einrichtung dauert etwa 5 Minuten. Erstelle einen Linear API Key und setze ihn als Umgebungsvariable.'
  - question: 'Welche Berechtigungen benötigt die Linear-Integration?'
    answer: 'Die Integration benötigt einen Linear API Key. Dein API Key erbt die Berechtigungen deines Linear-Benutzerkontos – du kannst auf Teams zugreifen, in denen du Mitglied bist, und auf Issues, die du anzeigen darfst.'
  - question: 'Kann ich diese Integration mit allen Linear-Teams verwenden?'
    answer: 'Ja, du kannst auf alle Teams zugreifen, in denen du Mitglied bist. Wenn du Administrator bist, kannst du alle Teams und Issues in deinem Workspace verwalten.'
  - question: 'Wie hoch ist das Rate Limit für Linear API-Anfragen?'
    answer: 'Authentifizierte Anfragen haben ein Rate Limit von 10.000 Anfragen pro Stunde. Die Integration behandelt Rate Limiting automatisch.'
  - question: 'Wie finde ich Team-IDs und Issue-IDs?'
    answer: 'Verwende den "List Teams" Warp, um Team-IDs zu finden, und "List Issues", um Issue-IDs zu finden. Die Antwort enthält sowohl IDs als auch menschenlesbare Bezeichner.'
llmAnswer: 'Richte die Linear-Integration in JoAi ein, indem du einen API Key aus Linear Settings > API erstellst und ihn als LINEAR_API_KEY Umgebungsvariable setzt. Dies ermöglicht das Erstellen von Issues, das Verwalten von Teams, das Aktualisieren von States und das Hinzufügen von Kommentaren über die Linear GraphQL API.'
---

Die Linear-Integration für JoAi ermöglicht es dir, deine Linear-Issues, Teams und Projekte direkt aus deinem Arbeitsbereich zu verwalten. Diese Linear-Integration nutzt die Linear GraphQL API, damit du deinen Projektmanagement-Workflow automatisieren kannst, ohne JoAi zu verlassen. Die Einrichtung der Linear-Integration dauert nur 5 Minuten und eröffnet leistungsstarke Automatisierungsmöglichkeiten.

## Was du lernen wirst

* Wie du die Linear-Integration mit API Keys einrichtest
* Erstellen und Verwalten von Linear-Issues und Teams
* Aktualisieren von Issue-States und Prioritäten
* Hinzufügen von Kommentaren zur Fortschrittsverfolgung
* Fehlerbehebung bei häufigen Linear-Integrationsfehlern
* Best Practices für Linear-API-Authentifizierung und Sicherheit

## Wie du die Linear-Integration einrichtest

Du benötigst einen Linear API Key, um diese Linear-Integration zu verwenden. So richtest du ihn in nur wenigen Minuten ein.

### Erstelle deinen Linear API Key

Melde dich in deinem Linear-Konto unter [linear.app](https://linear.app) an und navigiere zu **Settings** → **API** (oder gehe direkt zu [https://linear.app/settings/api](https://linear.app/settings/api)).

Klicke auf **"Create API Key"** und gib ihm einen Namen wie "JoAi Integration".

**Wichtig**: Kopiere den API Key sofort – Linear zeigt ihn dir nicht erneut an!

### Konfiguriere die Linear-Integrations-Umgebungsvariable

Setze die Umgebungsvariable `LINEAR_API_KEY` mit deinem **Linear API Key**:

**macOS/Linux:**
```bash
export LINEAR_API_KEY="your_api_key_here"
```

Um es dauerhaft zu machen, füge es zu deiner `~/.zshrc` oder `~/.bashrc` hinzu:
```bash
echo 'export LINEAR_API_KEY="your_api_key_here"' >> ~/.zshrc
source ~/.zshrc
```

**Windows (PowerShell):**
```powershell
$env:LINEAR_API_KEY="your_api_key_here"
```

**Windows (Command Prompt):**
```cmd
setx LINEAR_API_KEY "your_api_key_here"
```

**Docker:**
```bash
docker run -e LINEAR_API_KEY="your_api_key_here" ...
```

### Überprüfe die Linear-Integration-Einrichtung

Versuche den "List Teams" Warp, um zu überprüfen, ob deine **Linear-Integration** funktioniert. Wenn erfolgreich, erhältst du eine Liste aller Teams in deinem Linear-Workspace.

## Linear-Integrations-Funktionen und Aktionen

### Linear-Teams auflisten

Verwende den `linear/list-teams` Warp, um alle Teams in deinem Linear-Workspace abzurufen. Dies ist normalerweise der erste Schritt, um Team-IDs zu finden, die für andere Operationen benötigt werden.

Du erhältst zurück:
* `TEAMS`: Array von Team-Objekten mit ID, Name, Key und Beschreibung
* `COUNT`: Anzahl der gefundenen Teams

Verwende dies, um Team-IDs zu finden, bevor du Issues erstellst oder auflistest.

### Linear-Issues erstellen

Verwende den `linear/create-issue` Warp, um ein neues **Linear-Issue** in einem beliebigen Team über die Linear-Integration zu erstellen.

Du benötigst:
* Team ID (erforderlich) – Hole dir diese von "List Teams"
* Titel (erforderlich)
* Beschreibung (optional, unterstützt Markdown)
* Assignee ID (optional)
* Priorität (optional): `0` = Keine Priorität, `1` = Dringend, `2` = Hoch, `3` = Mittel, `4` = Niedrig

Du erhältst die Issue-ID, Titel, URL, Bezeichner (z.B. "ENG-123") und Erfolgsstatus zurück.

Hier ist ein Beispiel:
```
Team ID: abc123def456
Title: Fix login bug
Description: The login form is not validating email addresses correctly.
Priority: 2
```

### Linear-Issues auflisten

Verwende `linear/list-issues`, um **Linear-Issues** in einem Team über die Integration aufzulisten. Du kannst nach Assignee, State filtern und Ergebnisse begrenzen (max. 50, Standard: 20).

Du erhältst ein Array von Issues mit ID, Bezeichner, Titel, Beschreibung, State, Assignee, Priorität und Erstellungsdatum zurück.

```
Team ID: abc123def456
State: started
Limit: 50
```

### Details eines bestimmten Linear-Issues abrufen

Der `linear/get-issue` Warp holt alle Details für ein einzelnes **Linear-Issue** – ID, Bezeichner, Titel, Beschreibung, State, Assignee, Priorität, URL und Erstellungsdatum.

```
Issue ID: xyz789ghi012
```

### Linear-Issues aktualisieren

Der `linear/update-issue` Warp ermöglicht es dir, ein bestehendes **Linear-Issue** über die Integration zu aktualisieren. Du kannst Titel, Beschreibung, State, Assignee oder Priorität ändern.

Du benötigst die Issue-ID und alle Felder, die du aktualisieren möchtest (lasse Felder leer, um aktuelle Werte beizubehalten).

Du erhältst die aktualisierten Issue-Details und den Erfolgsstatus zurück.

```
Issue ID: xyz789ghi012
State ID: started
Priority: 1
```

### Kommentare zu Linear-Issues hinzufügen

Verwende `linear/add-comment`, um einen Kommentar zu einem **Linear-Issue** über die Integration hinzuzufügen. Der Kommentar-Body unterstützt Markdown.

Du erhältst die Kommentar-ID, Body, Autor, Erstellungsdatum und Erfolgsstatus zurück.

```
Issue ID: xyz789ghi012
Comment Body: This has been fixed in the latest commit. Please test and close if working.
```

## Linear-Integrations-Authentifizierung

Wir verwenden API-Key-Authentifizierung für die Linear-Integration. Dein API Key bietet vollen Zugriff auf deinen Linear-Workspace basierend auf deinen Benutzerberechtigungen.

### Welche Berechtigungen du benötigst

Dein API Key erbt die Berechtigungen deines Linear-Benutzerkontos:
* **Voller Zugriff**: Wenn du Administrator bist, kannst du alle Teams und Issues verwalten
* **Team-Zugriff**: Du kannst nur auf Teams zugreifen, in denen du Mitglied bist
* **Issue-Zugriff**: Du kannst nur auf Issues zugreifen, die du anzeigen darfst

### Sicherheitstipps

Einige Dinge, die du beachten solltest:

* Rotiere API Keys regelmäßig
* Verwende API Keys nur aus sicheren Umgebungen
* Committe niemals API Keys in die Versionskontrolle
* Verwende Umgebungsvariablen oder Secret Manager in der Produktion
* Widerrufe Keys sofort, wenn sie kompromittiert wurden

### Rate Limits

Linear begrenzt authentifizierte Anfragen auf 10.000 pro Stunde. Du siehst Rate-Limit-Informationen in den Response-Headern. Die Linear-Integration behandelt Rate Limiting automatisch.

## Wie die Linear-Integration funktioniert

Alle Linear-Integrations-Anfragen gehen an `https://api.linear.app/graphql` mit deinem API Key im Authorization-Header. Wir verwenden die Linear GraphQL API, daher folgt alles ihrem Standardformat.

GraphQL-Antworten enthalten Daten und eventuelle Fehler. Diese Linear-Integration übernimmt die gesamte API-Kommunikation für dich.

## Linear-Integrations-Anwendungsfälle und Beispiele

### Automatische Bug-Meldung

Erstelle automatisch ein **Linear-Issue**, wenn deine App einen Bug erkennt, mit der Linear-Integration:

```
Action: Create Issue
Team ID: [Ihre Team ID]
Title: [BUG] Login validation failing
Description: ## Description
The login form is not validating email addresses correctly.

## Steps to Reproduce
1. Go to login page
2. Enter invalid email
3. Submit form

Priority: 2 (High)
```

### Linear-Issue-Triage-Workflow

Filtere **Linear-Issues**, um zu finden, was Aufmerksamkeit benötigt, mit der Linear-Integration:

```
Step 1: List Issues
Team ID: abc123def456
State: unstarted

Step 2: Get Issue
Issue ID: [aus Liste oben]

Step 3: Update Issue
Issue ID: [aus Schritt 2]
State ID: started
Assignee ID: [Ihre Benutzer-ID]
```

### Tägliche Standup-Automatisierung

Liste alle gestarteten Issues für ein Team auf:

```
Action: List Issues
Team ID: abc123def456
State: started
Limit: 50
```

### Issue-State-Verwaltung

Bewege ein Issue durch Workflow-States:

```
Action: Update Issue
Issue ID: xyz789ghi012
State ID: started

# Später, wenn die Arbeit erledigt ist:
Action: Update Issue
Issue ID: xyz789ghi012
State ID: completed
```

### Fortschrittsverfolgung mit Kommentaren

Füge Kommentare hinzu, um den Fortschritt zu verfolgen:

```
Action: Add Comment
Issue ID: xyz789ghi012
Comment Body: ## Progress Update

- [x] Implemented login validation
- [x] Added error messages
- [ ] Write tests
- [ ] Code review

ETA: Tomorrow
```

## IDs finden

### Team-IDs

Verwende den **List Teams** Warp, um Team-IDs zu finden. Die Antwort enthält:
* `id`: Verwende dies für Team-Operationen
* `name`: Team-Name zur Referenz
* `key`: Team-Key (kurzer Bezeichner)

### Issue-IDs

Verwende den **List Issues** Warp, um Issue-IDs zu finden. Die Antwort enthält:
* `id`: Verwende dies für Issue-Operationen
* `identifier`: Menschenlesbarer Bezeichner (z.B. "ENG-123")

### Benutzer-/Assignee-IDs

Um Benutzer-IDs für Zuweisungen zu finden:
1. Verwende **Get Issue** für ein bestehendes Issue
2. Überprüfe das `assignee.id` Feld in der Antwort
3. Oder überprüfe die Benutzer-URLs in der Linear-Weboberfläche

### State-IDs

Linear-States sind typischerweise:
* `backlog`: Issues im Backlog
* `unstarted`: Noch nicht gestartet
* `started`: In Bearbeitung
* `completed`: Erledigt
* `canceled`: Abgebrochen

Verwende **Get Issue**, um die aktuelle State-ID zu sehen, oder überprüfe die Linear-API-Dokumentation für State-IDs in deinem Workspace.

## Fehlerbehebung bei Linear-Integrations-Problemen

### "Unauthorized" Fehler

Dein API Key funktioniert nicht. Überprüfe, dass:
* Die Umgebungsvariable `LINEAR_API_KEY` korrekt gesetzt ist
* Der API Key nicht widerrufen wurde
* Der API Key gültig und nicht abgelaufen ist

Wenn alles andere fehlschlägt, generiere den API Key neu.

### "Team not found" Fehler

Linear kann das Team nicht finden. Stelle sicher, dass:
* Die Team-ID korrekt ist (verwende "List Teams" zur Überprüfung)
* Du Mitglied des Teams bist
* Du die Team-ID verwendest (nicht den Team-Key)

### "Issue not found" Fehler

Linear kann das Issue nicht finden. Überprüfe, dass:
* Die Issue-ID korrekt ist (verwende "List Issues" zur Überprüfung)
* Du Berechtigung zum Anzeigen des Issues hast
* Du die Issue-ID verwendest (nicht den Bezeichner wie "ENG-123")

### "Invalid state" Fehler

Die State-ID ist ungültig. Überprüfe, dass:
* Du eine gültige State-ID aus deinem Workspace verwendest
* Der State in deinem Linear-Workflow existiert
* Du "Get Issue" verwendest, um gültige State-IDs zu sehen

### Rate Limit überschritten

Du erreichst die Rate Limits von Linear. Warte auf das Reset oder implementiere Throttling in deiner App. Authentifizierte Anfragen erhalten 10.000 Anfragen/Stunde, was für die meisten Anwendungsfälle ausreichen sollte.

### Schnelle Debugging-Tipps

* Beginne mit "List Teams", um zu überprüfen, ob deine Einrichtung funktioniert
* Verwende List-Operationen, um korrekte IDs zu finden
* Überprüfe, dass du Zugriff auf Teams/Issues hast
* Lies die Fehlermeldungen – sie sagen dir normalerweise genau, was falsch ist

## Best Practices

### ID-Verwaltung

Verwende immer zuerst "List Teams", um Team-IDs zu erhalten. Speichere Team-IDs zur Wiederverwendung. Verwende Issue-Bezeichner (wie "ENG-123") für menschliche Referenz, aber verwende IDs für API-Aufrufe.

### State-Verwaltung

Verstehe die Workflow-States deines Workspaces. Verwende konsistente State-Übergänge. Dokumentiere State-Änderungen in Kommentaren.

### Fehlerbehandlung

Prüfe immer auf GraphQL-Fehler in Antworten. Implementiere Retry-Logik für Rate-Limit-Fehler und protokolliere alles für das Debugging. Deine Benutzer werden dir für klare Fehlermeldungen danken.

### Rate Limiting

Behalte Rate-Limit-Header im Auge. Verwende exponentielles Backoff für Retries, cache Antworten, wenn möglich, und batchiere Operationen, wenn möglich.

### Sicherheit

Committe niemals API Keys in die Versionskontrolle. Verwende `.gitignore` für Umgebungsdateien, rotiere API Keys regelmäßig und auditiere die Key-Nutzung regelmäßig.

### Issue-Verwaltung

Verwende beschreibende Titel. Füge detaillierte Beschreibungen mit Markdown hinzu. Setze angemessene Prioritäten. Weise Issues prompt zu. Füge Kommentare für Fortschritts-Updates hinzu.

## Erweiterte Nutzung

### GraphQL-Variablen

Alle Warps verwenden GraphQL-Variablen für sichere Parameterinjektion. Variablen werden automatisch escaped und korrekt typisiert.

### Markdown-Unterstützung

Linear unterstützt GitHub Flavored Markdown in Issue-Beschreibungen, Kommentaren und allen Textfeldern. Du kannst Überschriften, Listen, Code-Blöcke, Task-Listen, Tabellen, Mentions (@username) und Issue-Referenzen (#123) verwenden.

### Workflow-Automatisierung

Kombiniere mehrere Warps für Automatisierung:
1. **List Issues** → Finde Issues, die Aufmerksamkeit benötigen
2. **Get Issue** → Hole Details
3. **Update Issue** → Ändere State/Assignee
4. **Add Comment** → Protokolliere die Änderung

### Integrations-Muster

* **CI/CD-Integration**: Erstelle Issues aus Build-Fehlern
* **Monitoring-Integration**: Erstelle Issues aus Alerts
* **Support-Integration**: Erstelle Issues aus Support-Tickets
* **Code Review**: Aktualisiere Issues, wenn PRs gemerged werden

## Ressourcen

* [Linear API Dokumentation](https://developers.linear.app/docs/graphql/overview)
* [Linear GraphQL API Referenz](https://developers.linear.app/docs/graphql/working-with-the-graphql-api)
* [Linear API Authentifizierung](https://developers.linear.app/docs/graphql/authentication)
* [Linear GraphQL Explorer](https://linear.app/developers/graphql)
* [Linear API Rate Limits](https://developers.linear.app/docs/graphql/working-with-the-graphql-api#rate-limits)
* [Linear Markdown Guide](https://linear.app/docs/markdown)

---

## Fazit

Du bist jetzt bereit, die Linear-Integration in JoAi zu verwenden! Diese Linear-Integration ermöglicht es dir, deinen Projektmanagement-Workflow zu automatisieren, Issues und Teams zu verwalten und deinen Entwicklungsprozess zu optimieren. Beginne mit einfachen Operationen wie dem Erstellen von Issues, dann erkunde erweiterte Funktionen wie automatisierte State-Verwaltung und Fortschrittsverfolgung.

Denke daran, deinen API Key sicher zu halten, ihn regelmäßig zu rotieren und deine API-Rate-Limits zu überwachen. Für erweiterte Automatisierung solltest du diese Linear-Integration mit Webhooks und anderen JoAi-Funktionen kombinieren. Erkunde andere JoAi-Integrationen, um umfassende Automatisierungs-Workflows zu erstellen.

**Hinweis**: Diese Linear-Integration verwendet die Linear GraphQL API. Für die neuesten Funktionen und Fähigkeiten verweise auf die [Linear API-Dokumentation](https://developers.linear.app/docs/graphql/overview).
