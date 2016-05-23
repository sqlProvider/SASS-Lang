# Yorum Satırları /* */ ve //

SASS iki tür yorum satırını destekler. CSS'in gerçek yorum satırı olan **` /* */ `** ve SASS ile beraber gelen **` // `**. 
Çok satırlı yorum satırları derlenirken olduğu gibi bırakılır.
Ancak tek satırlık yorum satıları derlenme sürecinde ortadan kaldırılır ve CSS'e yansımaz.

```sass
	/* Bu yorum satırı
	* birkaç satırlıktır.
	* CSS syntax'ı ile uyumludur,
	* derlenirken CSS içinde de yer alır. */
	body {color: black; }

	// Bu yorum satırı tek satırlıktır.
	// CSS de böyle bir kullanım mevcut değildir,
	// Derlenirken çıkış dosyasına yazılmaz.
	a {color: green; }
```

Yukarıda ki yorum satırı örneğinin çıktısı aşağıdaki gibidir.

```css
	/* Bu yorum satırı
	* birkaç satırlıktır.
	* CSS syntax'ı ile uyumludur,
	* derlenirken CSS içinde de yer alır. */
	body {color: black; }
	a{color: green; }
```

--
| [![Back][back]](CSS.md) | [![Next][next]](#) |
|-------|-----:|

[back]: https://raw.githubusercontent.com/sqlProvider/SASS-Lang/master/Resources/back.png
[next]: https://raw.githubusercontent.com/sqlProvider/SASS-Lang/master/Resources/next.png