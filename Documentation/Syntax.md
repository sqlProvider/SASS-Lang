## 1. Syntax

**`SASS`** iki farklı syntax'a izin verir. 

Birincisi CSS syntax'ına benzer bu syntax **`Sassy CSS`** adı ile bilinir.
Sassy CSS'in dosya uzantısı **`.scss`** şeklindedir ayrıca 
SASS'dan daha fazla CSS hack'i ve trick'i kullanmaya izin verir.

İkincisi SASS'ın ortaya çıktığı ilk yazım şeklidir. 
Süslü parantezler **`{,}`** ve noktalı virgül **`;`** kullanılmaz.
Dil yapısı tablar veya boşluklarla sağlanır. **`Pyhton, Ruby`** vb. dillerinin syntax'ına benzer.
SASS'ın dosya uzantısı **`.sass`** şeklindedir.

Bazı insanlar SASS'ın yazımını SCSS'den daha kolay ve hızlı bulurken bazı insanlar 
CSS'in verdiği alışkanlıklarla SCSS kullanırlar. 
SASS geliştiricileri bu iki syntax farkından kullanıcıların etkilenmemesi için çevirici bir araç sunmuştur.

```bash
# SCSS'i SASS'a çevirmek için sass-convert komutu kullanılır.
# Kullanım şekli;
# sass-convert cevirilecekdosya.[scss|sass] yenisassdosyasi.[scss|sass] 
#
# Örnek kullanımlar
$ sass-convert style.scss style.sass
$ sass-convert style.sass style.scss
```
>Bu komut css dosyası oluşturmaz. SASS'tan SCSS'e veya SCSS'den SASS'a çevirme yapar.	

---
| [![Back][back]](https://github.com/sqlProvider/SASS-Lang) | [![Next][next]](UsingSASS.md) |
|-------|-----:|

[back]: https://raw.githubusercontent.com/sqlProvider/SASS-Lang/master/Resources/back.png
[next]: https://raw.githubusercontent.com/sqlProvider/SASS-Lang/master/Resources/next.png