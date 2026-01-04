---
title: 'Linear Integration Guide für JoAi'
description: 'Richten Sie die Linear-Integration mit JoAi in 5 Minuten ein. Erstellen Sie Issues, verwalten Sie Teams, aktualisieren Sie States und automatisieren Sie Projekt-Workflows mit Linear GraphQL API. Komplette Anleitung.'
category: 'integrations'
tags: ['linear', 'integration', 'api', 'projektmanagement', 'graphql']
author: 'JoAi Team'
publishedAt: '2024-01-20'
updatedAt: '2024-01-20'
featured: false
difficulty: 'intermediate'
readTime: 12
keywords:
  ['linear integration', 'linear integration einrichten', 'linear mit joai verbinden', 'linear api integration', 'linear projektmanagement', 'linear workflow automatisierung', 'linear graphql api', 'linear api key', 'linear issues api', 'linear teams']
relatedArticles: []
faqs:
  - question: 'Wie lange dauert die Einrichtung der Linear-Integration?'
    answer: 'Die Einrichtung dauert etwa 5 Minuten. Sie müssen einen Linear API Key erstellen und ihn als Umgebungsvariable setzen.'
  - question: 'Welche Berechtigungen benötigt die Linear-Integration?'
    answer: 'Die Integration benötigt einen Linear API Key. Ihr API Key erbt die Berechtigungen Ihres Linear-Benutzerkontos - Sie können auf Teams zugreifen, in denen Sie Mitglied sind, und auf Issues, die Sie anzeigen dürfen.'
  - question: 'Kann ich diese Integration mit allen Linear-Teams verwenden?'
    answer: 'Ja, Sie können auf alle Teams zugreifen, in denen Sie Mitglied sind. Wenn Sie Administrator sind, können Sie alle Teams und Issues in Ihrem Workspace verwalten.'
  - question: 'Wie hoch ist das Rate Limit für Linear API-Anfragen?'
    answer: 'Authentifizierte Anfragen haben ein Rate Limit von 10.000 Anfragen pro Stunde. Die Integration behandelt Rate Limiting automatisch.'
  - question: 'Wie finde ich Team-IDs und Issue-IDs?'
    answer: 'Verwenden Sie den "List Teams" Warp, um Team-IDs zu finden, und "List Issues", um Issue-IDs zu finden. Die Antwort enthält sowohl IDs als auch menschenlesbare Bezeichner.'
llmAnswer: 'Richten Sie die Linear-Integration in JoAi ein, indem Sie einen API Key aus Linear Settings > API erstellen und ihn als LINEAR_API_KEY Umgebungsvariable setzen. Dies ermöglicht das Erstellen von Issues, das Verwalten von Teams, das Aktualisieren von States und das Hinzufügen von Kommentaren über die Linear GraphQL API.'
---

Die Linear-Integration für JoAi ermöglicht es Ihnen, Ihre Linear-Issues, Teams und Projekte direkt aus Ihrem Arbeitsbereich zu verwalten. Diese Linear-Integration nutzt die Linear GraphQL API, damit Sie Ihren Projektmanagement-Workflow automatisieren können, ohne JoAi zu verlassen. Die Einrichtung der Linear-Integration dauert nur 5 Minuten und eröffnet leistungsstarke Automatisierungsmöglichkeiten.

## Was Sie lernen werden

* Wie Sie die Linear-Integration mit API Keys einrichten
* Erstellen und Verwalten von Linear-Issues und Teams
* Aktualisieren von Issue-States und Prioritäten
* Hinzufügen von Kommentaren zur Fortschrittsverfolgung
* Fehlerbehebung bei häufigen Linear-Integrationsfehlern
* Best Practices für Linear-API-Authentifizierung und Sicherheit

## Wie Sie die Linear-Integration einrichten

Sie benötigen einen Linear API Key, um diese Linear-Integration zu verwenden. So richten Sie ihn in nur wenigen Minuten ein.

### Erstellen Sie Ihren Linear API Key

