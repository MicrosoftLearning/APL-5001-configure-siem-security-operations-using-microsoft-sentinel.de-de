---
lab:
  title: 'Übung 03: Überprüfen der Sentinel-Bereitstellung'
  module: 'Guided Project - Configure Microsoft Sentinel Data Collection rules, NRT Analytic rule and Automation'
---

>**Hinweis**: Dieses Lab baut auf Lab 01 und Lab 02 auf. Für diese Übung benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/free/?azure-portal=true). In dem Sie über Administratorzugriff verfügen.

## Allgemeine Richtlinien

- Verwenden Sie beim Erstellen von Objekten die Standardeinstellungen, es sei denn, es gibt Anforderungen, die unterschiedliche Konfigurationen erfordern.
- Erstellen, löschen oder ändern Sie nur Objekte, um die angegebenen Anforderungen zu erfüllen. Unnötige Änderungen an der Umgebung können sich negativ auf Ihre Endbewertung auswirken.
- Wenn es mehrere Möglichkeiten gibt, ein Ziel zu erreichen, wählen Sie immer den Ansatz, der den geringsten Verwaltungsaufwand erfordert.

Wir müssen Microsoft Sentinel so konfigurieren, dass Sicherheitsereignisse von virtuellen Computern empfangen werden, auf denen Windows ausgeführt wird.

## Architekturdiagramm

![Diagramm der Windows-Sicherheitsereignisse über AMA mithilfe von DCR.](../Media/apl-5001-lab-diagrams-lab03.png)

## Qualifikationsaufgabe

Sie müssen die Microsoft Sentinel-Bereitstellung überprüfen, um die folgenden Anforderungen zu erfüllen:

- Konfigurieren Sie die Windows-Sicherheit Ereignisse über den AMA-Connector, um alle Sicherheitsereignisse nur von einem virtuellen Computer namens VM1 zu erfassen.
- Erstellen Sie eine NRT-Abfrageregel (Near-Real-Time), um einen Vorfall basierend auf der folgenden Abfrage zu generieren.

```KQL
SecurityEvent 
| where EventID == 4732
| where TargetAccount == "Builtin\\Administrators"
```

- Erstellen Sie eine Automatisierungsregel, die Operator1 die Besitzerrolle für Vorfälle zuweist, die von der NRT-Regel generiert werden.

## Übungsanweisungen

>**Hinweis**: Um in den folgenden Aufgaben auf `Microsoft Sentinel` zuzugreifen, wählen Sie `workspace`, das Sie in Lab 01 erstellt haben.

### Aufgabe 1: Konfigurieren von Datensammlungsregeln (DCRs) in Microsoft Sentinel

Konfigurieren Sie ein Windows-Sicherheitsereigniss über den AMA-Connector. Erfahren Sie mehr über [Windows-Sicherheitsereignisse über AMA-Connector](https://learn.microsoft.com/azure/sentinel/data-connectors/windows-security-events-via-ama).

 1. Navigieren Sie in `Microsoft Sentinel` zum Menüabschnitt `Configuration` und wählen Sie **Datenconnectors**.
 1. Suchen Sie nach und wählen Sie **Windows-Sicherheitsereignisse über AMA**.
 1. Wählen Sie **Connectorseite öffnen**.
 1. Wählen Sie im Bereich `Configuration` **+ Datensammlungsregeln erstellen**
 1. Auf der Registerkarte `Basics` geben Sie `Rule Name` ein.
 1. Erweitern Sie auf der Registerkarte `Resources` Ihr Abonnement und die Ressourcengruppe `RG1` in der Spalte `Scope`.
 1. Wählen Sie `VM1`, und wählen Sie dann **Weiter: Sammeln >** aus.
 1. Auf der Registerkarte `Collect` lassen Sie den Standardwert `All Security Events` stehen.
 1. Wählen Sie **Weiter: Überprüfen + Erstellen >**, dann **Erstellen** aus.

### Aufgabe 2 – Erstellen einer in Quasi-Echtzeit-Abfrageerkennung (NRT)

Erkennen Sie Bedrohungen mit Analyseregeln in Quasi-Echtzeit (NRT) in Microsoft Sentinel. Hier erfahren Sie mehr über [NRT-Analyseregeln in Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/near-real-time-rules).

 1. Navigieren Sie in `Microsoft Sentinel` zum Menüabschnitt `Configuration` und wählen Sie **Analyse** aus.
 1. Wählen Sie **+ Erstellen**, und **NRT-Abfrageregel (Vorschau)** aus.
 1. Geben Sie einen `Name` für die Regel ein, und wählen Sie **Rechteausweitung** aus `Tactics and techniques`.
 1. Wählen Sie **Weiter: Regellogik festlegen >**.
 1. Geben Sie die KQL-Abfrage in das Formular `Rule query` ein.

    ```KQL
    SecurityEvent 
    | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    ```

 1. Wählen Sie **Weiter: Vorfallseinstellungen >**, und wählen Sie **Weiter: Automatisierte Antwort >** aus.
 1. Klicken Sie auf **Weiter: Überprüfen und erstellen**.
 1. Wenn die Überprüfung abgeschlossen ist, wählen Sie **Speichern**.

### Aufgabe 3 – Konfigurieren der Automatisierung in Microsoft Sentinel 

Konfigurieren der Automatisierung in Microsoft Sentinel. Erfahren Sie mehr über [Erstellen und Verwenden von Microsoft Sentinel-Automatisierungsregeln](https://learn.microsoft.com/azure/sentinel/create-manage-use-automation-rules).

 1. Navigieren Sie in `Microsoft Sentinel` zum Menüabschnitt `Configuration` und wählen Sie **Automatisierung** aus.
 1. Wählen Sie **+ Erstellen**, und die Automatisierungsregel aus.
 1. Geben Sie eine `Automation rule name` ein, und wählen Sie **Besitzer zuweisen** aus `Actions`.
 1. Weisen Sie **Operator1** als Besitzer zu.
 1. Wählen Sie **Übernehmen** aus.
