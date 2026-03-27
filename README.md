<h1>FritzingCheckPart.py – Deutsche Anleitung</h1>

<h2>Beschreibung</h2>
<p><code>FritzingCheckPart.py</code> ist ein Python-Skript zur Überprüfung von Bauteildateien für das EDA-Programm Fritzing.</p>

<p>Ursprünglich wurde es entwickelt, um Probleme mit SVG-Dateien aus Inkscape zu beheben. Inzwischen prüft es:</p>
<ul>
  <li>.fzp-Dateien (Bauteildefinition)</li>
  <li>.svg-Dateien (Grafiken)</li>
  <li>Struktur eines Fritzing-Parts</li>
</ul>

<p>Zusätzlich kann es:</p>
<ul>
  <li>XML „pretty printen“</li>
  <li>CSS-Styles in Inline-Attribute umwandeln</li>
  <li>SVG-Dateien Fritzing-kompatibel machen</li>
</ul>

<p>Ein separates Skript <code>PP.py</code> dient nur zur XML-Formatierung.</p>

<hr>

<h2>Voraussetzungen</h2>
<ul>
  <li>Python 3</li>
  <li>lxml (<code>pip install lxml</code>)</li>
</ul>

<hr>

<h2>Installation</h2>

<h3>Linux / Ubuntu</h3>
<pre><code>sudo cp FritzingCheckPart.py /usr/local/bin
sudo cp FritzingTools.py /usr/local/bin
sudo cp PP.py /usr/local/bin
sudo cp PPTools.py /usr/local/bin

chmod ugo+x /usr/local/bin/*.py
</code></pre>

<h3>Windows (Cygwin empfohlen)</h3>
<p>Pakete installieren:</p>
<ul>
  <li>python3</li>
  <li>python3-lxml</li>
</ul>

<pre><code>cp *.py /usr/local/bin
chmod ugo+x /usr/local/bin/*.py
</code></pre>

<hr>

<h2>Nutzung</h2>

<h3>1. Verzeichnis → Verzeichnis</h3>
<pre><code>FritzingCheckPart.py src_dir dst_dir
</code></pre>
<ul>
  <li>verarbeitet alle Parts</li>
  <li><code>dst_dir</code> muss leer sein</li>
</ul>

<h3>2. Einzelnes Part prüfen</h3>
<pre><code>FritzingCheckPart.py part.fzp
</code></pre>
<ul>
  <li>erstellt .bak Backup</li>
  <li>korrigiert .fzp und SVGs</li>
</ul>

<h3>3. User-Parts prüfen</h3>
<pre><code>FritzingCheckPart.py parts/user/filename.fzp
</code></pre>

<h3>4. Nur SVG prüfen</h3>
<pre><code>FritzingCheckPart.py file.svg
</code></pre>

<p>Funktionen:</p>
<ul>
  <li>CSS → Inline-Attribute</li>
  <li>entfernt <code>px</code> bei Schriftgrößen</li>
  <li>korrigiert Silkscreen-Farbe</li>
  <li>erkennt fehlerhafte Pads</li>
  <li>behebt Gerber-Probleme</li>
</ul>

<p><strong>Wichtig nach jeder Inkscape-Bearbeitung!</strong></p>

<hr>

<h2>Pretty Print (XML formatieren)</h2>
<pre><code>PP.py file.svg
</code></pre>
<ul>
  <li>formatiert XML</li>
  <li>erstellt .bak Datei</li>
</ul>

<hr>

<h2>Konfiguration</h2>

<h3>PPTools.py</h3>
<pre><code>DetailPP = 'y'
</code></pre>
<p><code>'n'</code> → weniger aggressives Formatting</p>

<h3>FritzingTools.py</h3>
<pre><code>ModifyTerminal = 'n'
</code></pre>
<ul>
  <li><code>'y'</code> → setzt 0-Größe von Pins auf 10</li>
  <li>Achtung: Position muss danach geprüft werden</li>
</ul>

<h3>FritzingCheckPart.py</h3>
<pre><code>IssueNameDupWarning = 'y'
</code></pre>
<p><code>'n'</code> → weniger Warnungen</p>

<pre><code>Debug = 0
</code></pre>
<ul>
  <li>1–3 → Debug-Ausgaben</li>
</ul>

<hr>

<h2>Wichtige Hinweise</h2>

<h3>Nach Inkscape-Bearbeitung</h3>
<pre><code>FritzingCheckPart.py file.svg
</code></pre>

<p>Grund:</p>
<ul>
  <li>Inkscape nutzt CSS → Fritzing ist nicht vollständig kompatibel</li>
</ul>

<h3>Backups</h3>
<ul>
  <li>Originaldateien → .bak</li>
  <li><strong>Achtung:</strong> werden beim erneuten Ausführen überschrieben</li>
</ul>

<hr>

<h2>Typische Fehler</h2>

<h3>XML-Fehler</h3>
<ul>
  <li>fehlende Leerzeichen</li>
  <li>doppelte Attribute</li>
</ul>

<h3>Connector-Probleme</h3>
<ul>
  <li>fehlen in SVG</li>
  <li>falsche Reihenfolge</li>
  <li>doppelte IDs</li>
</ul>

<h3>SVG-Probleme</h3>
<ul>
  <li><code>style</code> statt Attribute</li>
  <li>Maße in <code>px</code></li>
  <li>falsche Layer-Struktur</li>
  <li>Ellipsen statt Kreise</li>
</ul>

<hr>

<h2>Warnungen</h2>
<ul>
  <li>falsche Fonts (nur Droid Sans oder OCRA empfohlen)</li>
  <li>fehlende Views</li>
  <li>doppelte Namen</li>
  <li>Maße in <code>px</code></li>
</ul>

<hr>

<h2>Automatische Änderungen</h2>
<ul>
  <li><code>style="..."</code> → Inline-Attribute</li>
  <li><code>font-size="3.5px"</code> → <code>3.5</code></li>
  <li>Silkscreen-Farbe wird korrigiert</li>
  <li>Terminalgrößen werden angepasst (optional)</li>
</ul>

<hr>

<h2>Fazit</h2>
<p>Sehr hilfreiches Tool für:</p>
<ul>
  <li>saubere Fritzing-Parts</li>
  <li>Fehleranalyse</li>
  <li>Inkscape-Kompatibilität</li>
  <li>korrekte Gerber-Erstellung</li>
</ul>

<p><strong>Empfehlung: Immer vor dem Export ausführen</strong></p>
