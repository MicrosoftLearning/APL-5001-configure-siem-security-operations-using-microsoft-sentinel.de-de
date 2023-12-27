---
lab:
  title: 'Übung 02: Aufnehmen Windows-Sicherheit Ereignisdaten'
  module: Guided Project - Deploy Microsoft Sentinel Content Hub solutions and data connectors
---

>**Hinweis**: Dieses Lab baut auf Lab 01 auf. Für diese Übung benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/free/?azure-portal=true). in dem Sie über Administratorzugriff verfügen.

## Allgemeine Richtlinien

- Verwenden Sie beim Erstellen von Objekten die Standardeinstellungen, es sei denn, es gibt Anforderungen, die unterschiedliche Konfigurationen erfordern.
- Erstellen, löschen oder ändern Sie nur Objekte, um die angegebenen Anforderungen zu erfüllen. Unnötige Änderungen an der Umgebung können sich negativ auf Ihre Endbewertung auswirken.
- Wenn es mehrere Ansätze zum Erreichen eines Ziels gibt, wählen Sie immer den Ansatz aus, der den geringsten Verwaltungsaufwand erfordert.

Wir müssen Microsoft Sentinel so konfigurieren, dass Daten mithilfe von Microsoft Sentinel-Lösungen aufgenommen werden.

## Architekturdiagramm

![Diagramm von Inhaltshub-Datenconnectors](../Media/apl-5001-lab-diagrams-lab02.png)

## Qualifikationsaufgabe

Sie müssen Content Hub-Lösungen im Microsoft Sentinel-Arbeitsbereich bereitstellen und die folgenden Anforderungen erfüllen:

- Installieren Sie folgende Software:
  - Windows-Sicherheitsereignisse
  - Azure-Aktivitätsconnector
  - Microsoft Defender für Cloud:
- Konfigurieren Sie den Datenconnector für Azure Activity, um alle neuen und vorhandenen Ressourcen im Abonnement anzuwenden.
- Konfigurieren Sie den Datenconnector für Microsoft Defender für Cloud, um eine Verbindung mit dem Azure-Abonnement herzustellen und sicherzustellen, dass nur bidirektionale Synchronisierung aktiviert ist.
- Aktivieren Sie eine Analyseregel basierend auf der Vorlage "Verdächtige Anzahl von Ressourcenerstellungs- oder Bereitstellungsaktivitäten". Die Regel sollte jede Stunde und nur Nachschlagedaten für diese letzte Stunde ausgeführt werden.
- Stellen Sie sicher, dass die Azure-Aktivitätsarbeitsmappe in "Meine Arbeitsmappen" verfügbar ist.

## Übungsanweisungen

>**Hinweis**: Wählen Sie in den folgenden Aufgaben für den Zugriff `Microsoft Sentinel`die `workspace` in Lab 01 erstellte Datei aus.

### Bereitstellen einer Microsoft Sentinel-Inhaltshublösung

