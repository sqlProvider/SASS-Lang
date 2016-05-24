# SASS (Syntactically Awesome StyleSheets)

## Nedir?

Sass CSS'in bir uzantısıdır. CSS dilini güçlü ve zarif şekilde yazmka için tasarlanmıştır. [Değişkenleri](#), [iç içe kuralları](#), [fonksiyonları](#), [satır içi importları](#) ve daha fazlasını
CSS uyumlu bir sözdizimi ile kullanmanızı sağlar. 
SASS büyük CSS sayfalarınızı organize eder ve kısa bir sürede hazır hale getirir.


## İçindekiler

* [**Syntax**](../master/Documentation/Syntax.md)
* [**SASS Kullanımı**](../master/Documentation/UsingSASS.md)
	1. [NPM Projesi Oluşturma](../master/Documentation/UsingSASS.md#21-npm-projesi-oluşturma)
	2. [Önbellekleme](../master/Documentation/UsingSASS.md#22-Önbellekleme)
	3. [Ek Seçenekler](../master/Documentation/UsingSASS.md#23-ek-seçenekler)
	4. [Encoding](../master/Documentation/UsingSASS.md#24-encoding)
* [**CSS**](../master/Documentation/CSS.md)
	1. [İç İçe Kurallar](../master/Documentation/CSS.md#31-İç-İçe-kurallar)
	2. [Evebeyn Refesansı: &](../master/Documentation/CSS.md#32-evebeyn-referansı-)
	3. [İç İçe Özellikler](../master/Documentation/CSS.md#33-İç-İçe-Özellikler)
* [**Yorum Satırları**](../master/Documentation/CommentLines.md)
* [**SASS Script**](../master/Documentation/SASSScript.md)
	1. [Değişkenler: $](../master/Documentation/SASSScript.md#51-değişkenler-)
	2. [Veri Tipleri](../master/Documentation/SASSScript.md#52-veri-tipleri)
		1. [Numbers](../master/Documentation/SASSScript.md#521-numbers)
		2. [Strings](../master/Documentation/SASSScript.md#522-strings)
		3. [Colors](../master/Documentation/SASSScript.md#523-colors)
		4. [Booleans](../master/Documentation/SASSScript.md#524-booleans)
		5. [Nulls](../master/Documentation/SASSScript.md#525-nulls)
		6. [Lists](../master/Documentation/SASSScript.md#526-lists)
		7. [Maps](../master/Documentation/SASSScript.md#527-maps)
	3. Operatörler
		1. Sayı Operatörleri
			1. Çarpma ve Bölme
			2. Toplama ve Çıkarma
		2. Renk Operatörleri
		3. String Operatörler
		4. Bolean Operatörler
		5. Liste Operatörleri
	4. Parantezler
	5. Fonksiyonlar
		1. Parametre Kullanma
	6. İnterpolasyon
	7. SassScript'te & Kullanımı
	8. Default Değişkenler
* **Kurallar**
	1. @import
		1. Kısmı
		2. İç İçe @import
	2. @media
	3. @extend
		1. Nasıl Çalışır
		2. Seçicileri Genişletmek
		3. Multi Genişletme
		4. Zincirleme Genişletme
		5. Seçici Dizileri
			1. Seçici Dizileri Birleştirme
		6. @extend-Only Seçiciler
		7. !optional Seçeneği
		8. Direktif İçinde Genişletme
	4. @at-root
		1. @at-root (without | with)
	5. @debug
	6. @warn
	7. @error
* **Karar Yapıları**
	1. if ()
	2. @if
	3. @for
	4. @each
		1. Çoklu Atama
	5. @while
* **Mixinler**
	1. Tanımlama
	2. Dahil Etme
	3. Parametre Kullanımı
		1. Kelime Parametleri
		2. Değişken Parametleri
	4. İçerik @mixin'leri oluşturma
* **Fonksiyonlar**
* **Derleme Şekli**
	1. İç İçe
	2. Açık
	3. Normal
	4. Sıkıştırılmış