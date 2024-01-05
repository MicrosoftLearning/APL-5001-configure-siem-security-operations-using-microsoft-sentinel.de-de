---
lab:
  title: 'Übung 02: Erfassen von Daten zu sicherheitsrelevanten Ereignissen unter Windows'
  module: Guided Project - Deploy Microsoft Sentinel Content Hub solutions and data connectors
---

>**Hinweis**: Dieses Lab baut auf Lab 01 auf. Für diese Übung benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/free/?azure-portal=true). In dem Sie über Administratorzugriff verfügen.

## Allgemeine Richtlinien

- Verwenden Sie beim Erstellen von Objekten die Standardeinstellungen, es sei denn, es gibt Anforderungen, die unterschiedliche Konfigurationen erfordern.
- Erstellen, löschen oder ändern Sie nur Objekte, um die angegebenen Anforderungen zu erfüllen. Unnötige Änderungen an der Umgebung können sich negativ auf Ihre Endbewertung auswirken.
- Wenn es mehrere Möglichkeiten gibt, ein Ziel zu erreichen, wählen Sie immer den Ansatz, der den geringsten Verwaltungsaufwand erfordert.

Wir müssen Microsoft Sentinel so konfigurieren, dass Daten mithilfe von Microsoft Sentinel-Lösungen erfasst werden.

## Architekturdiagramm

![Diagramm von Content-Hub-Datenconnectors](../Media/apl-5001-lab-diagrams-lab02.png)

## Qualifikationsaufgabe

Sie müssen Content Hub-Lösungen im Microsoft Sentinel-Arbeitsbereich bereitstellen und die folgenden Anforderungen erfüllen:

- Installieren der folgenden Lösungen:
  - Windows-Sicherheitsereignisse.
  - Azure-Aktivitätsconnector.
  - Microsoft Defender für Cloud:
- Konfigurieren des Datenconnectors für Azure-Aktivität, um alle neuen und vorhandenen Ressourcen im Abonnement anzuwenden.
- Konfigurieren des Datenconnectors für Microsoft Defender for Cloud, um eine Verbindung mit dem Azure-Abonnement herzustellen und sicherzustellen, dass nur bidirektionale Synchronisierung aktiviert ist.
- Aktivieren einer Analyseregel basierend auf der Vorlage der verdächtigen Anzahl von Ressourcenerstellungs- oder -bereitstellungsaktivitäten. Die Regel sollte stündlich ausgeführt werden und nur die Daten der letzten Stunde abrufen.
- Sicherstellen, dass die Azure-Aktivitäts-Arbeitsmappe unter „Meine Arbeitsmappen“ verfügbar ist.

## Übungsanweisungen

>**Hinweis**: Um in den folgenden Aufgaben auf `Microsoft Sentinel` zuzugreifen, wählen Sie `workspace`, das Sie in Lab 01 erstellt haben.

### Aufgabe 1 – Bereitstellen einer Microsoft Sentinel Content Hub-Lösung