Stellen Sie eine Content Hub-Lösung bereit, und konfigurieren Sie Datenconnectors. Erfahren Sie mehr über [Content Hub-Lösungen](https://learn.microsoft.com/azure/sentinel/sentinel-solutions).

1. Wechseln `Microsoft Sentinel`Sie in , `Content management` wechseln Sie zum Menüabschnitt, und wählen Sie "Inhaltshub" aus **.**
1. Suchen und auswählen Windows-Sicherheit **Ereignisse**
1. Wählen Sie den Link für **"Details anzeigen" aus.**
1. Wählen Sie Windows-Sicherheit Ereignisplan und dann "Erstellen" aus **.**
1. Wählen Sie die `RG2` Ressourcengruppe aus, die den Microsoft Sentinel-Arbeitsbereich enthält, und wählen Sie dann die Option aus `Workspace`.
1. Wählen Sie auf der Registerkarte "Daten Verbinden ors" die Option **"Weiter**" aus (Lösung stellt 2 Datenconnectors bereit)
1. Wählen Sie auf der Registerkarte "Arbeitsmappen" die Option **"Weiter** " aus (Projektmappe installiert Arbeitsmappen)
1. Wählen Sie auf der Registerkarte "Analyse" die Option **"Weiter** " aus (Lösungen installieren Analyseregeln)
1. Wählen Sie **auf der Registerkarte "Suchabfragen" die Option "Weiter** " aus (Lösungssucheabfragen)
1. Klicken Sie auf **Überprüfen + erstellen**.
1. Klicken Sie auf **Erstellen**.

1. Wiederholen Sie diese Schritte für die `Azure Activity` und die `Microsoft Defender for Cloud` Lösungen.

### Aufgabe 2 – Einrichten des Datenconnectors für Azure Activity

Konfigurieren Sie den Datenconnector für Azure Activity, um alle neuen und vorhandenen Ressourcen im Abonnement anzuwenden. Erfahren Sie mehr über Microsoft Sentinel-Datenconnectortypen.

  1. Wechseln Sie in `Microsoft Sentinel`, `Content management` wechseln Sie zum Menüabschnitt, und wählen Sie "Inhaltshub **" aus**.
  1. Filtern `Status` Sie im `Content hub`Filter nach installierten Lösungen.
  1. Wählen Sie die `Azure Activity` Lösung und dann "Verwalten"** aus**.
  1. Wählen Sie den Connector und dann die Seite `Azure Activity`Connector öffnen aus.
  1. Scrollen Sie auf der Registerkarte `Configuration`Anweisungen`Instructions` nach unten, und wählen Sie `2. Connect your subscriptions...`Azure Policy Zuweisungs-Assistent starten aus.
  1. Wählen Sie auf der Registerkarte **Grundlagen** unter **Bereich** die Schaltfläche mit den Auslassungspunkten (…) aus, und wählen Sie in der Dropdownliste Ihr "Azure-Abonnement"aus, und klicken Sie anschließend auf **Auswählen**.
  1. Wählen Sie auf der Registerkarte Parameter Ihren Workspace uniquenameDefender aus der Dropdownliste Primärer Log Analytics-Arbeitsbereich aus.
  1. Wählen Sie die Registerkarte **Wartung** aus, und aktivieren Sie dann das Kontrollkästchen **Korrekturtask erstellen**.
  1. Wählen Sie die Schaltfläche **Überprüfen + erstellen** aus, um die Konfiguration zu überprüfen.
  1. Wählen Sie **Erstellen** aus, um den Vorgang abzuschließen.
  
### Aufgabe 3 – Einrichten des Für Defender für Cloud-Datenconnectors

Konfigurieren Sie den Datenconnector für Microsoft Defender für Cloud, und stellen Sie sicher, dass nur die Vorfallverwaltung konfiguriert ist.

  1. Wechseln Sie in `Microsoft Sentinel`, `Content management` wechseln Sie zum Menüabschnitt, und wählen Sie "Inhaltshub **" aus**.
  1. Filtern `Status` Sie im `Content hub`Filter nach installierten Lösungen.
  1. Wählen Sie die `Microsoft Defender for Cloud` Lösung und dann "Verwalten"** aus**.
  1. Wählen Sie den Connector und dann die Seite `Subscription-based Microsoft Defender for Cloud (Legacy)`Connector öffnen aus.
  1. `Configuration` Scrollen Sie im Bereich unter der `Instructions` Registerkarte nach unten zu Ihrem Abonnement, und verschieben Sie den Schieberegler in der `Status` Spalte auf **Verbinden.**
  1. Stellen Sie sicher, dass sie aktiviert ist.

### Aufgabe 4: Erstellen einer Analyseregel

Erstellen Sie eine Analyseregel basierend auf der Vorlage "Verdächtige Anzahl von Ressourcenerstellungs- oder Bereitstellungsaktivitäten". Die Regel sollte jede Stunde und nur Nachschlagedaten für diese letzte Stunde ausgeführt werden. Erfahren Sie mehr über die [Verwendung von Microsoft Sentinel Analytic-Regelvorlagen](https://learn.microsoft.com/azure/sentinel/detect-threats-built-in).

  1. Wechseln Sie in `Microsoft Sentinel`, `Configuration` wechseln Sie zum Menüabschnitt, und wählen Sie "Analyse"** aus**.
  1. Suchen Sie auf der `Rule templates` Registerkarte nach **verdächtiger Anzahl von Ressourcenerstellungs- oder Bereitstellungsaktivitäten**.
  1. Wählen Sie die **Verdächtige Anzahl von Ressourcenerstellungs- oder Bereitstellungsaktivitäten** aus, und wählen Sie "Regel** erstellen" aus**.
  1. Behalten Sie die Standardeinstellungen auf der `General` Registerkarte bei, und wählen Sie "Weiter" aus **: Regellogik >** festlegen.
  1. Behalten Sie die Standardeinstellung `Rule query` bei, und konfigurieren Sie `Query scheduling` die Tabelle:

     |Einstellung |Wert|
     |---|---|
     |Abfrage ausführen alle|Stündlich|
     |Datensuche für letzte:|Stündlich|

  1. Wählen Sie **Weiter: Incident-Einstellungen** aus.
  1. Behalten Sie die Standardwerte bei, und wählen Sie **"Weiter: Automatisierte Antwort >**" aus.
  1. Übernehmen Sie die übrigen Standardeinstellungen, und wählen Sie **Überprüfen + erstellen** aus.
  1. Wählen Sie **Speichern**.

### Aufgabe 5 – Stellen Sie sicher, dass die Azure-Aktivitätsarbeitsmappe in "Meine Arbeitsmappen" verfügbar ist

  1. Wechseln Sie in `Microsoft Sentinel`, `Content management` wechseln Sie zum Menüabschnitt, und wählen Sie "Inhaltshub **" aus**.
  1. Filtern `Status` Sie im `Content hub`Filter nach installierten Lösungen.
  1. Wählen Sie die `Azure Activity` Lösung und dann "Verwalten"** aus**.
  1. Wählen Sie `Azure Activity`Arbeitsmappen`checkbox` und dann **Konfiguration überprüfen** aus.
  1. Wählen Sie die `Azure Activity` Arbeitsmappe und dann "Speichern" aus****.
  1. Wählen Sie den `Azure Region` Arbeitsbereich aus `Microsoft Sentinel` .  
