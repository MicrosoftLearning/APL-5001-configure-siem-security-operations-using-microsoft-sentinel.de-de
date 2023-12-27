---
lab:
  title: 'Übung 04: Durchführen eines simulierten Angriffs'
  module: Guided Project - Perform a simulated attack to validate Analytic and Automation rules
---

>**Hinweis**: Dieses Labor baut auf Labs 01, 02 und 03 auf. Für diese Übung benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/free/?azure-portal=true). in dem Sie über Administratorzugriff verfügen.

## Allgemeine Richtlinien

- Verwenden Sie beim Erstellen von Objekten die Standardeinstellungen, es sei denn, es gibt Anforderungen, die unterschiedliche Konfigurationen erfordern.
- Erstellen, löschen oder ändern Sie nur Objekte, um die angegebenen Anforderungen zu erfüllen. Unnötige Änderungen an der Umgebung können sich negativ auf Ihre Endbewertung auswirken.
- Wenn es mehrere Ansätze zum Erreichen eines Ziels gibt, wählen Sie immer den Ansatz aus, der den geringsten Verwaltungsaufwand erfordert.

Jetzt müssen wir überprüfen, ob unsere Microsoft Sentinel-Bereitstellung Sicherheitsereignisse empfängt und Incidents zu virtuellen Computern erstellt, auf denen Windows ausgeführt wird.

## Architekturdiagramm

![Diagramm eines simulierten Angriffs ](../Media/apl-5001-lab-diagrams-lab04.png)

## Qualifikationsaufgabe

In dieser Übung erfahren Sie, wie Sie einen simulierten Angriff durchführen, um zu überprüfen, ob die Analyse- und Automatisierungsregeln einen Incident erstellen und dem `Operator1` zuweisen. Sie führen einen einfachen `Privilege Escalation` Angriff durch `vm1`.

## Übungsanweisungen

### Aufgabe 1 – Durchführen eines simulierten Berechtigungseskalationsangriffs

Verwenden Sie simulierte Angriffe, um Analyseregeln in Microsoft Sentinel zu testen. Erfahren Sie mehr über die Simulation von [Berechtigungseskalationsangriffen](https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1078.003/T1078.003.md).

1. Suchen sie den **virtuellen Computer vm1** in Azure, und scrollen Sie nach unten zu **"Vorgänge** ", und wählen Sie den **Befehl "Ausführen" aus.**
1. Wählen Sie im **Befehlsbereich** "Ausführen" die Option **"RunPowerShellScript" aus.**
1. Kopieren Sie die folgenden Befehle, um die Erstellung eines Administratorkontos im `PowerShell Script` Formular zu simulieren, und wählen Sie "Ausführen" aus **.**

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

>**Hinweis**: Stellen Sie sicher, dass pro Zeile nur ein Befehl vorhanden ist, und Sie können die Befehle erneut ausführen, indem Sie den Benutzernamen ändern.

1. `Output` Im Fenster sollte dreimal angezeigt werden `The command completed successfully`

### Aufgabe 2 – Überprüfen eines Vorfalls anhand des simulierten Angriffs

Stellen Sie sicher, dass ein Vorfall erstellt wird, der Kriterien für die Analyseregel und Automatisierung entspricht. Hier erfahren Sie mehr über die Incidentverwaltung in Microsoft Sentinel.

1. Wechseln `Microsoft Sentinel`Sie im `Threat management` Menüabschnitt zum Menüabschnitt, und wählen Sie **"Vorfälle" aus.**
1. Es sollte ein Vorfall angezeigt werden, der mit der `Severity` von Ihnen erstellten Regel übereinstimmt und `Title` Sie in der `NRT` von Ihnen erstellten Regel konfiguriert haben.
1. Wählen Sie den `Incident` Bereich aus, und der `detail` Bereich wird geöffnet.
1. Die `Owner` Zuordnung sollte "Operator1 **" sein**, erstellt aus dem `Automation rule`, und die `Tactics and techniques` sollte "Berechtigungseskalation **" (aus der `NRT` Regel) sein**.
1. Wählen Sie **"Vollständige Details** anzeigen" aus, um alle `Incident management` Funktionen anzuzeigen und `Incident actions`
