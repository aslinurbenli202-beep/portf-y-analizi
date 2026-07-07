# Portföy Optimizasyonu Projesi

Doğrusal Programlama dersi kapsamında hazırlanmış, dört varlıktan oluşan
bir portföy için Markowitz risk-getiri modeliyle Sharpe oranını maksimize
eden optimal ağırlıkların bulunduğu bir Excel çalışması.

## Amaç
Platin, devlet tahvili, Vakıfbank hissesi ve THY hissesinden oluşan bir
portföyde, varlıklara verilen ağırlıkların portföyün beklenen getirisini
ve riskini (standart sapma) nasıl etkilediğini modellemek; risk/getiri
performansını en iyi seviyeye taşıyan (Sharpe oranını maksimize eden)
ağırlık dağılımını optimizasyon yoluyla bulmak.

## Veri
Dört varlık için günlük fiyat/kur verileri (2025 başından geriye ~68 gün):
- **Platin**: TL/Kg fiyatı
- **Tahvil**: gösterge tahvil faizi
- **Vakıfbank**: hisse kapanış fiyatı
- **THY**: hisse kapanış fiyatı

## Yöntem
1. Günlük getiriler: `(bugünkü fiyat - dünkü fiyat) / dünkü fiyat`
2. Her varlık için ortalama günlük getiri ve varyans (`AVERAGE`, `VAR`)
3. 4x4 varyans-kovaryans matrisi (`COVAR`)
4. Günlük risksiz faiz oranı (yıllık %5'in güne çevrilmiş hali)
5. Sharpe oranını maksimize eden portföy ağırlıklarının optimizasyonu,
   kısıtlar: ağırlıklar toplamı 1, hiçbir ağırlık negatif olamaz (açığa
   satış yok)
6. Beklenen portföy getirisi: `MMULT(ağırlıklar, ortalama getiriler)`
7. Portföy riski: `SQRT(MMULT(MMULT(ağırlıklar, kovaryans matrisi), ağırlıklar)))`
8. Sharpe oranı: `(beklenen getiri - risksiz faiz oranı) / standart sapma`

## Sonuç
| Varlık | Ağırlık |
|---|---|
| Platin | %88.2 |
| Tahvil | %0 |
| Vakıfbank | %0 |
| THY | %11.8 |

- **Günlük beklenen getiri:** %0.065
- **Günlük risk (standart sapma):** %1.03
- **Sharpe oranı:** +0.043

Portföy, düşük korelasyonlu iki varlık (Platin ve THY) arasında
çeşitlendirilmiş durumda; riski tek bir varlığa yoğunlaşmış bir portföye
göre belirgin şekilde daha düşük, beklenen getirisi ise pozitif.

## Notlar
Bu proje bir üniversite dersi kapsamında hazırlanmıştır ve eğitim
amaçlıdır; yatırım tavsiyesi değildir.
