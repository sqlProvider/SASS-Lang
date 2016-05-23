# CSS 

Projemiz tamam ve çalışma ortamımızı da ayarladık atık SASS ile nasıl CSS oluşturacağımızı öğrenmek kaldı.

## İç İçe Kurallar

SASS iç içe kurallar tanımlamıza olanak tanır. Karmaşık CSS tanımlarını ortadan kaldırmak için geliştirilmiş bir özelliktir. SASS'ın en çok kullanılan özellliği diyebiliriz. Örneği inceleyecek olursak;
```sass
	#main{
		color: #FFF;
		width: 80%;
		
		.redBox{
			background-color: #F00;
			color: #000;
		}
	}
```
Yazdığımız satırlar derlendikten sonra aşağıdaki CSS'e çevrilir.
```css
	#main{
		color: #FFF;
		width: 80%;
	}
	#main .redBox{
		background-color: #F00;
		color: #000;
	}
```

Bir başka kullanım olarak iç içe kuralları `,` ile ayırabiliriz;

```sass
	#main{
		color: #FFF;
		width: 80%;
		
		.redBox, p{
			background-color: #F00;
			color: #000;
		}
	}
```
Yazdığımız satırlar derlendikten sonra aşağıdaki CSS'e çevrilir.
```css
	#main{
		color: #FFF;
		width: 80%;
	}
	#main .redBox, #main p{
		background-color: #F00;
		color: #000;
	}
```

--

## Evebeyn Referansı: &

Yazdığımız bir kuralın içinden bir üstteki kurala etki etmek için `&` anahter kelimesi kullanılır. 
Bu işaret class içerisindeki bir fonksiyon içinde `this` kullanmaya benzer. 
Örneğin sayfadaki bütün `<a></a>` taglarını bir yerden yönetmek istiyoruz ve aşağıdaki gibi bir örnek hazırlıyoruz;

```sass
	a {
		font-weight: bold;
		text-decoration: none;
		&:hover { text-decoration: underline; }
		body.firefox & { font-weight: normal; }
	}
```
Yazdığımız satırlar derlendikten sonra aşağıdaki CSS'e çevrilir.

```css
a {
	font-weight: bold;
	text-decoration: none; 
}
a:hover {
	text-decoration: underline; 
}
body.firefox a {
	font-weight: normal; 
}
```
--

`&` karakteri her zaman kullanıldığı yerin **bir üst kuralına** referans olur.

```sass
#main {
	color: black;
	a {
		font-weight: bold;
		&:hover { color: red; }
	}
}
```
Yukarıdaki satırlarda `&` karakteri bir üstü yani `a` tagına referanstır. Derlendikten sonraki çıktı şu şekildedir.

```css
#main {
	color: black;
}
#main a {
	font-weight: bold; 
}
#main a:hover {
	color: red; 
}
```
--

`&` karakterini referans olarak almayı öğrendik. Bu karakter referans olduğu kuralı string olarak döndürür. `&` karakterinin en kompleks kullanımı burda dervreye girer.
```scss
#main {
	color: black;
	&-sidebar { border: 1px solid; }
}
```
Evet string olarak döndürdü ve bir üst kuralı olduğu yere yapıştırdı. CSS'e derlenmiş haline göz atalım.
```css
#main {
	color: black; 
}
#main-sidebar {
	border: 1px solid;
}
```
`#main` nin içerisinde bir kural olmak yerine kendi başına bir kural oldu. Bunun nedeni `&` karakterinin ilk olarak bir üstteki kural ile değiştirilmesidir.
`&-sidebar` yerine `&.sidebar` yazsaydık bu sefer `main` ID'sine sahip aynı zamanda `sidebar` class'ını almış bir elementi seçmiş olacaktık.

Burada yeni bir ID'nin oluşmasının nedeni `$` karakterinin SASS tarafından `#main`'e dönüştürülmesidir.

## İç İçe Özellikler

Kuralları iç içe yazabildiğimiz gibi özellikleri de iç içe yazabiliriz. 
CSS'de çok fazla tekrar eden özellikler var mesela bunlardan birisi `background`. Bu özellik tireden sonra 10-15 tane özelliğe evriliyor.
Örnek üzerinde inceleyecek olursak;
```scss
#main{
	background:{
		color: #FFF;
		image: url("foo/bar.png");
		repeat: no-repeat;
		position: 50% 50%;
		// Ve daha fazlası
	}
}
```
Yazdığımız SASS kodlarında özellik mi yoksa kural mı olduğunu belirtmek için buradaki örnek için `background**:**` şeklinde kullanmalıyız.
`:` karakterini koymayı unutursak derlenme sonucu mantıksal olarak hatalı olacaktır.
```css
#main{
	background-color: #FFF;
	background-image: url("foo/bar.png");
	background-repeat: no-repeat;
	background-position: 50% 50%;
}
```

Bir de `:` karakterini unuttuğumuzda derleneceği hali inceleyelim. SASS böyle bir durumda hata vermeyecektir ve derleyecektir. Yapılan hata mantıksal bir hatadır.
```css
#main background{
	color: #FFF;
	image: url("foo/bar.png");
	repeat: no-repeat;
	position: 50% 50%;
}
```
--

İç içe özellik yazılırken farklı bir yöntem de kullanılabilir. Örneği inceleyim;
```sass
span{
	font: 20px/24px "Open Sans" {
		weight: bold;
	}
}
```
Font özelliğini yazarken `:` den sonra CSS'te ki font özelliği gibi birkaç değer tanımlanmış ve sonrasında `font-` ile başlayan özellikleri kullanmak için iç içe özellik tanımı kullanılmış.
```css
span{
	font: 20px/24px "Open Sans";
	font-weight: bold;
}
```