Melden Sie sich in Ihrem Linear-Konto unter [linear.app](https://linear.app) an und navigieren Sie zu **Settings** → **API** (oder gehen Sie direkt zu [https://linear.app/settings/api](https://linear.app/settings/api)).

Klicken Sie auf **"Create API Key"** und geben Sie ihm einen Namen wie "JoAi Integration".

**Wichtig**: Kopieren Sie den API Key sofort - Linear zeigt ihn Ihnen nicht erneut an!

### Konfigurieren Sie die Linear-Integrations-Umgebungsvariable

Setzen Sie die Umgebungsvariable `LINEAR_API_KEY` mit Ihrem **Linear API Key**:

**macOS/Linux:**
```bash
export LINEAR_API_KEY="your_api_key_here"
```

Um es dauerhaft zu machen, fügen Sie es zu Ihrer `~/.zshrc` oder `~/.bashrc` hinzu:
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

### Überprüfen Sie die Linear-Integration-Einrichtung

Versuchen Sie den "List Teams" Warp, um zu überprüfen, ob Ihre **Linear-Integration** funktioniert. Wenn erfolgreich, erhalten Sie eine Liste aller Teams in Ihrem Linear-Workspace.

## Linear-Integrations-Funktionen und Aktionen

### Linear-Teams auflisten

Verwenden Sie den `linear/list-teams` Warp, um alle Teams in Ihrem Linear-Workspace abzurufen. Dies ist normalerweise der erste Schritt, um Team-IDs zu finden, die für andere Operationen benötigt werden.

Sie erhalten zurück:
* `TEAMS`: Array von Team-Objekten mit ID, Name, Key und Beschreibung
* `COUNT`: Anzahl der gefundenen Teams

Verwenden Sie dies, um Team-IDs zu finden, bevor Sie Issues erstellen oder auflisten.

### Linear-Issues erstellen

Verwenden Sie den `linear/create-issue` Warp, um ein neues **Linear-Issue** in einem beliebigen Team über die Linear-Integration zu erstellen.

Sie benötigen:
* Team ID (erforderlich) - Holen Sie sich diese von "List Teams"
* Titel (erforderlich)
* Beschreibung (optional, unterstützt Markdown)
* Assignee ID (optional)
* Priorität (optional): `0` = Keine Priorität, `1` = Dringend, `2` = Hoch, `3` = Mittel, `4` = Niedrig

Sie erhalten die Issue-ID, Titel, URL, Bezeichner (z.B. "ENG-123") und Erfolgsstatus zurück.

Hier ist ein Beispiel:
```
Team ID: abc123def456
Title: Fix login bug
Description: The login form is not validating email addresses correctly.
Priority: 2
```

### Linear-Issues auflisten

Verwenden Sie `linear/list-issues`, um **Linear-Issues** in einem Team über die Integration aufzulisten. Sie können nach Assignee, State filtern und Ergebnisse begrenzen (max. 50, Standard: 20).

Sie erhalten ein Array von Issues mit ID, Bezeichner, Titel, Beschreibung, State, Assignee, Priorität und Erstellungsdatum zurück.

```
Team ID: abc123def456
State: started
Limit: 50
```

### Details eines bestimmten Linear-Issues abrufen

Der `linear/get-issue` Warp holt alle Details für ein einzelnes **Linear-Issue** - ID, Bezeichner, Titel, Beschreibung, State, Assignee, Priorität, URL und Erstellungsdatum.

```
Issue ID: xyz789ghi012
```

### Linear-Issues aktualisieren

Der `linear/update-issue` Warp ermöglicht es Ihnen, ein bestehendes **Linear-Issue** über die Integration zu aktualisieren. Sie können Titel, Beschreibung, State, Assignee oder Priorität ändern.

Sie benötigen die Issue-ID und alle Felder, die Sie aktualisieren möchten (lassen Sie Felder leer, um aktuelle Werte beizubehalten).

Sie erhalten die aktualisierten Issue-Details und den Erfolgsstatus zurück.

```
Issue ID: xyz789ghi012
State ID: started
Priority: 1
```

### Kommentare zu Linear-Issues hinzufügen

Verwenden Sie `linear/add-comment`, um einen Kommentar zu einem **Linear-Issue** über die Integration hinzuzufügen. Der Kommentar-Body unterstützt Markdown.

Sie erhalten die Kommentar-ID, Body, Autor, Erstellungsdatum und Erfolgsstatus zurück.

```
Issue ID: xyz789ghi012
Comment Body: This has been fixed in the latest commit. Please test and close if working.
```

## Linear-Integrations-Authentifizierung

Wir verwenden API-Key-Authentifizierung für die Linear-Integration. Ihr API Key bietet vollen Zugriff auf Ihren Linear-Workspace basierend auf Ihren Benutzerberechtigungen.

### Welche Berechtigungen Sie benötigen

Ihr API Key erbt die Berechtigungen Ihres Linear-Benutzerkontos:
* **Voller Zugriff**: Wenn Sie Administrator sind, können Sie alle Teams und Issues verwalten
* **Team-Zugriff**: Sie können nur auf Teams zugreifen, in denen Sie Mitglied sind
* **Issue-Zugriff**: Sie können nur auf Issues zugreifen, die Sie anzeigen dürfen

### Sicherheitstipps

Einige Dinge, die Sie beachten sollten:

* Rotieren Sie API Keys regelmäßig
* Verwenden Sie API Keys nur aus sicheren Umgebungen
* Committen Sie niemals API Keys in die Versionskontrolle
* Verwenden Sie Umgebungsvariablen oder Secret Manager in der Produktion
* Widerrufen Sie Keys sofort, wenn sie kompromittiert wurden

### Rate Limits

Linear begrenzt authentifizierte Anfragen auf 10.000 pro Stunde. Sie sehen Rate-Limit-Informationen in den Response-Headern. Die Linear-Integration behandelt Rate Limiting automatisch.

## Wie die Linear-Integration funktioniert

Alle Linear-Integrations-Anfragen gehen an `https://api.linear.app/graphql` mit Ihrem API Key im Authorization-Header. Wir verwenden die Linear GraphQL API, daher folgt alles ihrem Standardformat.

GraphQL-Antworten enthalten Daten und eventuelle Fehler. Diese Linear-Integration übernimmt die gesamte API-Kommunikation für Sie.

## Linear-Integrations-Anwendungsfälle und Beispiele

### Automatische Bug-Meldung

Erstellen Sie automatisch ein **Linear-Issue**, wenn Ihre App einen Bug erkennt, mit der Linear-Integration:

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

Filtern Sie **Linear-Issues**, um zu finden, was Aufmerksamkeit benötigt, mit der Linear-Integration:

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

Listen Sie alle gestarteten Issues für ein Team auf:

```
Action: List Issues
Team ID: abc123def456
State: started
Limit: 50
```

### Issue-State-Verwaltung

Bewegen Sie ein Issue durch Workflow-States:

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

Fügen Sie Kommentare hinzu, um den Fortschritt zu verfolgen:

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

Verwenden Sie den **List Teams** Warp, um Team-IDs zu finden. Die Antwort enthält:
* `id`: Verwenden Sie dies für Team-Operationen
* `name`: Team-Name zur Referenz
* `key`: Team-Key (kurzer Bezeichner)

### Issue-IDs

Verwenden Sie den **List Issues** Warp, um Issue-IDs zu finden. Die Antwort enthält:
* `id`: Verwenden Sie dies für Issue-Operationen
* `identifier`: Menschenlesbarer Bezeichner (z.B. "ENG-123")

### Benutzer-/Assignee-IDs

Um Benutzer-IDs für Zuweisungen zu finden:
1. Verwenden Sie **Get Issue** für ein bestehendes Issue
2. Überprüfen Sie das `assignee.id` Feld in der Antwort
3. Oder überprüfen Sie die Benutzer-URLs in der Linear-Weboberfläche

### State-IDs

Linear-States sind typischerweise:
* `backlog`: Issues im Backlog
* `unstarted`: Noch nicht gestartet
* `started`: In Bearbeitung
* `completed`: Erledigt
* `canceled`: Abgebrochen

Verwenden Sie **Get Issue**, um die aktuelle State-ID zu sehen, oder überprüfen Sie die Linear-API-Dokumentation für State-IDs in Ihrem Workspace.

## Fehlerbehebung bei Linear-Integrations-Problemen

### "Unauthorized" Fehler

Ihr API Key funktioniert nicht. Überprüfen Sie, dass:
* Die Umgebungsvariable `LINEAR_API_KEY` korrekt gesetzt ist
* Der API Key nicht widerrufen wurde
* Der API Key gültig und nicht abgelaufen ist

Wenn alles andere fehlschlägt, generieren Sie den API Key neu.

### "Team not found" Fehler

Linear kann das Team nicht finden. Stellen Sie sicher, dass:
* Die Team-ID korrekt ist (verwenden Sie "List Teams" zur Überprüfung)
* Sie Mitglied des Teams sind
* Sie die Team-ID verwenden (nicht den Team-Key)

### "Issue not found" Fehler

Linear kann das Issue nicht finden. Überprüfen Sie, dass:
* Die Issue-ID korrekt ist (verwenden Sie "List Issues" zur Überprüfung)
* Sie Berechtigung zum Anzeigen des Issues haben
* Sie die Issue-ID verwenden (nicht den Bezeichner wie "ENG-123")

### "Invalid state" Fehler

Die State-ID ist ungültig. Überprüfen Sie, dass:
* Sie eine gültige State-ID aus Ihrem Workspace verwenden
* Der State in Ihrem Linear-Workflow existiert
* Sie "Get Issue" verwenden, um gültige State-IDs zu sehen

### Rate Limit überschritten

Sie erreichen die Rate Limits von Linear. Warten Sie auf das Reset oder implementieren Sie Throttling in Ihrer App. Authentifizierte Anfragen erhalten 10.000 Anfragen/Stunde, was für die meisten Anwendungsfälle ausreichen sollte.

### Schnelle Debugging-Tipps

* Beginnen Sie mit "List Teams", um zu überprüfen, ob Ihre Einrichtung funktioniert
* Verwenden Sie List-Operationen, um korrekte IDs zu finden
* Überprüfen Sie, dass Sie Zugriff auf Teams/Issues haben
* Lesen Sie die Fehlermeldungen - sie sagen Ihnen normalerweise genau, was falsch ist

## Best Practices

### ID-Verwaltung

Verwenden Sie immer zuerst "List Teams", um Team-IDs zu erhalten. Speichern Sie Team-IDs zur Wiederverwendung. Verwenden Sie Issue-Bezeichner (wie "ENG-123") für menschliche Referenz, aber verwenden Sie IDs für API-Aufrufe.

### State-Verwaltung

Verstehen Sie die Workflow-States Ihres Workspaces. Verwenden Sie konsistente State-Übergänge. Dokumentieren Sie State-Änderungen in Kommentaren.

### Fehlerbehandlung

Prüfen Sie immer auf GraphQL-Fehler in Antworten. Implementieren Sie Retry-Logik für Rate-Limit-Fehler und protokollieren Sie alles für das Debugging. Ihre Benutzer werden Ihnen für klare Fehlermeldungen danken.

### Rate Limiting

Behalten Sie Rate-Limit-Header im Auge. Verwenden Sie exponentielles Backoff für Retries, cachen Sie Antworten, wenn möglich, und batchieren Sie Operationen, wenn möglich.

### Sicherheit

Committen Sie niemals API Keys in die Versionskontrolle. Verwenden Sie `.gitignore` für Umgebungsdateien, rotieren Sie API Keys regelmäßig und auditieren Sie die Key-Nutzung regelmäßig.

### Issue-Verwaltung

Verwenden Sie beschreibende Titel. Fügen Sie detaillierte Beschreibungen mit Markdown hinzu. Setzen Sie angemessene Prioritäten. Weisen Sie Issues prompt zu. Fügen Sie Kommentare für Fortschritts-Updates hinzu.

## Erweiterte Nutzung

### GraphQL-Variablen

Alle Warps verwenden GraphQL-Variablen für sichere Parameterinjektion. Variablen werden automatisch escaped und korrekt typisiert.

### Markdown-Unterstützung

Linear unterstützt GitHub Flavored Markdown in Issue-Beschreibungen, Kommentaren und allen Textfeldern. Sie können Überschriften, Listen, Code-Blöcke, Task-Listen, Tabellen, Mentions (@username) und Issue-Referenzen (#123) verwenden.

### Workflow-Automatisierung

Kombinieren Sie mehrere Warps für Automatisierung:
1. **List Issues** → Finden Sie Issues, die Aufmerksamkeit benötigen
2. **Get Issue** → Holen Sie Details
3. **Update Issue** → Ändern Sie State/Assignee
4. **Add Comment** → Protokollieren Sie die Änderung

### Integrations-Muster

* **CI/CD-Integration**: Erstellen Sie Issues aus Build-Fehlern
* **Monitoring-Integration**: Erstellen Sie Issues aus Alerts
* **Support-Integration**: Erstellen Sie Issues aus Support-Tickets
* **Code Review**: Aktualisieren Sie Issues, wenn PRs gemerged werden

## Ressourcen

* [Linear API Dokumentation](https://developers.linear.app/docs/graphql/overview)
* [Linear GraphQL API Referenz](https://developers.linear.app/docs/graphql/working-with-the-graphql-api)
* [Linear API Authentifizierung](https://developers.linear.app/docs/graphql/authentication)
* [Linear GraphQL Explorer](https://linear.app/developers/graphql)
* [Linear API Rate Limits](https://developers.linear.app/docs/graphql/working-with-the-graphql-api#rate-limits)
* [Linear Markdown Guide](https://linear.app/docs/markdown)

---

## Fazit

Sie sind jetzt bereit, die Linear-Integration in JoAi zu verwenden! Diese Linear-Integration ermöglicht es Ihnen, Ihren Projektmanagement-Workflow zu automatisieren, Issues und Teams zu verwalten und Ihren Entwicklungsprozess zu optimieren. Beginnen Sie mit einfachen Operationen wie dem Erstellen von Issues, dann erkunden Sie erweiterte Funktionen wie automatisierte State-Verwaltung und Fortschrittsverfolgung.

Denken Sie daran, Ihren API Key sicher zu halten, ihn regelmäßig zu rotieren und Ihre API-Rate-Limits zu überwachen. Für erweiterte Automatisierung sollten Sie diese Linear-Integration mit Webhooks und anderen JoAi-Funktionen kombinieren. Erkunden Sie andere JoAi-Integrationen, um umfassende Automatisierungs-Workflows zu erstellen.

**Hinweis**: Diese Linear-Integration verwendet die Linear GraphQL API. Für die neuesten Funktionen und Fähigkeiten verweisen Sie auf die [Linear API-Dokumentation](https://developers.linear.app/docs/graphql/overview).
