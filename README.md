# Osmanlıca Kelimelerin Köken Dilini Yazımından Tahmin Etme

Makine öğrenmesi ile Arapça, Farsça ve Türkçe ayrımı

[![Colab'da aç](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/esrakonya/osmanlica-koken-tahmini/blob/main/osmanlica_koken_projesi.ipynb)

## Problem

Arap harfleriyle yazılmış tek bir Osmanlıca kelimenin köken dilini (Arapça, Farsça veya Türkçe) yalnızca yazımından tahmin etmek. Girdi kelimenin Arap harfli yazımı, çıktı üç sınıftan biridir. Çalışmanın temel sorusu: yazım tek başına köken hakkında ne kadar bilgi taşır?

## Veri

- **Kaynak:** Vikisözlük (en.wiktionary.org), herkese açık MediaWiki API, hesap veya API anahtarı gerekmez.
- **Etiketler:** Maddelerin köken kategorilerinden türetildi (Arapça: "borrowed from Arabic"; Farsça: "borrowed from Persian / Classical Persian"; Türkçe: "inherited from Proto-Turkic / Proto-Common Turkic / Proto-Oghuz / Early Old Oghuz").
- **Boyut:** 3298 kelime (Arapça 1466, Türkçe 1089, Farsça 743). Bölme: eğitim 2308 / doğrulama 495 / test 495 (stratified, `random_state=42`).
- **Toplama tarihi:** en geç 7 Ekim 2026. Özel isim kategorisi Ekim 2026'da çekildi (kesin gün kaydedilmedi). Vikisözlük içeriği zamanla değişir; sonuçları yeniden üretmek için `data/` klasöründeki dosyaları kullan.
- **Lisans:** Veri dosyaları CC BY-SA 4.0 (ve GFDL) altındadır, ayrıntı için `data/LICENSE-DATA.md`.

## Yöntem

Modeller basitten karmaşığa doğru karşılaştırıldı: çoğunluk sınıfı (M0), Lojistik Regresyon ve Doğrusal SVM (1-3 harflik karakter n-gram, TF-IDF), karakter CNN (3 seed) ve BiLSTM. Model seçimi yalnızca doğrulama kümesinde yapıldı; BiLSTM doğrulamada elendi. Test kümesi model seçiminde kullanılmadı; ayarlar sabitlendikten sonra, değiştirilmeden nihai değerlendirmede ölçüldü (yeniden çalıştırmada sonuçlar birebir tekrarlandı).

## Test sonuçları (495 kelime)

| Model | Accuracy (%95 GA) | Macro-F1 (%95 GA) |
|---|---|---|
| Çoğunluk sınıfı (M0) | 0,444 [0,400-0,491] | 0,205 [0,190-0,220] |
| Lojistik Regresyon | 0,802 [0,766-0,836] | 0,787 [0,749-0,825] |
| Doğrusal SVM | 0,816 [0,782-0,848] | 0,797 [0,761-0,835] |
| Karakter CNN (3 seed ort.) | 0,786 ± 0,011 | 0,770 ± 0,010 |

Güven aralıkları bootstrap ile (2000 yeniden örnekleme) hesaplandı. Modeller arasındaki farklar küçüktür ve güven aralıkları büyük ölçüde örtüşür; LR ile CNN (seed 1) arasında McNemar testi anlamlı fark bulmadı (p = 0,124). Bu nedenle bir model üstünlüğü iddia edilmemektedir.

## Başlıca bulgular ve sınırlılıklar

- Hataların yaklaşık yarısı Arapça ile Farsça arasındadır. Türkçe kelimeler, özellikle son harfin ق veya ك olması sayesinde nispeten iyi ayrılır.
- Etiketler, kelimenin Osmanlıcaya geçiş yolunu yansıtır; nihai kökenini her zaman temsil etmez.
- Model yalnızca üç dil arasında ayrım yapar.
- Birden fazla sınıfta görünen 101 belirsiz kelime çıkarıldı; bu, raporlanan başarımı gerçek koşullara göre iyimser yapmış olabilir.
- Test kümesi küçüktür, güven aralıkları geniştir (yaklaşık ±3,5 puan).
- Etiket denetimi yalnızca 10 kelimelik bir örneklemle yapıldı, genellenemez.

## Yeniden üretme

1. Yukarıdaki Colab rozetiyle not defterini aç (GPU önerilir: Çalışma zamanı > T4 GPU).
2. `data/osmanlica_koken.csv` dosyasını Colab'a yükle.
3. `VERI_TOPLA = False` kalsın ve hücreleri sırayla çalıştır. Test kümesi yalnızca E bölümünde kullanılır.

## Yapı

```
osmanlica_koken_projesi.ipynb   tüm çalışma (çıktılarıyla)
data/                           veri dosyaları ve lisans notu
figures/                        rapor görselleri
LICENSE                         kod lisansı (MIT)
```

## Lisans

- **Kod:** MIT.
- **Veri:** CC BY-SA 4.0 ve GFDL (Vikisözlük). Ayrıntı: `data/LICENSE-DATA.md`.
