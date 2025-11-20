# 📱 NeuroLens User Flow (Kullanıcı Akışı)

**Teknik Yaklaşım:** React tabanlı "Wizard" (Sihirbaz) form yapısı.  
**Mantık:** Her adım bir önceki adımın tamamlanmasıyla ilerler (Step-by-step progressive disclosure).

---

## 1. Sayfa: Karşılama & Vizyon (Splash Screen)
*Markanın ilk izlenimi ve değer önerisi.*

* **Görsel:** Ortada NeuroLens logosu (Büyük, modern bir göz veya beyin ikonu).
* **Başlık:** `NeuroLens`
* **Alt Başlık:** "Her Beyin Farklı Öğrenir."
* **Aksiyon (Button):** `Yolculuğa Başla`
* **Amaç:** Marka vizyonunu satmak ve "Eğitimde Eşitlik" vurgusu yapmak.

---

## 2. Sayfa: Tanışma (Identity)
*Kullanıcı ile duygusal bağ kurma aşaması.*

* **AI Mesajı:** "Merhaba! Ben senin kişisel öğrenme asistanınım. Sana nasıl hitap etmemi istersin?"
* **Input:** İsim girme alanı (Placeholder: "Adın nedir?").
* **Aksiyon (Button):** `Devam Et`
* **Psikolojik Etki:** Kullanıcıya ismiyle hitap etmek (Personalization), uygulamanın "soğuk bir bot" olmadığını, bir asistan olduğunu hissettirir.

---

## 3. Sayfa: Seviye Belirleme (Context)
*LLM (GPT-4o) Prompt ayarı için seviye tespiti.*

* **AI Mesajı:** "Memnun oldum **[Kullanıcı Adı]**! 🚀 Şu an eğitim seviyen veya yaş grubun nedir?"
* **Seçenekler (Büyük Seçim Kartları):**
    * 🎒 **İlkokul (7-10 Yaş)** -> *Çıktı: Çok basit, analojik (Örn: Mitokondri = Enerji Fabrikası).*
    * 🏫 **Ortaokul/Lise (11-17 Yaş)** -> *Çıktı: Orta seviye, ders kitabı formatı.*
    * 🎓 **Üniversite/Akademik** -> *Çıktı: Akademik, terminolojik dil.*
    * 💼 **Yetişkin/Profesyonel** -> *Çıktı: İş odaklı, net ve kısa.*
* **Amaç:** AI'nın yanıt üretirken kullanacağı "tone of voice" ve karmaşıklık seviyesini belirlemek.

---

## 4. Sayfa: Hedef Belirleme (Goal)
*Kullanıcının o anki niyetini (Intent) anlama.*

* **AI Mesajı:** "Bugün sana nasıl destek olmamı istersin?"
* **Seçenekler:**
    1.  📝 **Sınava Hazırlanıyorum** -> *Format: Madde madde, hap bilgiler, flashcard stili.*
    2.  📚 **Konuyu Anlamaya Çalışıyorum** -> *Format: Hikayeleştirme, detaylı anlatım.*
    3.  🌍 **Dil Öğreniyorum** -> *Format: Çeviri destekli, kelime açıklamalı.*
    4.  ⚡ **Sadece Göz Atıyorum** -> *Format: Hızlı özet (TL;DR).*
* **Amaç:** Çıktının formatını kullanıcının ihtiyacına göre optimize etmek.

---

## 5. Sayfa: Süper Güç Seçimi (Mode Selection)
*Erişilebilirlik ve kişiselleştirilmiş UI ayarları.*

* **AI Mesajı:** "Öğrenirken seni en çok ne zorluyor? Senin için sayfayı sihirli bir şekilde değiştireceğim."
* **Izgara Menü (Grid Layout):**
    * 🧠 **Odaklanamıyorum (DEHB Modu)** -> *UI: Dikkat dağıtıcı unsurlar gizlenir, metinler kısa paragraflara bölünür.*
    * 📖 **Harfler Karışıyor (Disleksi Modu)** -> *UI: OpenDyslexic fontu aktifleşir, harf aralıkları artar.*
    * 👶 **Çok Karmaşık Geliyor (Basitleştirme)** -> *Prompt: "Explain like I'm 5" modu.*
    * 🌉 **Yabancı Dil Sorunu (Dil Köprüsü)** -> *UI: Orijinal metin ve çeviri yan yana.*
    * 👁️ **Görmekte Zorlanıyorum (Yüksek Kontrast)** -> *UI: Siyah arka plan, sarı/beyaz büyük fontlar.*
* **Amaç:** Kullanıcının engelini tespit edip ona uygun **CSS** ve **System Prompt** ayarını seçmek.

---

## 6. Sayfa: Materyal Yükleme (Input)
*Sihrin başladığı nokta.*

* **Başlık:** "Harika! **[Seçilen Mod]** modunu senin için hazırladım."
* **Alt Başlık:** "Şimdi bana zorlandığın sayfayı göster."
* **Aksiyonlar:**
    * 📷 **Fotoğraf Çek** (Kamera API tetiklenir)
    * 📂 **Galeriden Yükle** (File Picker açılır)
* **Sonuç:** Yükleme yapıldığı an "Sihirli Dönüşüm" (Loading Skeleton) ekranı gelir ve sonuç sayfası (Render) açılır.

---

## 🛠 Akış Diyagramı (Mermaid)

```mermaid
graph TD
    A[Splash Screen] -->|Yolculuğa Başla| B[Identity: İsim Girişi]
    B -->|İsim Alındı| C[Context: Seviye Seçimi]
    C -->|Prompt Seviyesi Ayarlandı| D[Goal: Hedef Belirleme]
    D -->|Çıktı Formatı Belirlendi| E[Mode: Süper Güç Seçimi]
    E -->|CSS & Prompt Modu Ayarlandı| F[Input: Fotoğraf/Dosya Yükle]
    F -->|API Request| G[Loading: Sihirli Dönüşüm]
    G --> H[Result: Özelleştirilmiş Öğrenme Ekranı]
