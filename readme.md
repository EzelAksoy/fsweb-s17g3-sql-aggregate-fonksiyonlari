# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

## Proje Kurulumu

Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

### Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#### Tablolar

`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]

##### Görevler

Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın.

MIN-MAX, COUNT-AVG-SUM, GROUP BY, JOINS (INNER, OUTER, LEFT, RIGHT
#ilk 3 soruyu join kullanmadan yazın. 1) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.

    	CEVAP:SELECT O.ograd, O.ogrsoyad, I.atarih FROM ogrenci AS O, islem AS I WHERE O.ogrno=I.ogrno


    2) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

    	CEVAP:Select k.kitapadi,t.turadi from kitap as k,
              tur as t Where k.turno=t.turno and t.turno in(6,4)


    3) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.

    	CEVAP:Select o.ograd,o.ogrsoyad,o.ogrno,k.kitapadi from ogrenci as o,
    		  islem as i,kitap as k where i.ogrno=o.ogrno and sinif in('10B','10C')

    #join ile yazın
    4) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.

    	CEVAP:Select o.ograd,o.ogrsoyad,i.atarih from ogrenci as o
    		  Inner Join islem as i On i.ogrno=o.ogrno


    5) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

    	CEVAP: Select k.kitapadi,t.turadi from kitap as k
    		   Inner Join tur as t On t.turno=k.turno
    		   Where turadi in('Fıkra','Hikaye')


    6) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.

    	CEVAP: Select o.ograd,o.ogrsoyad,o.ogrno,k.kitapadi,o.sinif from ogrenci as o
    		   Inner Join islem as i On i.ogrno=o.ogrno
    		   Inner Join kitap as k On k.kitapno=i.kitapno
    		   Where sinif in('10B','10C')


    7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerinde listede görünsün.

    	CEVAP: Select o.ograd,o.ogrsoyad,o.ogrno,o.sinif,i.atarih from ogrenci as o
    		   Left Join islem as i On i.ogrno=o.ogrno


    8) Kitap almayan öğrencileri listeleyin.

    	CEVAP: Select o.ograd,o.ogrsoyad,o.ogrno,o.sinif,i.atarih from ogrenci as o
    		   Left Join islem as i On i.ogrno=o.ogrno
    		   Where ISNULL(i.atarih)


    9) Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.

    	CEVAP: Select COUNT(k.kitapno) as Toplam,k.kitapadi,k.kitapno from kitap as k
               Left Join islem as i On k.kitapno=i.kitapno
               Group By k.kitapno


    10) Alınan kitapların kitap numarasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.

    	CEVAP: Select COUNT(k.kitapno) as Toplam,k.kitapadi,k.kitapno from kitap as k
               Left Join islem as i On k.kitapno=i.kitapno
               Group By k.kitapno


    11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.

    	CEVAP: Select o.ograd,o.ogrsoyad,k.kitapadi from ogrenci as o
    		   Left Join islem as i On i.ogrno= o.ogrno
    		   Left Join kitap as k On k.kitapno=i.kitapno

    12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.

    	CEVAP: Select o.ograd,o.ogrsoyad,k.ktipadi,y.yazarad,y.yazarsoyad,k.turadi,i.atarih from ogrenci as o
    		   Left Join isle as i On i.ogrno=o.ogrno
    		   Left Join kitap as k On k.kitapno=i.kitapno
    		   Left Join yazar as y On y.yazarno= k.yazarno
    		   Left Join tur as t On t.turno=k.turno


    13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.

    	CEVAP: Select o.ogrno,o.ograd,o.ogrsoyad,COUNT(k.kitapadi) as KitapSayisi from ogrenci as o
    		   Left Join islem as i On i.ogrno=o.ogrno
    		   Left Join kitap as k On i.kitapno=k.kitapno
    		   Where o.sinif in('10A','10B')
    		   Group By ogrno


    14) Tüm kitapların ortalama sayfa sayısını bulunuz.
    #AVG
    	CEVAP: Select AVG(sayfasayisi) from kitap

    15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.

    	CEVAP: Select * from kitap
    		   Where sayfasayisi > (SELECT AVG(sayfasayisi) from kitap)


    16) Öğrenci tablosundaki öğrenci sayısını gösterin.

    	CEVAP: Select Count(ogrno) from ogrenci


    17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.

    	CEVAP: Select Count(ogrno) as toplamsayi from ogrenci


    18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.

    	CEVAP: Select Distinct(ograd) from ogrenci


    19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

    	CEVAP: Select MAX(sayfasayisi)  from kitap


    20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

    	CEVAP: Select kitapadi,sayfasayisi  from kitap
    		   Where sayfasayisi=(Select MAX(sayfasayisi)  from kitap)


    21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

    	CEVAP: Select MIN(sayfasayisi) from kitap


    22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

    	CEVAP: Select kitapadi,sayfasayisi from kitap
    		   Where sayfasayisi =(Select MIN(sayfasayisi) from kitap)


    23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.

    	CEVAP: Select * from kitap as k,
               tur as t where t.turno = k.turno and t.turadi = 'Dram' and sayfasayisi =(Select MAX(sayfasayisi) from kitap)


    24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.

    	CEVAP: Select Sum(sayfasayisi) from ogrenci as o
    		   Left Join islem as i On o.ogrno=i.ogrno
    		   Left Join kitap as k On i.kitapno= k.kitapno
    		   Where o.ogrno=15



    25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )

    	CEVAP: Select CONCAT(Count(ograd),'   adet'),ograd from ogrenci
    		   Group by ograd


    26) Her sınıftaki öğrenci sayısını bulunuz.

    	CEVAP: Select COUNT(ogrno),sinif from ogrenci
    		   Group by sinif


    27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz.

    	CEVAP: Select CONCAT(COUNT(ogrno),'    adet'),cinsiyet,sinif from ogrenci
    		   Group by sinif,cinsiyet




    28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.

    	CEVAP: Select o.ogrno,o.ograd,o.ogrsoyad,SUM(k.sayfasayisi) as Toplam from ogrenci as o
    		   Left Join islem as i  On o.ogrno= i.ogrno
    		   Left Join kitap as k On k.kitapno=i.kitapno
    		   Group by o.ogrno
    		   order by Toplam DESC


    29) Her öğrencinin okuduğu kitap sayısını getiriniz.

    	CEVAP: Select Count(k.kitapno), o.ograd,o.ogrsoyad  from ogrenci as o
    		   Left Join islem as i  On o.ogrno= i.ogrno
    		   Left Join kitap as k On k.kitapno=i.kitapno
    		   Group by o.ogrno
