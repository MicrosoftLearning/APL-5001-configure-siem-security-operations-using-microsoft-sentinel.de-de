---
lab:
  title: 'Übung 03: Überprüfen der Sentinel-Bereitstellung'
  module: 'Guided Project - Configure Microsoft Sentinel Data Collection rules, NRT Analytic rule and Automation'
---

>**Hinweis**: Dieses Lab baut auf Lab 01 und Lab 02 auf. Für diese Übung benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/free/?azure-portal=true). in dem Sie über Administratorzugriff verfügen.

## Allgemeine Richtlinien

- Verwenden Sie beim Erstellen von Objekten die Standardeinstellungen, es sei denn, es gibt Anforderungen, die unterschiedliche Konfigurationen erfordern.
- Erstellen, löschen oder ändern Sie nur Objekte, um die angegebenen Anforderungen zu erfüllen. Unnötige Änderungen an der Umgebung können sich negativ auf Ihre Endbewertung auswirken.
- Wenn es mehrere Ansätze zum Erreichen eines Ziels gibt, wählen Sie immer den Ansatz aus, der den geringsten Verwaltungsaufwand erfordert.

Wir müssen Microsoft Sentinel so konfigurieren, dass Sicherheitsereignisse von virtuellen Computern empfangen werden, auf denen Windows ausgeführt wird.

## Architekturdiagramm

![Diagramm der Windows-Sicherheit Ereignisse über AMA mit DCR](../Media/apl-5001-lab-diagrams-lab03.png)

## Qualifikationsaufgabe

Sie müssen die Microsoft Sentinel-Bereitstellung überprüfen, um die folgenden Anforderungen zu erfüllen:

- Konfigurieren Sie die Windows-Sicherheit Ereignisse über den AMA-Connector, um alle Sicherheitsereignisse nur von einem virtuellen Computer namens VM1 zu erfassen.
- Erstellen Sie eine NrT-Abfrageregel (Near-Real-Time), um einen Vorfall basierend auf der folgenden Abfrage zu generieren.

```KQL
SecurityEvent 
| where EventID == 4732
| where TargetAccount == "Builtin\\Administrators"
```

- Erstellen Sie eine Automatisierungsregel, die Operator1 der Rolle "Besitzer" für Vorfälle zuweist, die von der NRT-Regel generiert werden.

## Übungsanweisungen

>**Hinweis**: Wählen Sie in den folgenden Aufgaben für den Zugriff `Microsoft Sentinel`die `workspace` in Lab 01 erstellte Datei aus.

### Aufgabe 1: Konfigurieren von Datensammlungsregeln (DCRs) in Microsoft Sentinel

Windows-Sicherheitsereignisse über AMA Connector Windows-Sicherheitsereignisse über AMA Connector

 1. `Microsoft Sentinel`Wechseln Sie im `Configuration` Menüabschnitt zum Menüabschnitt, und wählen Sie "Datenconnectors" aus **.**
 1. Suchen und auswählen Windows-Sicherheit **Ereignisse über AMA**
 1. Wählen Sie **Connectorseite öffnen** aus.
 1. Wählen Sie im Bereich Konfiguration die Option Datensammlungsregel erstellen aus.
 1. Auf der Registerkarte `Basics`Allgemein`Rule Name`: 
 1. Erweitern Sie auf der `Resources` Registerkarte Ihr Abonnement und die `RG1` Ressourcengruppe in der `Scope` Spalte.
 1. Wählen Sie Weiter und anschließend Verbinden aus.
 1. Lassen Sie auf der `Collect` Registerkarte die Standardeinstellung von `All Security Events`
 1. Wählen Sie **Weiter: Überprüfen** und dann **Erstellen** aus.

### Aufgabe 2 – Erstellen einer Fast-Echtzeit-Abfrageerkennung (NRT)

Schnelle Erkennung von Bedrohungen mit NRT-Analyseregeln (Near-Real-Time, Quasi-Echtzeit) in Microsoft Sentinel Hier erfahren Sie mehr über [Analyseregeln nahezu in Echtzeit (NRT) in Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/near-real-time-rules).

 1. `Microsoft Sentinel`Wechseln Sie in , `Configuration` wechseln Sie zum Menüabschnitt, und wählen Sie "Analyse" aus **.**
 1. Auswählen **+ Erstellen** und **NRT-Abfrageregel (Vorschau)**
 1. Geben Sie eine `Name` für die Regel ein, und wählen Sie **"Berechtigungseskalation** " aus `Tactics and techniques`.
 1. Klicken Sie auf **Weiter: Regellogik festlegen**.
 1. Geben Sie die KQL-Abfrage in das Formular ein.`Rule query`

    ```KQL
    SecurityEvent 
    | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    ```

 1. Wählen Sie **"Weiter" aus: Einstellungen für Vorfälle >**, und wählen Sie **"Weiter: Automatisierte Reaktion >**
 1. Klicken Sie auf **Weiter: Überprüfen und erstellen**.
 1. Wählen Sie nach Abschluss der Validierung die Option **Erstellen** aus.

### Konfigurieren der Automatisierung in Microsoft Sentinel 

Konfigurieren der Automatisierung in Microsoft Sentinel Erfahren Sie mehr über das [Erstellen und Verwenden von Microsoft Sentinel-Automatisierungsregeln](https://learn.microsoft.com/azure/sentinel/create-manage-use-automation-rules).

 1. Wechseln `Microsoft Sentinel`Sie im Menüabschnitt zum `Configuration` Menüabschnitt, und wählen Sie "Automatisierung" aus **.**
 1. Wählen Sie **Automatisierungsregel erstellen** aus.
 1. Geben Sie einen `Automation rule name`Namen ein, und wählen Sie " **Besitzer** zuweisen" aus. `Actions`
 1. Weisen Sie **Operator1** als Besitzer zu.
 1. Wählen Sie **Übernehmen** aus.
