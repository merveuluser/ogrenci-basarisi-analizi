# Ortaöğretim Öğrencilerinde Akademik Başarıyı Etkileyen Faktörler

**Ders:** Araştırma Yöntem ve Teknikleri (2026–2027 Güz) · Marmara Üniversitesi, Bilgisayar Programcılığı (Uzaktan Öğretim)
**Hazırlayan:** Merve Uluser
**Aşama:** Vize. Proje sürüyor; bu depo dönem boyunca güncellenecek.

## Problem
Öğrenci başarısızlığı hem öğrenci hem de okul açısından maliyetli bir sorundur. Başarısızlık riski taşıyan öğrencilerin erken fark edilmesi, danışmanlık ve destek hizmetlerinin zamanında planlanmasına yardımcı olabilir. Ancak hangi demografik, sosyal ve okulla ilgili etkenlerin başarıyla daha güçlü ilişkili olduğu ve önceki dönem notları bilinmeden başarının ne ölçüde tahmin edilebileceği açık değildir.

## Araştırma sorusu
Ortaöğretim öğrencilerinde haftalık çalışma süresi, geçmiş ders başarısızlığı, devamsızlık ve aile/sosyal etkenler ile dönem sonu notu (G3) arasında ilişki var mıdır? Bu değişkenler öğrencinin dersi geçip geçmeyeceğini önceden tahmin etmeye yeterli midir?

### Alt problemler
1. Öğrencilerin dönem sonu notlarının ve geçme oranlarının dağılımı nasıldır?
2. Çalışma süresi, geçmiş başarısızlık ve devamsızlık ile G3 arasında ilişki var mıdır?
3. Önceki dönem notları (G1, G2) dahil edildiğinde ve hariç tutulduğunda geçme/kalma ne doğrulukla tahmin edilebilir?
4. Tahminde en etkili değişkenler hangileridir?

### Hipotezler
| | Hipotez (H₁) | Sıfır hipotezi (H₀) |
|---|---|---|
| H1 | Haftalık çalışma süresi ile G3 arasında pozitif ilişki vardır. | İlişki yoktur. |
| H2 | Geçmiş başarısızlık sayısı ile G3 arasında negatif ilişki vardır. | İlişki yoktur. |
| H3 | Devamsızlık ile G3 arasında negatif ilişki vardır. | İlişki yoktur. |

**Sayıltı:** Veri setindeki not ve anket bilgilerinin öğrencilerin gerçek durumunu yansıttığı varsayılmıştır.
**Sınırlılık:** Veri, Portekiz'deki iki devlet okulundan ve 2005–2006 öğretim yılından derlenmiştir; sonuçlar Türkiye'ye doğrudan genellenemez. Korelasyon nedensellik göstermez.

## Veri seti
- **Kaynak:** Cortez, P. (2008). *Student Performance* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5TG7T
- **Sayfa:** https://archive.ics.uci.edu/dataset/320/student+performance
- **Lisans:** CC BY 4.0. Kaynak gösterilerek kullanılabilir.
- **İçerik:** Matematik (n = 395) ve Portekizce (n = 649) dersleri; 33 değişken (demografik, sosyal, okulla ilgili değişkenler ve G1, G2, G3 notları). Eksik değer yoktur.
- Ders kuralları gereği **kişilerden doğrudan veri toplanmamıştır**. Yalnızca açık erişimli ikincil veri kullanılmıştır.
- Veri dosyaları depoya konmamıştır. Notebook çalıştırıldığında veri doğrudan UCI'den indirilir (bkz. [`veri/README.md`](veri/README.md)).

## Yöntem
| Adım | Yöntem / araç |
|---|---|
| Ortam | Google Colab, Python (pandas, SciPy, scikit-learn, matplotlib, seaborn) |
| Betimsel analiz | Ortalama, standart sapma, medyan, frekans; histogram ve kutu grafikleri |
| Hipotez testleri | Spearman sıra korelasyonu (sayısal/sıralı değişkenler), Mann–Whitney U (iki gruplu kategorik değişkenler); α = 0,05 |
| Tahmin | İkili sınıflandırma (geçti: G3 ≥ 10). Çoğunluk sınıfı (temel model), lojistik regresyon, karar ağacı, rastgele orman |
| Değerlendirme | 10 katlı tabakalı çapraz doğrulama; doğruluk ve makro F1; permütasyon önemi |
| Sürümleme | Git / GitHub |

