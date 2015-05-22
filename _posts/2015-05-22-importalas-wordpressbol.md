---
layout: post
title: "Importálás Wordpressből"
date: 2015-05-22 19:58:30
tags: jekyll wordpress import
---
Megpróbáltam a `jekyll-import` segítségével behúzni a Wordpress blogom 
tartalmát, de felemás sikereket értem csak el sajnos.

Szerencsére a dokumentáció elég jó. 
Ugyan a `jekyll-import` függőségeihez keresgélnem kellett egy keveset, végül rájöttem, hogy mi 
kell. Az független, self-hosting Wordpress oldalakra vonatkozó 
[kódrészletet](http://import.jekyllrb.com/docs/wordpress/) végül sajnos nem tudtam 
felhasználni, mert a szolgáltató nem tette lehetővé a kívülről történő hozzáférést arra 
hivatkozva, hogy az nem biztonságos. Ja, vagy inkább azért, mert másra is lehet használni egy 
adatbázist, mint pár gagyi szkript mellé adattárolásra és nehogy aztán már mást is 
lehessen, ha fizetünk érte.
Szerencsére a Wordpress.com blogszolgáltató export XML-je is 
használható egy másik importer osztállyal. Márpedig XML-be én is tudok exportot készíteni a 
saját blogomról. Reméltem, hogy ez működni fog.

{% highlight ruby %}
ruby -rubygems -e 'require "jekyll-import";
    JekyllImport::Importers::WordpressDotCom.run({
      "source" => "/home/zsolti/zsoltiblog.wordpress.2015-05-22.xml",
      "no_fetch_images" => false,
      "assets_folder" => "assets"
    })'
{% endhighlight %}

Működött is, csak nem lett tökéletes az eredmény. Nem tudta átmásolni az összes képet bizonyos
Unicode karakterek miatt. Ugyan az adatbázis karakterkódolása `utf8` (és nem `latin1_swedish`) néha 
baja volt az *ő* és *ű* betűkkel. Többek közt. Végül is megjelenítette a képeket a Wordpress
blogon, de egyszer írtam egy plugint, amit miután ráeresztettem a Wordpress bejegyzésekre, lerendezte
azokat, amikben az említett képek szerpenek. Szerencsére volt mentésem.

Ami ennél is jobban zavart, az az, hogy a bejegyzésekhez tartozó meta-adatokat hülyén dolgozta fel. 
Mondjuk lehet, hogy én vagyok a hülye és lehet állítani Jekyllben, hogy a „front matter” ne csak
szabványos YAML legyen. Mindenesetre amit beszúrt az importer, az nem volt szabványos.

Úgyhogy ebből egyelőre nem lett semmi. A képekhez csak az eredeti linkeket szúrta be. Szóval ez
eddig nem nyert. Szerintem marad a Jekyll játékszernek. Meglátjuk.

Na, most legenerálom életem első általam Markdownban írt Jekyll blogbejegyzését és meglátjuk, hogy
hogyan eszi meg a Markdownt, ami nekem még új.

