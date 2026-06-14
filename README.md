# CST Studio Suite ve MATLAB ile Elektronik Hüzme Taramalı Doğrusal Anten Dizisi Tasarımı

Bu proje; 1 GHz merkez frekansında çalışan, yarı dalga boyu ($d = \lambda/2$) kriterine göre konumlandırılmış 9 elemanlı doğrusal bir dipol anten dizisinin elektromanyetik modellenmesi, analitik analizi ve elektronik hüzme yönlendirme (beamsteering) süreçlerini içermektedir.

Proje kapsamında, ana hüzme odağı broadside ($0^{\circ}$) durumunun yanı sıra analitik olarak hesaplanan faz kaymalarıyla $12^{\circ}$ ve $38^{\circ}$ hedef açılarına başarıyla yönlendirilmiş; CST simülasyon sonuçları ile MATLAB analitik modelleri üst üste bindirilerek doğrulanmıştır.

---

## 🛠️ Tasarım ve Anten Geometrisi Parametreleri

- **Merkez Frekansı ($f_{0}$):** 1.0 GHz
- **Serbest Uzay Dalga Boyu ($\lambda$):** 300 mm
- **Dizi Elemanı:** Yarım Dalga Dipol Anten (Half-Wave Dipole)
- **Optimize Edilmiş Dipol Boyu ($L_{dipol}$):** Uç etkilerini (fringing fields) sönümlemek adına $141 \text{ mm} \ (0.47\lambda)$ olarak ayarlanmıştır.
- **Elemanlar Arası Mesafe ($d$):** $150 \text{ mm} \ (0.5\lambda)$
- **Giriş Empedansı:** 73 $\Omega$

---

## 📐 Teorik Altyapı ve Faz Hesaplamaları

Doğrusal anten dizisinde ana hüzmeyi uzayda belirli bir $\theta_{0}$ açısına elektronik olarak yönlendirebilmek için ardışık elemanlar arasına uygulanması gereken sabit faz farkı ($\beta$), **Doğrusal Dizi Tarama Denklemi** ile hesaplanır:

$$\beta = -k \cdot d \cdot \sin(\theta_{0})$$

$k = \frac{2\pi}{\lambda}$ ve $d = \frac{\lambda}{2}$ değerleri yerine konulduğunda denklem derece cinsinden şu basitleştirilmiş hale gelir:

$$\beta = -180^{\circ} \cdot \sin(\theta_{0})$$

### Target Faz Kaymaları ve Port Konfigürasyonları:
- **Durum 1: Broadside ($\theta_{0} = 0^{\circ}$)** ➡️ $\beta = 0^{\circ}$ (Tüm portlar eş fazlı)
- **Durum 2: 1. Doğrultu ($\theta_{0} = 12^{\circ}$)** ➡️ $\beta = -37.42^{\circ}$
- **Durum 3: 2. Doğrultu ($\theta_{0} = 38^{\circ}$)** ➡️ $\beta = -110.82^{\circ}$

---

## 📊 CST Studio Suite Simülasyon Sonuçları

9 adet ayrık (discrete) port ile beslenen dizi, Zaman Alanı Çözücüsü (Transient Solver) ve doğruluğu artırmak adına **"Combine Results"** yöntemi kullanılarak analiz edilmiştir.

### 1. Empedans Uyumu (S-Parametreleri)
- **Broadside ve $12^{\circ}$ Tarama:** Karşılıklı kuplaj (mutual coupling) etkilerine rağmen, tüm portların rezonans eğrileri tam olarak 1 GHz üzerinde keskin düşüşler sergilemiş, yansıma katsayıları $-15 \text{ dB}$ ile $-43 \text{ dB}$ arasında mükemmel değerlere ulaşmıştır.
- **$38^{\circ}$ Büyük Açı Taraması:** Elemanlar arası faz adımları büyüdükçe yakın alan etkileşimleri artmış, rezonans vadilerinde hafif asimetriler oluşmuştur. Buna rağmen tüm portlar $-13 \text{ dB}$ ile $-36 \text{ dB}$ arasında kalarak endüstriyel kabul kriterlerinin altında kararlılık göstermiştir.

### 2. Uzak Alan (Farfield) Işıma Desenleri ve Yönelticilik (Directivity)
- **$\theta_{0} = 0^{\circ}$:** Maksimum yönelticilik $12.84 \text{ dBi}$ olarak elde edilmiştir. Yan lob seviyesi (SLL) $-13.0 \text{ dB}$ olarak ölçülmüştür.
- **$\theta_{0} = 12^{\circ}$:** Ana hüzme tam olarak $12.0^{\circ}$ açısına kilitlenmiş, yönelticilik $12.38 \text{ dBi}$ olarak korunmuştur. Meydana gelen $0.46 \text{ dB}$'lik azalma, tarama açısından kaynaklanan efektif alan daralması (**Scanning Loss**) ile uyumludur.
- **$\theta_{0} = 38^{\circ}$:** Hüzme başarıyla $38.0^{\circ}$ doğrultusuna bükülmüş, yönelticilik $11.37 \text{ dBi}$ olarak hesaplanmıştır. Dik eksenden uzaklaşıldığı için hüzme taban genişliği yayvanlaşmış ve $1.47 \text{ dB}$'lik bir Tarama Kaybı gözlemlenmiştir.

---

## 💻 MATLAB Analitik Dizi Faktörü Karşılaştırması

Dizi teorisindeki matematiksel modeli doğrulamak adına, MATLAB ortamında toplam hüzme örüntüsünü oluşturan **Dizi Faktörü (Array Factor - AF)** formülasyonu koşturulmuştur:

$$AF = \left| \frac{\sin(N\psi/2)}{N\sin(\psi/2)} \right|$$
$$\psi = k \cdot d \cdot \sin(\theta) + \beta$$

MATLAB'dan elde edilen normalize güç spektrum grafiklerinin, CST'den alınan 2D polar ve kartezyen uzak alan çıktılarıyla **sıfır hata ile örtüştüğü** görülmüştür. Bu durum, analitik hesaplamaların nümerik simülasyon başarısını kanıtlamaktadır.
