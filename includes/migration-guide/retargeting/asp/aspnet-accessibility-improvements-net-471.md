### <a name="aspnet-accessibility-improvements-in-net-471"></a>ASP.NET Eingabehilfen-Verbesserungen in .NET 4.7.1

|   |   |
|---|---|
|Details|Ab .NET Framework 4.7.1, verbessert ASP.NET wie ASP.NET Web Controls mit Eingabehilfen-Technologie in Visual Studio für eine bessere Unterstützung für ASP.NET Kunden arbeiten.  Dazu gehören die folgenden Änderungen:<ul><li>Änderungen an der fehlenden UI Eingabehilfen Muster in Steuerelementen zu implementieren, wie das Dialogfeld Feld hinzufügen, in der Detailansicht-Assistent oder das Dialogfeld "ListView konfigurieren" im ListView-Assistenten.</li><li>Änderungen zur Verbesserung der Anzeige im Modus für hohe Kontraste, wie Felder Editors für den Pager.</li><li>Änderungen zur Verbesserung der Tastaturnavigation erfährt für Steuerelemente, z. B. um das Dialogfeld Felder im Assistenten bearbeiten Pagerfelder DataPager-Steuerelement, das Dialogfeld "ObjectContext konfigurieren" oder das Dialogfeld "Konfigurieren von Data-Auswahl" des Assistenten zum Konfigurieren von Datenquellen.</li></ul>|
|Vorschlag|<strong>Wie Sie diese Änderungen Einverständnis im</strong>damit für den Visual Studio-Designer diese Änderungen profitieren können, muss es auf .NET Framework 4.7.1 ausgeführt oder höher. Diese Änderungen in einer der folgenden Methoden kann die Webanwendung profitieren:<ul><li>Installieren Visual Studio 2017 15.3 oder später, die die neuen Funktionen für Barrierefreiheit mit dem folgenden AppContext Switch standardmäßig unterstützt werden.</li><li>Die ältere Eingabehilfen Verhalten abwählen, durch Hinzufügen der <code>Switch.UseLegacyAccessibilityFeatures</code> AppContext zu wechseln der <code>&lt;runtime&gt;</code> im Abschnitt der Datei "devenv.exe.config" und Festlegen des Werts auf <code>false</code>, wie das folgende Beispiel zeigt.</li></ul><pre><code class="language-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;...&#13;&#10;&lt;!-- AppContextSwitchOverrides value attribute is in the form of &#39;key1=true/false;key2=true/false&#39;  --&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;...;Switch.UseLegacyAccessibilityFeatures=false&quot; /&gt;&#13;&#10;...&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>Anwendungen, die das .NET 4.7.1 Framework oder höher und die Vorgängerversion beibehalten möchten Eingabehilfen Verhalten können Sie dies für die Verwendung von älteren Barrierefreiheitsfunktionen durch explizites Festlegen dieser Option AppContext auf <code>true</code>.|
|Bereich|Gering|
|Version|4.7.1|
|Typ|Neuzuweisung|
