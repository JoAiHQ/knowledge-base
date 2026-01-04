---
title: 'GitHub Integration Guide'
description: 'Erfahren Sie, wie Sie die GitHub-Integration in Warpbase einrichten und verwenden. Erstellen Sie Issues, verwalten Sie Pull Requests, durchsuchen Sie Repositories und automatisieren Sie Ihren GitHub-Workflow.'
category: 'integrations'
tags: ['github', 'integration', 'api', 'automatisierung', 'version-control']
author: 'JoAi Team'
publishedAt: '2024-01-20'
updatedAt: '2024-01-20'
featured: false
difficulty: 'intermediate'
readTime: 12
keywords:
  ['github', 'git', 'repository', 'issues', 'pull requests', 'api', 'automatisierung']
relatedArticles: []
faqs:
  - question: 'Welche Berechtigungen benötigt die GitHub-Integration?'
    answer: 'Die Integration benötigt ein Personal Access Token mit dem `repo` Scope für volle Funktionalität. Zusätzliche Scopes wie `read:org` und `read:user` können für Organisations-Repositories erforderlich sein.'
  - question: 'Kann ich diese Integration mit privaten Repositories verwenden?'
    answer: 'Ja, solange Ihr Personal Access Token den `repo` Scope hat, können Sie auf private Repositories zugreifen und diese verwalten.'
  - question: 'Wie hoch ist das Rate Limit für GitHub API-Anfragen?'
    answer: 'Authentifizierte Anfragen haben ein Rate Limit von 5.000 Anfragen pro Stunde. Nicht authentifizierte Anfragen sind auf 60 Anfragen pro Stunde begrenzt.'
  - question: 'Wie erstelle ich einen Pull Request über mehrere Repositories hinweg?'
    answer: 'Verwenden Sie das Format `username:branch-name` für das Head Branch Feld, wenn Sie einen Pull Request von einem Fork oder einem anderen Repository erstellen.'
llmAnswer: 'Die GitHub-Integration für Warpbase ermöglicht es Ihnen, Repositories zu verwalten, Issues und Pull Requests zu erstellen, Kommentare hinzuzufügen und Repositories mit der GitHub REST API v3 zu durchsuchen. Die Einrichtung erfordert ein Personal Access Token mit entsprechenden Scopes.'
---

Die GitHub-Integration ermöglicht es Ihnen, Ihre GitHub-Repositories, Issues und Pull Requests direkt aus Warpbase zu verwalten. Wir haben dies mit der GitHub REST API v3 gebaut, damit Sie Ihren GitHub-Workflow automatisieren können, ohne Ihren Arbeitsbereich zu verlassen.

Hier ist, was Sie tun können:

* Issues erstellen und verwalten
* Pull Requests erstellen
* Repositories durchsuchen
* Kommentare zu Issues und PRs hinzufügen
* Repository-Informationen abrufen

## Erste Schritte

Sie benötigen ein GitHub Personal Access Token, um diese Integration zu verwenden. So richten Sie es ein.

### Erstellen Sie Ihr GitHub-Token