Stellen Sie eine Content Hub-Lösung bereit, und konfigurieren Sie Datenconnectors. Erfahren Sie mehr über [Content Hub-Lösungen](https://learn.microsoft.com/azure/sentinel/sentinel-solutions).

1. Gehen Sie in `Microsoft Sentinel` zum Menüabschnitt `Content management` und wählen Sie **Content Hub**.
1. Suchen Sie nach und wählen Sie **Windows-Sicherheitsereignisse**.
1. Wählen Sie den Link für **Details anzeigen**.
1. Wählen Sie den Plan „Windows-Sicherheitsereignisse“ und wählen Sie **Erstellen**.
1. Wählen Sie die `RG2`-Ressourcengruppe aus, die den Microsoft Sentinel-Arbeitsbereich enthält, und wählen Sie dann `Workspace`.
1. Wählen Sie **Weiter** auf der Datenconnectors-Registerkarte (die Lösung wird 2 Datenconnectors bereitstellen).
1. Wählen Sie **Weiter** auf der Arbeitsmappen-Registerkarte (die Lösung installiert Arbeitsmappen).
1. Wählen Sie **Weiter** auf der Analyse-Registerkarte (die Lösungen installieren Analyseregeln).
1. Wählen Sie **Weiter** auf der Registerkarte für Hunting-Abfragen (die Lösung installiert Hunting-Abfragen).
1. Klicken Sie auf **Überprüfen + erstellen**.
1. Klicken Sie auf **Erstellen**.

1. Wiederholen Sie diese Schritte für die Lösungen `Azure Activity` und `Microsoft Defender for Cloud`.

### Aufgabe 2: Einrichten des Datenconnectors für Azure-Aktivität

Konfigurieren des Datenconnectors für Azure-Aktivität, um alle neuen und vorhandenen Ressourcen im Abonnement anzuwenden. Erfahren Sie mehr über [Microsoft Sentinel-Datenconnectors](https://learn.microsoft.com/azure/sentinel/connect-data-sources).

  1. Gehen Sie in `Microsoft Sentinel` zum Menüabschnitt `Content management` und wählen Sie **Content Hub**.
  1. Filtern Sie im `Content hub` den `Status` nach installierten Lösungen.
  1. Wählen Sie die Lösung `Azure Activity` und wählen Sie **Verwalten**.
  1. Wählen Sie den `Azure Activity`-Datenconnector und wählen Sie **Connectorseite öffnen**.
  1. Scrollen Sie im Bereich `Configuration` unter der Registerkarte `Instructions` nach unten zu `2. Connect your subscriptions...` und wählen Sie **Assistent für die Zuweisung von Azure-Richtlinien starten>**.
  1. Wählen Sie auf der Registerkarte **Grundlagen** die Schaltfläche  Auslassungspunkte(...) unter **Bereich** und wählen Sie Ihr Abonnement aus der Dropdown-Liste aus und klicken Sie auf **Auswählen**.
  1. Wählen Sie die Registerkarte **Parameter** und wählen Sie Ihren Arbeitsbereich aus der Dropdown-Liste **Log Analytics-Arbeitsbereich**.
  1. Wählen Sie die Registerkarte **Wartung** aus, und aktivieren Sie dann das Kontrollkästchen **Korrekturtask erstellen**.
  1. Wählen Sie die Schaltfläche **Überprüfen + erstellen** aus, um die Konfiguration zu überprüfen.
  1. Wählen Sie **Erstellen** aus, um den Vorgang abzuschließen.
  
### Aufgabe 3 – Einrichten des Defender for Cloud-Datenconnectors

Konfigurieren Sie den Datenconnector für Microsoft Defender for Cloud, und stellen Sie sicher, dass nur das Incident Management konfiguriert ist.

  1. Gehen Sie in `Microsoft Sentinel` zum Menüabschnitt `Content management` und wählen Sie **Content Hub**.
  1. Filtern Sie im `Content hub` den `Status` nach installierten Lösungen.
  1. Wählen Sie die Lösung `Microsoft Defender for Cloud` und wählen Sie **Verwalten** aus.
  1. Wählen Sie den `Subscription-based Microsoft Defender for Cloud (Legacy)`-Datenconnector und wählen Sie **Connectorseite öffnen**.
  1. Scrollen Sie im Bereich `Configuration` unter der Registerkarte `Instructions` nach unten zu Ihrem Abonnement und bewegen Sie den Schieberegler in der Spalte `Status` auf **Verbunden**.
  1. Stellen Sie sicher, dass `Bi-directional sync` **aktiviert** ist.

### Aufgabe 4: Erstellen einer Analyseregel

Erstellen Sie eine Analyseregel basierend auf der Vorlage der verdächtigen Anzahl von Ressourcenerstellungs- oder -bereitstellungsaktivitäten. Die Regel sollte stündlich ausgeführt werden und nur die Daten der letzten Stunde abrufen. Erfahren Sie mehr über die [Verwendung von Microsoft Sentinel-Analyseregelvorlagen](https://learn.microsoft.com/azure/sentinel/detect-threats-built-in).

  1. Gehen Sie in `Microsoft Sentinel` zum Menüabschnitt `Configuration` und wählen Sie **Analyse**.
  1. Suchen Sie auf der Registerkarte `Rule templates` nach **Verdächtige Anzahl von Ressourcenerstellungs- oder -bereitstellungsaktivitäten**.
  1. Wählen Sie die **Verdächtige Anzahl von Ressourcenerstellungs- oder -bereitstellungsaktivitäten**, und wählen Sie **Regel erstellen**.
  1. Lassen Sie die Standardeinstellungen auf der Registerkarte `General` und wählen Sie **Weiter: Regellogik festlegen >**.
  1. Belassen Sie die Voreinstellung `Rule query` und konfigurieren Sie `Query scheduling` anhand der Tabelle:

     |Einstellung |Wert|
     |---|---|
     |Abfrage ausführen alle|Stündlich|
     |Datensuche für letzte:|Stündlich|

  1. Wählen Sie **Weiter: Vorfallseinstellungen >**.
  1. Belassen Sie die Standardeinstellungen und wählen Sie **Weiter: Automatisierte Antwort >**.
  1. Belassen Sie die Standardeinstellungen und wählen Sie **Weiter: Überprüfen und erstellen >**.
  1. Wählen Sie **Speichern**.

### Aufgabe 5: Sicherstellen, dass die Azure-Aktivitäts-Arbeitsmappe unter „Meine Arbeitsmappen“ verfügbar ist

  1. Gehen Sie in `Microsoft Sentinel` zum Menüabschnitt `Content management` und wählen Sie **Content Hub**.
  1. Filtern Sie im `Content hub` den `Status` nach installierten Lösungen.
  1. Wählen Sie die Lösung `Azure Activity` und wählen Sie **Verwalten**.
  1. Wählen Sie die `Azure Activity`-Arbeitsmappe `checkbox` und wählen Sie dann **Konfiguration**.
  1. Wählen Sie die `Azure Activity`-Arbeitsmappe und wählen Sie **Speichern**.
  1. Wählen Sie `Azure Region` für Ihren `Microsoft Sentinel`-Arbeitsbereich.  
