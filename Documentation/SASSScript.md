# 5. SASS Script

CSS'in basit syntax'ına eklemeler yapılarak geliştirilmiştir.
SASS Script te değişken kullanabilir, aritmetik işlemler yapabilir, döngüler oluşturabilir, karar yapılarını ve ekstra fonksiyonları kullanabilirsiniz.
SASS Script ayrıca kural ve özellik isimleri oluşturmada da kullanılabilir. 

---
## 5.1 Değişkenler: $

Programlama dillerinde yer alan değişkenler bir programın neredeyse herşeyidir. 
Orjinal CSS'de değişkenler bulunmamakta ancak SASS Script ile birlikte değişkenlerin kullanımı da dile adapte edildi.
Değişknleri **`$`** karakteri ile kullanabiliyoruz. 
SASS Script te değişken tanımlamak klasik bir CSS özelliği tanımlamaya benzer.

```sass
	$width: 5em;
```
Tanımladığımız değişkenleri nerede istersek kullanabiliriz.
```sass
	#main{
		width: $width;
	}
```
---

Değişkenler sadece tanımlandığı seviyede ve alt seviyelerde kullanılabilir haldedir. 
Eğer en dış seviyede bir değişken tanımlarsanız bütün seviyelerde kullanabilirsiniz. 
Ayrıca değiken tanımınızın sonunda **`!global`** anahtar kelimesini kullanırsanız değişkenin üst seviyelerdeki değerini değiştirebilir veya 
iç seviyelerde tanımladığınız değişkeni diğer seviyelerde de kullanabilirsiniz.

```sass
	#main{
		$width: 5em !global;
		width: $width;
	}
	#sidebar{
		width: 5em;
	}
```
Yukarıdaki kodun çıktısına bakacak olursak;

```css
	#main{
		width: 5em;
	}
	#sidebar{
		width: 5em;
	}
```
Eğer `!global` anahtar kelimesini kullanmasaydık Gulp bize şöyle bir hata dönecekti;

```sass
	[10:43:42] gulp-notify: [SCSS Error] resources/sass/style.scss
	Error: Undefined variable: "$width".
			on line 12 of resources/sass/style.scss
	>> 	width: $width
	--------^
```
Yukarıda görüldüğü gibi `$width` değişkeni bulunamıyor. Örnekte `#main` altında tanımlanan `$width` `#sidebar` altında kullanılmaya çalışıyor.
Değişkenler lokal olarak çalıştığı için böyle bir kullanıma izin verilmiyor. Eğer bu şekilde kullanılmak istenirse `!global` anahtar kelimesinin **kesinlikle** kullanılması gerekiyor.

> Not: Diğer programlama dillerinde olduğu gibi SASS'da da değişken tanımlama kuralları vardır. SASS'da değişken tanımlamaları kural tanımlama ile aynıdır.
 * Bütün değişkenler `$` ile başlar.
 * Değişkenler de `$`dan sonraki karakter sayı olamaz.
 * `$, !, ?` gibi özel karakterler kullanılamaz.
 * Diğer dillerden farklı olarak `-` kullanılabilirdir.
 
---

## 5.2 Veri Tipleri