Gehen Sie zu [GitHub Settings > Developer settings > Personal access tokens](https://github.com/settings/tokens) und klicken Sie auf **"Generate new token"** → **"Generate new token (classic)"**.

Geben Sie ihm einen Namen wie "Warpbase Integration" und setzen Sie ein Ablaufdatum (wir empfehlen 90 Tage). Für Scopes benötigen Sie:

* **`repo`** - Dies gibt Ihnen vollständige Kontrolle über private Repositories. Sie benötigen dies für die meisten Operationen wie das Erstellen von Issues und PRs.
* **`read:org`** - Nur wenn Sie mit Organisations-Repositories arbeiten
* **`read:user`** - Zum Lesen von Benutzerprofildaten

Klicken Sie auf **"Generate token"** und kopieren Sie es sofort. GitHub zeigt es Ihnen nicht erneut an.

### Setzen Sie Ihre Umgebungsvariable

Setzen Sie die Umgebungsvariable `GITHUB_TOKEN` mit Ihrem Token:

**macOS/Linux:**
```bash
export GITHUB_TOKEN="your_token_here"
```

Um es dauerhaft zu machen, fügen Sie es zu Ihrer `~/.zshrc` oder `~/.bashrc` hinzu:
```bash
echo 'export GITHUB_TOKEN="your_token_here"' >> ~/.zshrc
source ~/.zshrc
```

**Windows (PowerShell):**
```powershell
$env:GITHUB_TOKEN="your_token_here"
```

**Windows (Command Prompt):**
```cmd
setx GITHUB_TOKEN "your_token_here"
```

**Docker:**
```bash
docker run -e GITHUB_TOKEN="your_token_here" ...
```

### Testen Sie es

Versuchen Sie den "Get Repository" Warp mit einem öffentlichen Repo, um zu überprüfen, ob alles funktioniert:

* Owner: `octocat`
* Repository: `Hello-World`

Wenn Sie Repository-Informationen mit Stars und Forks sehen, sind Sie fertig.

## Was Sie tun können

### Issues erstellen

Verwenden Sie den `github/create-issue` Warp, um ein neues Issue in einem beliebigen Repository zu erstellen.

Sie benötigen:
* Owner (Benutzername oder Organisation)
* Repository-Name
* Titel
* Body (optional, unterstützt Markdown)
* Labels (optional, kommagetrennt wie "bug,enhancement")
* Assignees (optional, kommagetrennte Benutzernamen)

Sie erhalten die Issue-Nummer, URL und die interne GitHub-ID zurück.

Hier ist ein Beispiel:
```
Owner: myusername
Repository: myproject
Title: Fix login bug
Body: The login form is not validating email addresses correctly.
Labels: bug,priority-high
Assignees: developer1,developer2
```

### Repository-Informationen abrufen

Der `github/get-repository` Warp gibt Ihnen alle Details über ein Repository.

Geben Sie einfach den Owner und den Repository-Namen an. Sie erhalten Name, Beschreibung, Stars, Forks, Sprache und Clone-URLs zurück.

```
Owner: facebook
Repository: react
```

### Issues auflisten

Verwenden Sie `github/list-issues`, um Issues in einem Repo aufzulisten. Sie können nach Status (`open`, `closed` oder `all`), Labels, Assignee filtern und Ergebnisse begrenzen (max. 100, Standard: 30).

Sie erhalten ein Array von Issues und die Gesamtzahl zurück.

```
Owner: myusername
Repository: myproject
State: open
Labels: bug
Assignee: developer1
Limit: 50
```

### Ein bestimmtes Issue abrufen

Der `github/get-issue` Warp holt alle Details für ein einzelnes Issue - Titel, Body, Status, Labels, Assignees und Autor.

```
Owner: myusername
Repository: myproject
Issue Number: 42
```

### Pull Requests erstellen

Der `github/create-pull-request` Warp erstellt einen neuen PR, um Änderungen zwischen Branches zu mergen.

Sie benötigen den Owner, Repo, Titel, Head Branch (Quelle) und Base Branch (Ziel, normalerweise `main`). Für Cross-Repo-PRs verwenden Sie das Format `username:branch` für den Head Branch. Setzen Sie `Draft: true`, wenn Sie einen Draft-PR möchten.

Sie erhalten die PR-Nummer, URL und den Status zurück.

```
Owner: myusername
Repository: myproject
Title: Add user authentication
Body: Implements OAuth2 authentication flow with JWT tokens.
Head Branch: feature/auth
Base Branch: main
Draft: false
```

### Kommentare hinzufügen

Verwenden Sie `github/add-comment`, um einen Kommentar zu einem Issue oder PR hinzuzufügen. Der Kommentar-Body unterstützt Markdown.

Sie erhalten die Kommentar-ID und URL zurück.

```
Owner: myusername
Repository: myproject
Issue Number: 42
Comment Body: This has been fixed in the latest commit. Please test and close if working.
```

### Repositories durchsuchen

Der `github/search-repositories` Warp ermöglicht es Ihnen, GitHub mit ihrer Suchsyntax zu durchsuchen. Sie können nach Stars, Forks, help-wanted-issues oder aktualisiertem Datum sortieren und Ergebnisse begrenzen (max. 100).

Sie erhalten ein Array von passenden Repositories und die Gesamtzahl zurück.

Einige Suchabfrage-Beispiele:
* `language:javascript stars:>100` - JavaScript-Repos mit 100+ Stars
* `topic:machine-learning` - Repos mit dem Tag machine-learning
* `user:facebook` - Alle Repos von Facebook
* `react in:name` - Repos mit "react" im Namen

```
Query: language:typescript stars:>500
Sort: stars
Order: desc
Limit: 50
```

## Authentifizierung

Wir verwenden Personal Access Tokens (PATs) zur Authentifizierung. Es ist der einfachste Weg, sich mit der GitHub-API zu verbinden.

### Welche Scopes Sie benötigen

Für volle Funktionalität benötigt Ihr Token den `repo` Scope. Dies ermöglicht es Ihnen, Issues zu erstellen, Pull Requests zu erstellen, Kommentare hinzuzufügen und auf private Repositories zuzugreifen.

Sie möchten auch `read:org`, wenn Sie mit Organisations-Repositories arbeiten, und `read:user` für Benutzerprofil-Operationen.

### Sicherheitstipps

Einige Dinge, die Sie beachten sollten:

* Setzen Sie Tokens auf Ablauf (90 Tage ist ein guter Standard)
* Gewähren Sie nur die Scopes, die Sie tatsächlich benötigen
* Rotieren Sie Tokens regelmäßig
* Committen Sie niemals Tokens in die Versionskontrolle
* Verwenden Sie Umgebungsvariablen oder Secret Manager in der Produktion
* Für Org-Repos sollten Sie feingranulierte Tokens oder GitHub Apps in Betracht ziehen

### Rate Limits

GitHub begrenzt authentifizierte Anfragen auf 5.000 pro Stunde. Nicht authentifizierte Anfragen sind auf 60 pro Stunde begrenzt. Sie sehen Rate-Limit-Informationen in den Response-Headern.

## Wie es funktioniert

Alle Anfragen gehen an `https://api.github.com` mit Ihrem Token im Authorization-Header. Wir verwenden die GitHub REST API v3, daher folgt alles ihrem Standardformat.

Rate-Limit-Informationen kommen in Response-Headern zurück - Sie sehen, wie viele Anfragen Sie noch haben und wann das Limit zurückgesetzt wird.

## Praktische Beispiele

### Automatische Bug-Meldung

Erstellen Sie automatisch ein Issue, wenn Ihre App einen Bug erkennt:

```
Action: Create Issue
Owner: mycompany
Repository: myapp
Title: [BUG] Login validation failing
Body: ## Description
The login form is not validating email addresses correctly.

## Steps to Reproduce
1. Go to login page
2. Enter invalid email
3. Submit form

Labels: bug,priority-high
Assignees: backend-team
```

### Repository-Statistiken überwachen

Prüfen Sie, wie es Ihrem Repo geht:

```
Action: Get Repository
Owner: myusername
Repository: myproject
```

Dann schauen Sie sich die Stars-, Forks- und Sprachstatistiken an.

### Issue-Triage

Filtern Sie Issues, um zu finden, was Aufmerksamkeit benötigt:

```
Action: List Issues
Owner: myusername
Repository: myproject
State: open
Labels: bug,needs-triage
Limit: 100
```

### Cross-Repo Pull Requests

Erstellen Sie einen PR von einem Fork mit dem Format `username:branch`:

```
Action: Create Pull Request
Owner: upstream-org
Repository: upstream-repo
Title: Fix typo in README
Body: Fixed a typo in the installation instructions.
Head Branch: myusername:patch-1
Base Branch: main
```

### Trending Repos finden

Suchen Sie nach beliebten Repositories:

```
Action: Search Repositories
Query: language:rust stars:>1000 created:>2024-01-01
Sort: stars
Order: desc
Limit: 20
```

## Fehlerbehebung

### "Bad credentials" Fehler

Ihr Token funktioniert nicht. Überprüfen Sie, dass:
* Die Umgebungsvariable `GITHUB_TOKEN` korrekt gesetzt ist
* Das Token nicht abgelaufen ist
* Das Token die erforderlichen Scopes hat

Wenn alles andere fehlschlägt, generieren Sie das Token neu.

### "Not Found" Fehler

GitHub kann das Repository oder die Ressource nicht finden. Stellen Sie sicher, dass:
* Der Owner und Repository-Name korrekt geschrieben sind
* Das Repository tatsächlich existiert
* Für private Repos Ihr Token den `repo` Scope hat
* Sie Zugriff auf Organisations-Repositories haben, falls erforderlich

### "Resource not accessible by integration" Fehler

Ihr Token hat nicht die richtigen Berechtigungen. Generieren Sie es mit den entsprechenden Scopes neu. Für Organisations-Repos sollten Sie auch Ihre Org-Einstellungen überprüfen.

### Rate Limit überschritten

Sie erreichen die Rate Limits von GitHub. Warten Sie auf das Reset (prüfen Sie den `X-RateLimit-Reset` Header) oder implementieren Sie Throttling in Ihrer App. Authentifizierte Anfragen erhalten 5.000 Anfragen/Stunde, was für die meisten Anwendungsfälle ausreichen sollte.

### "Validation Failed" Fehler

Etwas stimmt mit Ihrer Eingabe nicht. Überprüfen Sie, dass:
* Alle erforderlichen Felder ausgefüllt sind
* Branch-Namen und Benutzernamen korrekt formatiert sind
* Labels tatsächlich im Repository existieren
* Assignee-Benutzernamen gültig sind

### Schnelle Debugging-Tipps

* Testen Sie zuerst mit öffentlichen Repos (wie `octocat/Hello-World`), um Ihre Einrichtung zu überprüfen
* Überprüfen Sie Ihre Token-Scopes nochmals
* Stellen Sie sicher, dass alle erforderlichen Felder ausgefüllt sind
* Lesen Sie die Fehlermeldungen - sie sagen Ihnen normalerweise genau, was falsch ist

## Best Practices

### Token-Verwaltung

Verwenden Sie separate Tokens für Dev, Staging und Produktion. Rotieren Sie sie regelmäßig und speichern Sie sie sicher in Umgebungsvariablen oder Secret Managern. Feingranulierte Tokens sind großartig, wenn Sie sie verwenden können.

### Fehlerbehandlung

Prüfen Sie immer auf API-Fehler in Antworten. Implementieren Sie Retry-Logik für Rate-Limit-Fehler und protokollieren Sie alles für das Debugging. Ihre Benutzer werden Ihnen für klare Fehlermeldungen danken.

### Rate Limiting

Behalten Sie Rate-Limit-Header im Auge. Verwenden Sie exponentielles Backoff für Retries, cachen Sie Antworten, wenn möglich, und batchieren Sie Operationen, wenn möglich.

### Sicherheit

Committen Sie niemals Tokens in die Versionskontrolle. Verwenden Sie `.gitignore` für Umgebungsdateien, beschränken Sie Scopes auf das Minimum, das Sie benötigen, und auditieren Sie die Token-Nutzung regelmäßig.

### Repository-Verwaltung

Halten Sie die Benennung konsistent, dokumentieren Sie Ihre Repo-Struktur, verwenden Sie Labels effektiv und richten Sie Branch-Schutzregeln ein.

## Erweiterte Nutzung

### Cross-Repo Pull Requests

Für PRs von Forks oder anderen Repos verwenden Sie das Format `username:branch-name` für den Head Branch.

### Markdown-Unterstützung

Alle Textfelder unterstützen GitHub Flavored Markdown - Überschriften, Listen, Code-Blöcke, Task-Listen, Tabellen, Mentions (@username) und Issue/PR-Referenzen (#123).

### Webhooks

Während nicht direkt unterstützt, können Sie GitHub-Webhooks mit Warpbase kombinieren, um automatisch Issues zu erstellen, Issues von externen Triggern zu aktualisieren oder Daten zwischen Systemen zu synchronisieren.

## Ressourcen

* [GitHub REST API Docs](https://docs.github.com/en/rest)
* [GitHub API Authentication](https://docs.github.com/en/rest/authentication)
* [Personal Access Tokens](https://github.com/settings/tokens)
* [GitHub Search Syntax](https://docs.github.com/en/search-github/searching-on-github)
* [GitHub API Rate Limits](https://docs.github.com/en/rest/overview/resources-in-the-rest-api#rate-limiting)
* [GitHub Flavored Markdown](https://github.github.com/gfm/)

---

**Hinweis**: Diese Integration verwendet die GitHub REST API v3. Wir erwägen, GraphQL API v4-Unterstützung in Zukunft hinzuzufügen.
