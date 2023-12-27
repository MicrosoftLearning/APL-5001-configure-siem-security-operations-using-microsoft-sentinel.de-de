---
lab:
  title: "Aufgabe\_1: Bereitstellen von Microsoft Sentinel"
  module: Guided Project - Create and configure a Microsoft Sentinel workspace
---

>Für diese Übung benötigen Sie ein Azure-Abonnement. in dem Sie über Administratorzugriff verfügen.

## Allgemeine Richtlinien

- Verwenden Sie beim Erstellen von Objekten die Standardeinstellungen, es sei denn, es gibt Anforderungen, die unterschiedliche Konfigurationen erfordern.
- Erstellen, löschen oder ändern Sie nur Objekte, um die angegebenen Anforderungen zu erfüllen. Unnötige Änderungen an der Umgebung können sich negativ auf Ihre Endbewertung auswirken.
- Wenn es mehrere Ansätze zum Erreichen eines Ziels gibt, wählen Sie immer den Ansatz aus, der den geringsten Verwaltungsaufwand erfordert.

Wir bewerten derzeit den bestehenden Sicherheitsstatus unserer Unternehmensumgebung. Das Unternehmen benötigt Ihre Hilfe beim Einrichten einer SIEM-Lösung (Security Information & Event Management), um zukünftige Cyberangriffe zu identifizieren.

## Architekturdiagramm

![Diagramm mit Log Analytics-Arbeitsbereich.](../Media/apl-5001-lab-diagrams-01.png)

## Qualifikationsaufgabe

Sie planen, Microsoft Sentinel einzusetzen. Die Lösung muss die folgenden Anforderungen erfüllen:

- Dieses Dataset wird in der Azure-Region „USA, Westen“ gespeichert.
- Stellen Sie sicher, dass alle Sentinel-Analyseprotokolle 180 Tage lang aufbewahrt werden.
- Weisen Sie Operator1 Rollen zu, um sicherzustellen, dass Operator1 Vorfälle verwalten und Sentinel-Playbooks ausführen kann. Bei der Lösung muss nach dem Prinzip der geringsten Rechte verfahren werden.

## Übungsanweisungen

### Aufgabe 1: Erstellen eines Log Analytics-Arbeitsbereichs

Erstellen Sie einen Log Analytics-Arbeitsbereich, einschließlich der Regionsoption. Weitere Informationen zu [Rollen in Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/quickstart-onboard).

  1. Suchen Sie im Azure-Portal nach Datenträgern, und wählen Sie sie aus.
  1. Wählen Sie **+ Erstellen** aus.
  1. Klicken Sie auf **Create a new workspace** (Neuen Arbeitsbereich erstellen).
  1. Wählen Sie die Ressourcengruppe `RG2` aus.
  1. Geben Sie einen Namen für den neuen Log Analytics-Arbeitsbereich ein.
  1. Wählen Sie die Region für den Arbeitsbereich aus.
  1. Wählen Sie zum Erstellen des Arbeitsbereichs **Überprüfen und erstellen** aus.
  1. Wählen Sie **Erstellen** aus, um den Arbeitsbereich für die Bereitstellung zu erstellen.

### Aufgabe 2 – Bereitstellen von Microsoft Sentinel in einem Arbeitsbereich

Hinzufügen von Microsoft Sentinel zum Arbeitsbereich

  1. Wenn die `workspace` Bereitstellung abgeschlossen ist, wählen Sie **"Aktualisieren"** aus, um das neue `workspace`anzuzeigen.
  1. Wählen Sie die Option aus, zu der `workspace` Sentinel hinzugefügt werden soll (in Aufgabe 1 erstellt).
  1. Klicken Sie auf **Hinzufügen**.

### Aufgabe 3 – Zuweisen einer Microsoft Sentinel-Rolle zu einem Benutzer

Weisen Sie einer Verwendung eine Microsoft Sentinel-Rolle zu. Rollen und Berechtigungen für die Arbeit in Microsoft Sentinel

  1. Wechseln Sie zur Ressourcengruppe.
  1. Wählen Sie die Option **Zugriffssteuerung (IAM)** aus.
  1. Wählen Sie  aus, und fügen Sie  hinzu.
  1. `Microsoft Sentinel Contributor` in der Suchleiste eingeben und das Suchsymbol auswählen.
  1. Wählen Sie **Weiter** aus.
  1. Wählen Sie die `User, group, or service principal`-Option aus.
  1. Wählen Sie **+ Mitglieder auswählen** aus.
  1. Suchen Sie nach den `Operator1` zugewiesenen Anweisungen in Ihrer Übungseinheit `(operator1-XXXXXXXXX@LODSPRODMCA.onmicrosoft.com)`.
  1. Wählen Sie `user icon` aus.
  1. Wählen Sie **Auswählen**.
  1. Wählen Sie „Überprüfen und zuweisen“ aus.
  1. Wählen Sie „Überprüfen und zuweisen“ aus.

### Konfigurieren der Datenaufbewahrung

Konfigurieren der Datenaufbewahrung [Erfahren Sie mehr über die Datenaufbewahrung](https://learn.microsoft.com/azure/azure-monitor/logs/data-retention-archive).

  1. Wechseln Sie zu dem `Log Analytics workspace` in Schritt 1 Schritt 5 erstellten Vorgang.
  1. Wählen Sie **Nutzungs- und geschätzte Kosten** aus.
  1. Wählen Sie **Aufbewahrung** aus.
  1. Ändern Sie den Datenaufbewahrungszeitraum auf **180 Tage**.
  1. Klickan Sie auf **OK**.

>**Hinweis**: Für weitere Übungsbeispiele führen Sie das [Modul "Erstellen und Verwalten von Microsoft Sentinel-Arbeitsbereichen" aus](https://learn.microsoft.com/training/modules/create-manage-azure-sentinel-workspaces/) .
