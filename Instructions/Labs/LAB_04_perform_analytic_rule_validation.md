---
lab:
  title: 'Übung 04: Durchführen eines simulierten Angriffs'
  module: Guided Project - Perform a simulated attack to validate Analytic and Automation rules
---

>**Hinweis**: Dieses Lab baut auf Labs 01, 02 und 03 auf. Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/free/?azure-portal=true). In dem Sie über Administratorzugriff verfügen.

## Allgemeine Richtlinien zu 

- Verwenden Sie beim Erstellen von Objekten die Standardeinstellungen, es sei denn, es gibt Anforderungen, die unterschiedliche Konfigurationen erfordern.
- Erstellen, löschen oder bearbeiten Sie Objekte nur dann, wenn dies zum Erfüllen der Anforderungen dient. Unnötige Änderungen an der Umgebung können sich negativ auf Ihre Endbewertung auswirken.
- Wenn es mehrere Möglichkeiten gibt, ein Ziel zu erreichen, wählen Sie immer den Ansatz, der den geringsten Verwaltungsaufwand erfordert.

Wir müssen überprüfen, ob unsere Microsoft Sentinel-Bereitstellung Sicherheitsereignisse empfängt und Vorfälle von virtuellen Computern, auf denen Windows ausgeführt wird, erstellt.

## Architekturdiagramm

![Diagramm eines simulierten Angriffs ](../Media/apl-5001-lab-diagrams-lab04.png)

## Qualifikationsaufgabe

Sie müssen einen simulierten Angriff durchführen, um zu überprüfen, ob die Analyse- und Automatisierungsregeln einen Vorfall erstellen und ihn dem `Operator1` zuordnen. Sie führen einen einfachen `Privilege Escalation`-Angriff auf `vm1` durch.

## Übungsanweisungen

### Aufgabe 1: Durchführen eines simulierten Rechteausweitungsangriffs

Verwenden Sie simulierte Angriffe, um Analyseregeln in Microsoft Sentinel zu testen. Erfahren Sie mehr über die [Simulation eines Rechteausweitungsangriffs](https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1078.003/T1078.003.md).

1. Suchen und wählen Sie die virtuelle Maschine **vm1** in Azure aus und scrollen Sie die Menüpunkte nach unten zu **Operationen** und wählen Sie **Skriptausführung**.
1. Wählen Sie im Bereich **Skriptausführung** **RunPowerShellScript** aus.
1. Kopieren Sie die folgenden Befehle, um die Erstellung eines Adminstratorkontos zu simulieren, in das Formular `PowerShell Script` und klicken Sie auf **Ausführen**.

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

>**Hinweis**: Achten Sie darauf, dass Sie nur einen Befehl pro Zeile eingeben und dass Sie die Befehle durch Ändern des Benutzernamens erneut ausführen können.

1. Im Fenster `Output` sollten Sie dreimal `The command completed successfully` sehen.

### Aufgabe 2: Überprüfen eines Vorfalls anhand des simulierten Angriffs

Stellen Sie sicher, dass ein Vorfall erstellt wird, der Kriterien für die Analyseregel und Automatisierung entspricht. Erfahren Sie mehr über [Microsoft Sentinel Incident Management](https://learn.microsoft.com/azure/sentinel/incident-investigation).

1. Gehen Sie in `Microsoft Sentinel` zum Menüabschnitt `Threat management` und wählen Sie **Vorfälle**.
1. Es sollte ein Incident angezeigt werden, der mit `Severity` und `Title` übereinstimmt, die Sie in der von Ihnen erstellten Regel `NRT` konfiguriert haben.
1. Wählen Sie `Incident` aus, und der Bereich `detail` wird geöffnet.
1. Die Zuweisung `Owner` sollte **Operator1** sein, erstellt aus der `Automation rule`, und die `Tactics and techniques` sollte **Rechteausweitung** sein (aus der Regel `NRT`)
1. Wählen Sie **Vollständige Details anzeigen** aus, um alle `Incident management`-Funktionen und `Incident actions`
