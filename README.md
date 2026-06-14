# CST Studio Suite ve MATLAB ile Elektronik Hüzme Taramalı Doğrusal Anten Dizisi Tasarımı

Bu proje; [cite_start]1 GHz merkez frekansında çalışan, yarı dalga boyu ($d = \lambda/2$) kriterine göre konumlandırılmış 9 elemanlı doğrusal bir dipol anten dizisinin elektromanyetik modellenmesi, analitik analizi ve elektronik hüzme yönlendirme (beamsteering) süreçlerini içermektedir[cite: 2207, 2208, 2212, 2213]. 

Proje kapsamında, ana hüzme odağı broadside ($0^{\circ}$) durumunun yanı sıra analitik olarak hesaplanan faz kaymalarıyla $12^{\circ}$ ve $38^{\circ}$ hedef açılarına başarıyla yönlendirilmiş; [cite_start]CST simülasyon sonuçları ile MATLAB analitik modelleri üst üste bindirilerek doğrulanmıştır[cite: 2207, 2228, 2229, 2231, 2233, 2239].

---

## 🛠️ Tasarım ve Anten Geometrisi Parametreleri

- [cite_start]**Merkez Frekansı ($f_{0}$):** 1.0 GHz [cite: 2212]
- [cite_start]**Serbest Uzay Dalga Boyu ($\lambda$):** 300 mm [cite: 2213]
- [cite_start]**Dizi Elemanı:** Yarım Dalga Dipol Anten (Half-Wave Dipole) [cite: 2209]
- [cite_start]**Optimize Edilmiş Dipol Boyu ($L_{dipol}$):** Uç etkilerini (fringing fields) sönümlemek adına $141 \text{ mm} \ (0.47\lambda)$ olarak ayarlanmıştır[cite: 2210, 2214].
- [cite_start]**Elemanlar Arası Mesafe ($d$):** $150 \text{ mm} \ (0.5\lambda)$ [cite: 2213]
- [cite_start]**Giriş Empedansı:** 73 $\Omega$ [cite: 2216]

---

## 📐 Teorik Altyapı ve Faz Hesaplamaları

[cite_start]Doğrusal anten dizisinde ana hüzmeyi uzayda belirli bir $\theta_{0}$ açısına elektronik olarak yönlendirebilmek için ardışık elemanlar arasına uygulanması gereken sabit faz farkı ($\beta$), **Doğrusal Dizi Tarama Denklemi** ile hesaplanır[cite: 2220]:

[cite_start]$$\beta = -k \cdot d \cdot \sin(\theta_{0})$$ [cite: 2224]

[cite_start]$k = \frac{2\pi}{\lambda}$ ve $d = \frac{\lambda}{2}$ değerleri yerine konulduğunda denklem derece cinsinden şu basitleştirilmiş hale gelir[cite: 2223, 2225, 2226]:

[cite_start]$$\beta = -180^{\circ} \cdot \sin(\theta_{0})$$ [cite: 2227]

### Target Faz Kaymaları ve Port Konfigürasyonları:
- [cite_start]**Durum 1: Broadside ($\theta_{0} = 0^{\circ}$) ➡️** $\beta = 0^{\circ}$ (Tüm portlar eş fazlı) [cite: 2229, 2230]
- [cite_start]**Durum 2: 1. Doğrultu ($\theta_{0} = 12^{\circ}$) ➡️** $\beta = -37.42^{\circ}$ [cite: 2231]
- [cite_start]**Durum 3: 2. Doğrultu ($\theta_{0} = 38^{\circ}$) ➡️** $\beta = -110.82^{\circ}$ [cite: 2233]

---

## 📊 CST Studio Suite Simülasyon Sonuçları

[cite_start]9 adet ayrık (discrete) port ile beslenen dizi, Zaman Alanı Çözücüsü (Transient Solver) ve doğruluğu artırmak adına **"Combine Results"** yöntemi kullanılarak analiz edilmiştir[cite: 2236, 2237].

### 1. Empedans Uyumu (S-Parametreleri)
- [cite_start]**Broadside ve $12^{\circ}$ Tarama:** Karşılıklı kuplaj (mutual coupling) etkilerine rağmen, tüm portların rezonans eğrileri tam olarak 1 GHz üzerinde keskin düşüşler sergilemiş, yansıma katsayıları $-15 \text{ dB}$ ile $-43 \text{ dB}$ arasında mükemmel değerlere ulaşmıştır[cite: 2241, 2242, 2243, 2244].
- [cite_start]**$38^{\circ}$ Büyük Açı Taraması:** Elemanlar arası faz adımları büyüdükçe yakın alan etkileşimleri artmış, rezonans vadilerinde hafif asimetriler oluşmuştur[cite: 2228, 2429, 2430, 2431]. [cite_start]Buna rağmen tüm portlar $-13 \text{ dB}$ ile $-36 \text{ dB}$ arasında kalarak endüstriyel kabul kriterlerinin altında kararlılık göstermiştir[cite: 2432, 2433, 2434].

### 2. Uzak Alan (Farfield) Işıma Desenleri ve Yönelticilik (Directivity)
- [cite_start]**$\theta_{0} = 0^{\circ}$:** Maksimum yönelticilik $12.84 \text{ dBi}$ olarak elde edilmiştir[cite: 2252, 2331]. [cite_start]Yan lob seviyesi (SLL) $-13.0 \text{ dB}$ olarak ölçülmüştür[cite: 2331].
- [cite_start]**$\theta_{0} = 12^{\circ}$:** Ana hüzme tam olarak $12.0^{\circ}$ açısına kilitlenmiş, yönelticilik $12.38 \text{ dBi}$ olarak korunmuştur[cite: 2335, 2386]. [cite_start]Meydana gelen $0.46 \text{ dB}$'lik azalma, tarama açısından kaynaklanan efektif alan daralması (**Scanning Loss**) ile uyumludur[cite: 2335].
- [cite_start]**$\theta_{0} = 38^{\circ}$:** Hüzme başarıyla $38.0^{\circ}$ doğrultusuna bükülmüş, yönelticilik $11.37 \text{ dBi}$ olarak hesaplanmıştır[cite: 2467, 2470, 2486]. [cite_start]Dik eksenden uzaklaşıldığı için hüzme taban genişliği yayvanlaşmış ve $1.47 \text{ dB}$'lik bir Tarama Kaybı gözlemlenmiştir[cite: 2469, 2470].

-
