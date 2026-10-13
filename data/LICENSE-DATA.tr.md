# Veri lisansı ve atıf

*English version: [LICENSE-DATA.md](LICENSE-DATA.md)*

Bu klasördeki veri dosyaları (`osmanlica_koken.csv`, `train.csv`, `val.csv`, `test.csv` ve varsa `cache_*.json`), Vikisözlük'ün (Wiktionary) İngilizce sürümünden (https://en.wiktionary.org) türetilmiştir.

## Kaynak ve lisans

Vikisözlük maddelerinin özgün metinleri **Creative Commons Attribution-ShareAlike 4.0 (CC BY-SA 4.0)** ve **GNU Free Documentation License (GFDL)** çift lisansı altındadır (bkz. https://en.wiktionary.org/wiki/Wiktionary:Copyrights).

Bu nedenle bu klasördeki türetilmiş veri dosyaları da **CC BY-SA 4.0** altında paylaşılmaktadır:

- **Atıf:** Veri, Vikisözlük katkıcılarının eseridir. Kaynak: https://en.wiktionary.org
- **Aynı lisansla paylaşım:** Bu veriyi değiştirip paylaşırsanız aynı lisansı kullanmanız gerekir.
- Lisans metni: https://creativecommons.org/licenses/by-sa/4.0/

## Yapılan değişiklikler

- Vikisözlük'ün "Ottoman Turkish terms ..." köken kategorilerinden kelimeler toplandı ve kategoriye göre Arapça, Farsça veya Türkçe olarak etiketlendi.
- Yalnızca ana sözcükler (lemma), tek kelimelik, Arap harfli maddeler alındı; harekeler silindi.
- Birden fazla sınıfta görünen 101 kelime çıkarıldı; 1 harfli 4 kayıt çıkarıldı; sıfır genişlikli ayırıcı (ZWNJ) karakterleri silindi.
- Özel isimler `ozel_isim` sütunuyla işaretlendi.
- Veri %70 eğitim, %15 doğrulama ve %15 test olarak, sınıf oranları korunarak (`random_state=42`) bölündü.

Toplama tarihi: en geç 7 Ekim 2026. Özel isim kategorisi Ekim 2026'da çekilmiştir (kesin gün kaydedilmemiştir).

## Kod lisansı

Bu klasör dışındaki kod (not defteri) MIT lisansı altındadır (bkz. kök dizindeki `LICENSE`).