SASS Script 7 ana değişken tipini destekler;
 * Numbers (1, 2, 3, 4.5, 10px, 10em)
 * Strings ("falan", 'filan', folon)
 * Colors (blue, rgb(0, 0, 255), #00F, rgba(0,0,0,.4))
 * Booleans (true, false)
 * Nulls (null)
 * Lists (1.5em 1em 0 2em veya 1.5em, 1em, 0, 2em)
 * Maps ($harita: (anahtar1: deger1, anahtar2: deger2))
 
SASS Script ayrıca CSS özelliklerinde kullanılan bütün değerlere destek verir, 
bu değerlerin Unicode sınırları içerisinde olması gerekir ve **`!important`** anahtar kelimesi kullanılmalıdır.

---
### 5.2.1 Numbers

Sayı değişken tipleri bütün sayısal verileri tutabilir bunlara `10px, 100%` gibi içerisinde string barındıran ifadelerde dahildir.
```sass
	$width: 100px;
	$height: $width / 2;
	p{
		height: $height;
	}
``` 
Normal bir programlama dilinde hata verecek veya `NAN (Not a Numarable)` olarak geri dönüş yapacak olan bu kullanım SASS Script için oldukça normaldir.
Kodun çıktısını inceleyecek olursak;
```css
	p{
		height: 50px;
	}
```
Sadece `px` değil `%, em, vm` gibi bütün sayısal verileri tutabilirler.

---
### 5.2.2 Strings

Stringler içerisine her türden veriyi alabilen değişkenlerdir. 
Diğer programlama dillerinde çift tırnak `"` veya tek tırnak `'` içerisinde yazılan stringler 
SASS Script te istenilirse tırnak kullanılmadan yazılabilir.
Tabiki tırnak kullanılarak da yazılabilir. Tamamen isteğe kalmış bir durumdur.
```sass
	$pBeforeContent: 'Değer';
	p:before{
		content: $pBeforeContent;
	}
```
Çıktı şu şekilde olacaktır.
```css
	p:before {
  		content: "Değer"; 
  	}
```

---
### 5.2.3 Colors

Renk değişken tipleri CSS içerisinde kullanabildiğimiz bütün renk tanımlamalarını tutabilir.
Bu renkleri toplayabilir, çıkartabilir, çarpabilir ve bölebilir. 
Bu işlemleri renk tanımını sayısal veriye döndürerek yapar, 
örneğin hexadecimal bir renk ile rgb bir rengi birbiri ile toplyabilirsiniz.

```sass
	$color1: white;
	$color2: #456;
	$color3: rgb(213,131,123);
	$color4: rgba(12,143,65, .4);
	// ....
	
	p{
		color: $color1 - $color3;
	}
```
Kodun çıktısı şu şekildedir;
```css
	p {
  		color: #2a7c84; 
	}
```

---
### 5.2.4 Booleans

Mantıksal değişkenlerdir. Sadece `true` ve `false` değerlerini alabilirler. Karar yapıları konusunda bu veri tipleri üzerinde durulacaktır.
Tek başlarına bir anlam ifade etmezler.

---
### 5.2.5 Nulls

Nulls veri tipleri değişkenlerin içlerinin boş olduğunu gösterir. 
Bir değişkene `null` değeri atanırsa değişken tamamen boş olmuş olur hiçbir değeri yoktur.

---
### 5.2.6 Lists

Liste veri tipleri içlerinde belirli bir sıra gelen değerleri tutarlar. 
Klasik programlamada ki `diziler`in kasrşılığıdır.
Bu değerler iki şekilde tutulur;
 * Değerlerin `boşluk` karakteri ile ayrılması
 * Değerlerin `,` karakteri ile ayrılması

```sass
	$list: (10px) (20px) (30px) (40px);
	p{
		margin: $list;
	}
	
	$list2: 'Arial', Tahoma;
	span{
		font-family: $list2;
	}
```
Kodun derlendikten sonraki hali aşağıdaki gibi olacaktır;
```css
	p {
  		margin: 10px 20px 30px 40px; 
	}
	span {
		font-family: "Arial", Tahoma; 
	}
```
Listeler ilk bakışta yararsız gibi görükse de **`@each`** ile birlikte kullanırken yararlı hale gelirler. 


---
### 5.2.7 Maps

Map veri tipleri diğer programlama dillerindeki objelere benzerler.
Her değerin bir anahtarı vardır. Teoride İç içe sınırsız sayıda map açılabilir. 
Ancak unutulmamalıdır ki seviye sayısı ne kadar artarsa performans ve kullanım o kadar azalacaktır.

```sass
	$map: (
		key1: 200px,
		key2: (
			key21: 500px,
			key22: 100px
			key23: (
				key231: '3. seviyedeyiz',
				key232: 'daha da devam edebilriz'
			)
		)
	);
	
	p{
		width: map-get($map, key1);
		
		$seviye2: map-get($map, key2);
		height: map-get($seviye2, key21);
		line-height: map-get($seviye2, key22);
		
		$seviye3: map-get($seviye2, key23);
		&:after{
			content: map-get($seviye3, key321);
		}
		&:before{
			content: map-get($seviye3, key322);
		}
	}
```
Yukarıdaki map örneğinde özelliklerimizin değerlerini bir map'de tuttuk. Kodun çıktısı şu şekilde olacaktır.

```css
	.p {
		width: 200px;
		height: 500px;
		line-height: 100px; 
	}
	.p .after {
		content: "3. seviyedeyiz"; 
	}
	.p .before {
		content: "daha da devam edebilriz"; 
	}
```