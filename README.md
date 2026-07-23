# kedi-mama-takip
kedinizin günlük mama ihtiyacını hesaplayıp elinizdeki mama paketinin kaç gün yeteceğini söyler.
# Kedi Mama Hesaplama Aracı

Elinizde kaç gram kedi maması olduğuna bağlı olarak, mamanın kaç tam gün boyunca
yeterli olduğunu gösterir. Kedinizin günde ne kadar yemesi gerektiğini bilip
bilmemeniz önemli değil — gerekirse program onu da hesaplar.

## Ne yapar?

1. **Asıl amaç:** kedinin maması kaç gün yeterli, aşağı yuvarlayıp söyler.
   Yuvarlama bilinçli olarak aşağıdır: program size olduğundan fazla gün vaat
   etmesin, mama beklenmedik şekilde erken bitmesin diye.
2. **Gerekirse:** kedinin kilosuna, yaşam evresine ve kullandığı mamaya göre
   günde kaç gram yemesi gerektiğini hesaplar, sonra asıl amacı gerçekleştirir.

## Nasıl çalıştırılır?

Program bir Python not defteridir (`.ipynb`). Kurulum gerektirmez.

1. Bu depodan `kedi_mama.ipynb` dosyasını indirin
2. [colab.research.google.com](https://colab.research.google.com) adresine girin
3. **Dosya → Not defterini aç → Yükle** → indirdiğiniz dosyayı seçin
4. Kod hücresini çalıştırın (▶ düğmesi veya `Ctrl+Enter`)
5. Program sorularını sırayla sorar; cevaplayıp Enter'a basın

## Uyarılar

**Çarpanlar ve ihtiyaç tablosu kaba tahmindir. Veterinerinize danışın.**

Programı kullanmak için önceden kesin bilinmesi gerekenler:

- kedinizin yaşam evresi
- kedinizin kilosu

Kedinizin ne kadar yemesi gerektiğini bilmiyorsanız ve markanın çeşidine özel
kesin hesap yapmak istiyorsanız, ayrıca kullandığınız mamanın kilogram başına
kalori miktarı da gerekir.

Sizden istenen birimleri karıştırırsanız uygulama yanlış hesap yapabilir. Gram mı
kilogram mı istendiğine ve büyük/küçük harfe dikkat ediniz.

## Hesap nasıl yapılıyor?

Önce dinlenme halindeki enerji ihtiyacı (RER) hesaplanır — insanlardaki bazal
metabolizmanın gerektirdiği enerjinin karşılığı:

```
RER = 70 * (kilogram cinsinden vücut ağırlığı) ** 0.75
```

Bu enerji sadece hayati fonksiyonları sürdürmek için gereklidir. Kediler gün
içinde çok hareketli olduğundan tek başına yeterli olmaz. Yaşa ve yaşam tarzına
göre değişen bir katsayıyla çarpmak gerekir (MER).

Programın kullandığı katsayılar:

- yavru (0-4 ay): 3.0
- yavru (4-12 ay): 2.0
- kısır yetişkin: 1.2
- kısır olmayan yetişkin: 1.4
- yaşlı: 1.2

```
MER = katsayı * RER          (günlük kalori ihtiyacı)
gram = 1000 * MER / kcal_kg  (kalori ihtiyacını grama çevirir)
```

## Bilinen eksikler

- Evet/Hayır sorusu büyük/küçük harfe duyarlı
- Mama türü kcal değerleri sabit bir tablodan geliyor, gerçek marka verisi değil