## İlk bulgular (Matematik dersi)
- Öğrencilerin %67,1'i dersi geçmiştir. 38 öğrencinin G3 notu 0'dır.
- **H2 desteklendi:** Geçmiş başarısızlık, G3 ile en güçlü ilişkili değişkendir (ρ = −0,36; p < 0,001).
- **H1 desteklendi (zayıf ilişki):** Çalışma süresi ile G3 arasında ρ = 0,11 (p = 0,037).
- **H3:** Tüm örneklemde anlamlı ilişki bulunmadı (ρ = 0,02; p = 0,73). G3 = 0 olan öğrencilerin hepsinin devamsızlığı 0 olarak kayıtlıdır. Bu öğrenciler çıkarıldığında beklenen negatif ilişki ortaya çıkmaktadır (ρ = −0,24; p < 0,001).
- **Tahmin:** G1 ve G2 dahil edildiğinde lojistik regresyon %92,9 doğruluğa ulaşmaktadır. G1 ve G2 hariç tutulduğunda modeller, %67,1 doğruluklu temel modeli ancak sınırlı ölçüde geçebilmektedir (en iyi: %69,4). Erken tahmin daha zordur.

Ayrıntılar: [`analiz/ogrenci_basarisi_analiz.ipynb`](analiz/ogrenci_basarisi_analiz.ipynb) · Sonuç tablosu: [`sonuclar_model.csv`](sonuclar_model.csv)

## Depo yapısı
```
├── README.md                 Proje özeti (bu dosya)
├── analiz/                   Google Colab notebook'u
├── sekiller/                 Analizin ürettiği grafikler
├── uml/                      Use case, sınıf ve aktivite diyagramları (PNG + SVG)
├── veri/                     Veri kaynağı ve lisans notu
├── rapor/                    Vize raporu
└── sonuclar_model.csv        Model karşılaştırma sonuçları
```

## Nasıl çalıştırılır?
1. `analiz/ogrenci_basarisi_analiz.ipynb` dosyasını Google Colab'da açın (*File → Open notebook → GitHub*).
2. *Runtime → Run all* ile tüm hücreleri çalıştırın. Veri UCI'den otomatik olarak indirilir; ek kurulum gerekmez.
3. Sonuçlar `rastgele_tohum = 42` ile sabitlendiği için tekrarlanabilir.

## Literatür (özet)
| Kaynak | Veri | Yöntem | Projeye katkısı |
|---|---|---|---|
| Cortez & Silva (2008) | Bu projedeki veri seti | Karar ağacı, rastgele orman, SVM, sinir ağı; G1/G2 dahil-hariç senaryoları | Veri setinin özgün çalışması; senaryo kurgusu buradan alındı |
| Romero & Ventura (2010, 2020) | Derleme | Eğitsel veri madenciliği alanının genel görünümü | Kavramsal çerçeve |
| Shahiri vd. (2015) | Derleme | Başarı tahmininde kullanılan değişkenler ve yöntemler | Değişken seçimi gerekçesi |
| Yağcı (2022) | Türkiye, 1854 üniversite öğrencisi | RF, SVM, LR, NB, k-NN | Türkiye bağlamında karşılaştırma |
| Credé vd. (2010) | Meta-analiz | Devam ile notlar arasındaki ilişki | H3'ün kuramsal dayanağı |
| Aydın (2025); Zilyas & Yılmaz (2023) | Türkçe çalışmalar | Özellik seçimi, RF, CART | Türkçe literatürde benzer yaklaşımlar |

Tam künyeler vize raporunun kaynakça bölümündedir.

## Planlanan adımlar (finale kadar)
- [ ] Sınıf dengesizliğine yönelik yöntemler (sınıf ağırlığı, eşik ayarı)
- [ ] Hiperparametre ayarı ve ek modellerin denenmesi
- [ ] G3'ün sayısal tahmini (regresyon)
- [ ] İki dersin karşılaştırmalı analizi
- [ ] Bulguların literatürle tartışılması ve final raporu

## Yapay zekâ kullanımı beyanı
Kodun ve diyagramların ilk taslağının hazırlanmasında yapay zekâ destekli bir asistandan (Claude) yararlanılmıştır. Analiz sonuçları kod çalıştırılarak elde edilmiştir. Kaynak künyeleri DOI ve yayıncı sayfaları üzerinden doğrulanmıştır.
