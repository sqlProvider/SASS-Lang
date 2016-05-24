# 2. SASS Kullanımı

SASS bir kaç yol ile kullanılabilir ve CSS dosyaları üretmeye başlayabilir.
Biz bu dökümantasyon veya eğitim süreceinde **`NodeJS`** ve **`Gulp`** ile SASS kullanımını öğreneceğiz.

İlk olarak **NodeJS**'i bilgisayarınıza kurmalı ve **Gulp** paketini yüklemelisinz.

Kurulum ve kullanım talimatları;

 * Buradaki [adresten][nodejslink] NodeJs'in LTS(Stable) sürümünü indirip kurun.
 * Teminali/Komut satırını açın ve aşağıdaki komutu çalıştırın.
```bash
$ sudo npm i -g gulp
```

Bu aşamadan sonra proje gelişme sürecine başlanabilir.


> Buradaki [adresten](http://sass-lang.com/install) application veya command line arayüzlerini inceleyebilir ve diğer kullanım şekilleri hakkında bilgi alabilirsiniz.

Terminal veya komut satırı ile aranız iyi değilse aynı işi yapan arayüz programlarından birini kullanabilisiniz. Bunlardan birkaçı aşağıdan ulaşabilirsiniz.

 * [CodeKit][CodeKitLink] Ücretli | Mac
 * [CompassApp][CompassAppLink] Ücretli | Linux, Windows, Mac
 * [GhostLab][GhostlabLink] Ücretli | Windows, Mac
 * [Hammer][HammerLink] Ücretli | Mac
 * [Koala][KoalaLink] Ücretli | Linux, Windows, Mac
 * [LiveReload][LiveReloadLink] Ücretli | Windows, Mac
 * [Scout][ScoutLink] Ücretsiz | Windows, Mac

> **Not:** Bu dökümantasyonda baştan sona kadar **NodeJS** ve **Gulp** kullanılacaktır.


[CodeKitLink]: http://incident57.com/codekit/
[CompassAppLink]: http://compass.kkbox.comhttp://incident57.com/codekit/
[GhostlabLink]: http://www.vanamco.com/ghostlab/
[HammerLink]: http://hammerformac.com
[KoalaLink]: http://hammerformac.com
[LiveReloadLink]: http://livereload.com
[ScoutLink]: http://mhs.github.io/scout-app/

--

## 2.1 Npm Projesi Oluşturma

`Gulp` modülünü daha önce kurmuştuk. Şimdi Gulp'un yardımcı modüllerini kuracağız, sadece bize gereken modülleri. 

NPM projesi oluşturmak bizim modülleri yönetmemizi kolaylaştıracak ve bir sonraki projede de aynı konfigürasyonları kullanacaksak bir daha baştan uğraşmamıza gerek kalmayacak.

```bash
$ npm init
```
Bu komut şu şekilde bir çıktı verecektir ve burdaki satırları tek tek doldurmanız gerekir.

	This utility will walk you through creating a package.json file.
	It only covers the most common items, and tries to guess sane defaults.

	See **`npm help json`** for definitive documentation on these fields
	and exactly what they do.

	Use **`npm install <pkg> --save`** afterwards to install a package and
	save it as a dependency in the package.json file.

	Press ^C at any time to quit.
	name: (deneme) 
	version: (0.0.0) 1.0.0
	description: açıklama metni
	entry point: (index.js) 
	test command: 
	git repository: https://github.com/sqlProvider/SASS-Lang
	keywords: deneme, keywords
	author: Semih KEŞKEK
	license: (BSD-2-Clause)
	
 * **Name**: (deneme) kısmına projenizin adını küçük harflerle girmeniz gerekiyor. 
 * **Version**: projenizin versiyon numrasını tutar.
 * **Description**: Projenizin kısa açıklamasıdır.
 * **Entry Point**: Eğer NodeJS tabanlı bir proje ise projenizin başlangıç dosyasıdır.
 * **Git Repository**: Projenizin Git servisini kullanan herhangi bir sağlayıcıdaki repository URL'idir.
 * **Keywords**: Projenizin NPM gibi ortamlarda aratılırken üstte çıkmasını sağlayacak anahtar kelimelerdir.
 * **Author**: Projeyi yapan veya yapanların isimlerinin girildiği alandır.
 * **License**: Projenizi hangi lisansla lisanslamak istiyorsanız onun verisini girersiniz.

Eğer herhangi bir veriyi girerken boş bırakıp **`Enter`** tuşuna basarsanız **`()`** parantez içerisindeki veriyi girdiğinizi varsayacaktır.
> Not: 'deneme' ismini klasör isminden almıştır.  
	
Bu verileri girdikten sonra NPM bize bir özet sunar;

	About to write to /home/sqlprovider/Project/deneme/package.json:

	{
		"name": "deneme",
		"version": "1.0.0",
		"description": "açıklama metni",
		"main": "index.js",
		"scripts": {
			"test": "echo \"Error: no test specified\" && exit 1"
		},
		"repository": {
			"type": "git",
			"url": "https://github.com/sqlProvider/SASS-Lang"
		},
		"keywords": [
			"deneme",
			"keywords"
		],
		"author": "Semih KEŞKEK",
		"license": "BSD-2-Clause",
		"bugs": {
			"url": "https://github.com/sqlProvider/SASS-Lang/issues"
		}
	}

	Is this ok? (yes) 

**`Is this ok? (yes)`** satırını boş bırakıp veya **`yes`** yazıp **`Enter`** tuşuna bastıktan sonra **`package.json`** dosyamız oluşmuş olur.

Paket dosyası da oluşturduktan sonra artık Gulp'un yardımcı modüllerini kurmamız gerekiyor.

Terminal/Komut satırı üzerinden çalışacağınız klasöre gidin veya dosya yöneticisinden çalaşacağınız klasöre gidin 
Linux için; **`Right Click > Open In > Terminal`** 
Windows için; **`Shift + Right Click > Open Command Window Here`** kısayollarını kullanın ve aşağıdaki komutu çalıştırın.

```bash
$ npm i --save-dev gulp gulp-sass gulp-minify-css gulp-rename gulp-plumber gulp-notify
```
Buradaki satırları açıklayacak olursak;

| Komut           |   | Açıklama                                                                                                 |
|-----------------|---|----------------------------------------------------------------------------------------------------------|
| npm i           | : | Node Package Manager'e kendinden sonra gelen paketleri kurması gerektiğini söylüyor.                     |
| --save-dev      | : | Kurulacak olan paketlerin geliştirici bağımlılığı olduğunu belirtir. Uygulamaya etki etmez bu paketler.  |
| gulp            | : | Gulp modülünün proje içerisindeki paketi. Gulp'u çalıştırmak için gereklidir.                            |
| gulp-sass       | : | Gulp ile SASS derlemek için kullanılır.                                                                  |
| gulp-minify-css | : | Gulp ile CSS dosyasını sıkıştırmak için kullanılır.                                                      |
| gulp-rename     | : | Gulp ile dosya adı değiştirmek için kullanılır.                                                          |
| gulp-plumber    | : | Eğer yapılan işlem sırasında bir hata meydana gelirse plumber bu hatayı yakalar.                         |
| gulp-notify     | : | Gulp ile sistem bildirimi çıkarmak için kullanılır.                                                      |

Bu komutu çalıştırdıktan sonra bulunduğumuz klasörde **`node_modules`** adında bir klasör oluşur. Bütün paketlerimiz bu klasörün içine kurulmuştur.

-- 
 
## 2.2 Önbellekleme
	
SASS gelişmiş bir önbellekleme yapısı ile beraber gelir. Büyük projelerde payı aşırı derecede hissedilir.

SASS dosyaları derledikten sonra her dosyanın derlenmesini sırası ile birleştirir. 
Bu birleştirmeden önce her dosyadan gelen farklı sonuçları `.sass-cache` dosyasına yazar. 
Bunun yararı ise büyük dosyalar ile çalışırken değişiklik yapmadığımız halde dosyanın baştan derlenme sorununu ortadan kaldırmaktır.
NodeJS ile SASS derlerken varsayılan olarak `Caching` mekanizması kapalıdır. Ayarladan açmak gerekir. Buna daha sonra değineceğiz. 

--

## 2.3 Ek Seçenekler

SASS beraberinde onlarca ek seçenek ile beraber gelir. Bizim en çok işimize yaracak olanlara altta değineceğiz. 

##### :style

Derlemeden sonra CSS'in çıkış stilini ayarlar. CSS'i derleme sürecinde sıkıştırabilir, tek satır hale getirebilir veya açık bir şekilde bırakabiliriz.

##### :cache 

Derlerken her dosyanın ayrı ayrı derlenmiş halini tutar ve değişiklik yapılmamışsa derlemek ile bir daha uğraşmaz hazır olanı kullanır.

Diğer seçeneklere [buradaki][OptionsLink] bağlantıdan ulaşabilirsiniz.

--

## 2.4 Encoding

Türkçe karakter sorunu günümüzde baş belası bir sorun olurken SASS varsayılan olarak dosyaları `UTF-8` olarak derler. Türkçe karakterler olduğu gibi kalır ekstradan iş yükü harcatmaz.


--
| [![Back][back]](Syntax.md) | [![Next][next]](CSS.md) |
|-------|-----:|

[back]: https://raw.githubusercontent.com/sqlProvider/SASS-Lang/master/Resources/back.png
[next]: https://raw.githubusercontent.com/sqlProvider/SASS-Lang/master/Resources/next.png

[OptionsLink]:http://sass-lang.com/documentation/file.SASS_REFERENCE.html#options