title: Bloggen mit Spaßfaktor
date: 2015-02-14 22:33:20
tags:
- Hexo
- Blog

---

Ich bin von Haus aus ein neugieriger Mensch was technische Dinge angeht und probiere dementsprechend vieles aus. Dabei enstehen meist auch mehr oder weniger umfangreiche Notizen, die ich in meinem Desktop-Wiki ([Zim](http://zim-wiki.org/)) sammle. Allerdings muss ich immer wieder feststellen, dass ich meine eigenen Notizen nach einiger Zeit nicht mehr verstehe. Um meine persönliche Motivation für eine halbwegs nachvollziehbare Dokumentation etwas zu steigern, habe ich mir schon länger vorgenommen, einen Blog zu technischen Themen im Umfeld der Softwareentwicklung zu führen.

Heute möchte ich den Anfang machen und zeigen, welche Technik ich für meinen Blog ausgewählt habe. Meine wichtigsten Anforderungen an das Blog-System sind die folgenden:

- Open Source
- Automatisches Syntax-Highlighting für eingebetteten Beispiel-Code
- Spaßfaktor bei der Benutzung

<!-- more -->

# Wordpress als beliebte Lösung

Da ich mich bisher nicht mit der Technik von Blogs beschäftigt habe, war erstmal eine Recherche im Internet nötig. Dabei bin ich schnell auf [Wordpress](https://de.wordpress.org/) gestoßen, von dem ich schon öfter gehört habe. Wordpress ist Open Source und unter der GNU General Public License v2 lizenziert. Die Installation ist einfach und erlaubt einem, schnell mit dem Schreiben zu beginnen. Für die Darstellung der Inhalte gibt es viele kostenlose Themes, die direkt über das Wordpress-Backend installiert werden können.

So weit, so gut. Nachdem ich Wordpress lokal auf meinem Rechner installiert hatte, kamen die ersten Tests. Die Einbindung von Beispiel-Code funktioniert in der Basisinstallation noch nicht. Dafür gibt es Plugins, die ebenfalls direkt im Backend installiert werden können. Dementsprechend schnell bin ich auf [WP Code Highlight.js](https://wordpress.org/plugins/wp-code-highlightjs/) gestoßen, das in meinem ersten Test gute Arbeit in Sachen Syntax-Highlighting leistet. Ein erstes mögliches Blog-System habe ich für mich also gefunden.

# Spezialisierte Lösungen für Entwicklerblogs

Nach dem Test von Wordpress habe ich mich auf die Suche nach Systemen für Entwickler-Blogs gemacht, wobei ich auf den Artikel [10 Open Source Blogging Platforms for Developers](http://sixrevisions.com/tools/open-source-blogging-platforms-for-developers/) von Jacob Gube gestoßen bin. Die zentrale Erkenntnis für mich war, dass es im technischen Bereich durchaus spezialisierte Lösungen gibt, die teilweise auf Markup-Sprachen setzen und daraus statische Seiten erzeugen. Vorgestellt werden mehrere solcher Systeme, darunter auch [Hexo](http://hexo.io).

![](hexo.png)

Ein solches Konzept kannte ich bisher nicht, weshalb ich mir Hexo stellvertretend näher angesehen habe. Hexo basiert auf Node.js und bietet Kommandozeilenwerkzeuge zur Verwaltung des Blogs, z.B. für die Initialisierung des Blogs oder die Anlage eines neuen Blog-Posts. Alle Inhalte werden in Form von Textdateien im Markdown-Format verwaltet, weshalb auch die Einbindung und das Syntax-Highlighting von Beispielcode kein Problem sind. Die erstellten Seiten können während des Schreibens über einen Node.js-Server lokal angeschaut werden.

Das Konzept von Hexo, das übrigens als Open Source unter der MIT-Lizenz lizensiert ist, finde ich nach der ersten Betrachtung vielversprechend, weshalb Hexo vorerst das Blog-System meiner Wahl ist. Aus diesem Grund möchte ich nun noch etwas genauer auf die Benutzung von Hexo eingehen.

# Bloggen mit Hexo

An dieser Stelle möchte ich einen groben Überblick zur Arbeit mit Hexo liefern, wobei ich mich auf die Verwendung unter Ubuntu beziehe. Eine gute Anlaufstelle ist natürlich auch die [Dokumentation](http://hexo.io/docs/) zu Hexo.

## Setup

Zunächst müssen die Voraussetzungen für die Verwendung von Hexo geschaffen werden, weshalb als erstes [Node.js](http://nodejs.org/), der dazugehörige Package-Manager [npm](https://www.npmjs.com/) und das Versionskontrollsystem [Git](http://git-scm.com/) installiert werden.

``` bash
    sudo apt-get update
    sudo apt-get install nodejs
    sudo apt-get install npm
    sudo apt-get install git-core
```

Nachdem diese Voraussetzung geschaffen sind, kann Hexo per Package-Manager installiert werden.

``` bash
    sudo npm install -g hexo
```

Jetzt haben wir alles, was wir für den Anfang brauchen und können den Blog initialisieren und die benötigten Abhängigkeiten über den Package-Manager installieren lassen.

``` bash
    hexo init <verzeichnis>
    cd <verzeichnis>
    npm install
```

Als Ergebnis erhalten wir eine Verzeichnisstruktur, die bereits einen Eintrag als Beispiel enthält. Um diesen anzusehen wird nun der mitgelieferte Node.js-Server gestartet, der im Hintergrund läuft und die Inhalte aktualisiert sobald Dateien geändert, hinzugefügt oder gelöscht werden.

``` bash
    hexo server
```

Die erzeugten Seiten können nun im Browser unter der Adresse [http://localhost:4000](http://localhost:4000) betrachtet werden. Die mitgelieferte Beispiel-Seite gibt einen Überblick über die Verwendung von Hexo und sollte als Starthilfe ausreichen. Wie bereits erwähnt werden alle Inhalte im Markdown-Format hinterlegt, weshalb ein Blick auf die [Syntax](http://markdown.de/) nicht schadet.

![](hexo_init.png)

## Anpassung

Das mitgelieferte Theme ist nett anzusehen, kann aber auch ausgetauscht werden. Eine Auswahl solcher Themes ist auch im [Hexo-Wiki](https://github.com/hexojs/hexo/wiki/themes) zu finden. In meinem Fall fiel die Wahl auf das [hexo-theme-alex](https://github.com/ppoffice/hexo-theme-alex). Die Installation erfolgt durch das Klonen des Git-Repositories, wobei der folgende Befehl im Blog-Verzeichnis aufgerufen werden muss.

``` bash
    git clone git://github.com/ppoffice/alex-hexo-theme.git themes/alex
```

Anschließend muss das zu verwendene Theme noch in der Datei `_config.yml` eingetragen werden.

``` yaml
    theme: alex
```

Das Theme an sich kann natürlich an die eigenen Wünsche angepasst werden. Das bleibt aber jedem selbst überlassen. Was man aber definitiv nicht vergessen sollte, ist das Einfügen eines Impressums und einer Datenschutzerklärung. Sie werden nicht als Posts, sondern als Pages angelegt. Die Inhalte habe ich mir mit dem Impressum-Generator von [eRecht 24](http://www.e-recht24.de/) generieren lassen, nach `source/impressum/index.md` bzw. `source/datenschutz/index.md` kopiert und anschließend manuell nach Markdown überführt.

``` bash
    hexo new page "Impressum"
    hexo new page "Datenschutz"
```

Die erzeugten Seiten sollen im Menü auf allen Seiten auftauchen und müssen deshalb noch in der Konfiguration des Templates, hier in `themes/alex/_config.yml` eingetragen werden.

``` yaml
    menu:
        Blog: /
        Impressum: /impressum
        Datenschutz: /datenschutz
```

Da ich interessierten Lesern außerdem die Möglichkeit geben möchte, Kommentare zu hinterlassen, ist eine Registrierung bei [Disqus](https://disqus.com) notwendig. Hexo sieht diese Lösung bereits vor, so dass nur noch der Disqus-Shortname in `_config.xml` eingetragen werden muss.

## Generierung und Veröffentlichung

Den mitgelieferten Server verwende ich ausschließlich in der Entwurfsphase. Für die Bereitstellung im Internet lasse ich die Dateien generieren und übertrage sie anschließend manuell auf meinen Webspace. Hexo bietet auch für die Auslieferung einen Mechanismus, den ich derzeit nicht nutze. Informationen dazu sind in der Dokumenation zu Hexo im Abschnitt [Deployment](http://hexo.io/docs/deployment.html) zu finden.

Die generierten Seiten sind anschließend im Verzeichnis `public` zu finden. Die Anforderungen an das Webhosting sind übrigens sehr gering, weil die Inhalte nach der Generierung nur noch in Form statischer HTML-Seiten vorliegen. Dementsprechend werden weder PHP noch eine Datenbank benötigt.

``` bash
    hexo generate
```

Da ich die Sourcen zu meinem Blog mit Git versioniere, stelle ich das dazugehörige Repository auch auf Github unter dem Benutzername [Baitando](https://github.com/Baitando) im Repository [blog](https://github.com/Baitando/blog) zur Verfügung.

# Fazit und Ausblick

Mit Hexo bin ich auf ein spezialisiertes System für Entwickler-Blogs gestoßen, die in Kombination mit einer IDE für ein gewisses Entwickler-Flair beim Schreiben sorgt und damit - zumindest für mich - einen hohen Spaßfaktor bietet. Dementsprechend bin ich gespannt, ob sich mein erster, positiver Eindruck von Hexo bestätigt.

![](ide.png)

Wenn man das zu Grunde liegende Konzept weiter verfolgt, drängt sich natürlich die Anbindung an einen Continous-Integration-Server auf, der bei Änderungen im Git-Repository die Generierung anstößt und anschließend die Auslieferung auf den Webspace vornimmt. Ein interessanter Gedanke, dem ich demnächst eventuell etwas Zeit widme.
