# 5. SASS Script

CSS'in basit syntax'ına eklemeler yapılarak geliştirilmiştir.
**`SASS Script`** te değişken kullanabilir, aritmetik işlemler yapabilir, döngüler oluşturabilir, karar yapılarını ve ekstra fonksiyonları kullanabilirsiniz.
SASS Script ayrıca kural ve özellik isimleri oluşturmada da kullanılabilir. 

---
## 5.1 Değişkenler: $

Programlama dillerinde yer alan değişkenler bir programın neredeyse herşeyidir. 
Orjinal CSS'de değişkenler bulunmamakta ancak SASS Script ile değişkenler de kullanılabilir hale geliyor.
Değişkenleri **`$`** karakteri ile kullanabiliyoruz. 
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
--

Değişkenler sadece tanımlandığı seviyede ve alt seviyelerde kullanılabilir haldedir. 
Eğer en dış seviyede bir değişken tanımlarsanız bütün seviyelerde kullanabilirsiniz. 
Ayrıca değişken tanımınızın sonunda **`!global`** anahtar kelimesini kullanırsanız değişkenin üst seviyelerdeki değerini değiştirebilir veya 
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
>Sadece `px` değil `%, em, vm` gibi bütün sayısal verileri tutabilirler.

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

---
## 5.3 Operatörler

Bütün veri tipleri eşitllik operatörünü (**`== ve !=`**) destekler, ayrıca her tipin kendine has operatörleri vardır.

---
### 5.3.1 Number

SASS Script çarpma `*`, bölme `/`, toplama `+`, çıkarma `-`, mod alma `%` gibi aritmatik işlemleri yapabilir. 
Diğer programlama dillerinin aksine SASS Script'te sayıları sadece sayı olarak tutmak zorunda kalmıyoruz. 
Sayılar `px, em, %, ...` türlerinde olarabilir ve SASS Script birbirine dönüşebilir cinsler arasında aritmetik işlemler yapabilir. 

Sayı değişkenleri ayrıca mantıksal operatörlerden büyüktür, küçüktür, büyük eşit ve küçük eşit (**``<, >, <=, >=``**) operatörlerini destekler.

---
#### 5.3.1.1 Çarpma ve Bölme

CSS syntax'ında `/` operatörü özelliklerde kullanılmakta ayrıca SASS Script'te de bu operatör bölme işlemini yapmakta.
Bu yüzden bölme işleminde kısıtlamalar bulunmakta bazı durumdalar CSS syntax'ı devreye girerken bazı durumlar SASS Script bölme işlemini yapmakta.
SASS Script'in devreye 3 durum vardır bunlar;
 * Eğer değer bir değişkendeyse veya bir fonskiyon tarafından döndürülüyorsa
 * Eğer ifade parantez içine yazılmışsa
 * Eğer ifade de bölme işlemi dışında başka bir işlem daha yer alıyorsa
Örnek olarak inceleyecek olursak
```sass
	p{
		font: 10px/8px; // Bölme işlemi yapılmaz
		$width: 1000px; 
		width: $width/2; // Bölme işlemi yapılır
		width: round(1.5px)/2; // Bölme işlemi yapılır
		height: (500px/2); // Bölme işlemi yapılır
		margin-left: 5px + 8px/2px; // Bölme işlemi yapılır
		font: (italic bold 10px/8px) // Değer liste tipinde olduğu için bölme işlemi sayılmaz
	}
```
Yukarıdaki kodun CSS çıktısı aşağıdaki giib olur
```css
	p{
		font: 10px/8px;
		width: 500px;
		width: 1px;
		height: 250px;
		margin-left: 9px;
	}
```
--

Eğer değişkenleri bölme yapmadan ama `/` işaretini kullanarak yazırmak istiyorsanız **`#{}`** ifadesini kullanmanız gerekir.
```sass
	p{
		$font-size: 12px;
		$line-height: 30px;
		font: #{$font-size}/#{$line-height};
	}
```
Yukarıdaki kod derlendiğinde aşağıdaki çıktıyı verir.  
```css
	p{
		font: 12px/30px;
	}
```
> `#{}` ifadesi diğer programlama dillerindeki `toString()` fonksiyonuna karşılık gelir. 
> İfadeyi detaylı öğrenmek için [5.6 İnterpolasyon](#56-İnterpolasyon) bölümüne bakabilirsiniz.

---
#### 5.3.1.2 Toplama ve Çıkarma

Diğer bir karışıklıpa sebep olan operatör olan çıkarma `-` operatörünün bir kaç durumu vardır. 
Bazı durumlarda CSS'in `-` si geçerli olurken bazı durumlarda SASS Script çıkarma işlemini yapar.
Bu durumları inceleyecek olursak;
 * Eğer sabit değerler ile çıkarma işlemi yapılıyorsa (10px ve 8px'i ele alalım)
  * 10px-8px ve 10px - 8px ifadesi 2px döndürür.
  * 10px- 8px ve 10px -8px ifadesi olduğu gibi döner işlem yapılmaz.
 * Eğer bir sabit bir değişken ile işlem yapıyorsak ($size: 10px ve 8px'i ele alalım)
  * $size-8px ve $size- 8px ifadesi değişken bulunamadı hatası verecektir. Değişken tanımlama kurallarına göz atın.
  * $size -8px ifadesi 10px -8px olarak döner.
  * 8px- $size ifadesi 8px- 10px olarak döner.
  * 8px -$size ifadesi 2px döndürür.
  * $size - 8px ifadesi 2px döndürür.
  * 8px - $size ifadesi 2px döndürür.
 * Eğer iki değişken ile çalışıyorsak ($size1: 10px ve $size2: 8px)
  * $size1-$size2, $size- $size2, $size2- $size1 ifadeleri değişken bulunamadı hatası verecektir.
  * $size1 - $size2, $size1 -$size2 ve $size2 -$size1 ifadeleri düzgün bir şekilde işlemi yapar.
  * Diğer durumların hepsi değerleri işlem yapmadan ekrana yazdıracaktır.

---
### 5.3.1 Color

Bütün aritmatik işlemler renk değerlerini destekler. 
Bunun anlamı kırmızı ve maviyi toplayabileceğiniz(karıştırmak), çıkartabileceğiniz ve diğer işlemleri yapabileceğinizdir.
Örneğin;
```scss
	p{
		color: #010203 + #040506;
	}
```
yukarıdaki örnek şu şekilde hesaplanır: (01 + 04) (02 + 05) (03 + 06) = `#050709`
```css
	p{
		color: #050709;
	}
```

Bu işlemler genellikle [renk fonksiyonları](#) için kullanılır.
Aritmatik işlemler ayrıca renk ve sayı içinde kullanılabilirdir.
```scss
	p{
		color: #010203 * 2;
	}
```
yukarıdaki işlem şu şekilde hesaplanacaktır. (01 * 2) (02 * 2) (03 * 2) ve kodun çıktısı aşağıdaki gibi olacaktır.
```css
	p{
		color: #020406;
	}
```


---
| [![Back][back]](CommentLines.md) | [![Next][next]](SASSScript.md) |
|-------|-----:|

[back]: https://raw.githubusercontent.com/sqlProvider/SASS-Lang/master/Resources/back.png
[next]: https://raw.githubusercontent.com/sqlProvider/SASS-Lang/master/Resources/next.png