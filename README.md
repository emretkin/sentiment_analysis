# sentiment_analysis

PROJE RAPORU: TÜRKÇE METİNLERDE DUYGU ANALİZİ (3 SINIFLI LSTM MODELİ)

1. Proje Konusu
Projede sosyal medya, alışveriş siteleri, ve Wikipedia gibi çeşitli alanlardan toplanılan etiketli metinleri içeren veriseti kullanılmış ve bunların pozitif, negatif ve nötr olarak 3 farklı duygu haline göre sınıflandırılması için LSTM modeli eğitilmiş ve sonuçlar gözlemlenmiştir.
Sosyal medya verileri, müşteri memnuniyeti ve toplumsal eğilimleri anlamak için en zengin kaynaktır. Türkçe, eklemeli yapısı ve devrik cümle kullanımı nedeniyle NLP (Doğal Dil İşleme) alanında çalışılması zor ancak değerli bir dildir.
İşletmeler için marka algısını ölçmek, siyasi analizler yapmak veya kullanıcıların bir ürün hakkındaki "gerçek" görüşlerini (Pozitif/Negatif/Nötr) saniyeler içinde binlerce tweet üzerinden analiz etmek stratejik karar alma mekanizmalarını güçlendirir.
Geçmişte bu alanda Naive Bayes ve SVM (Support Vector Machines) gibi geleneksel yöntemler kullanılmış olsa da, günümüzde kelimeler arasındaki bağlamı koruyan Derin Öğrenme modelleri (LSTM, BERT) standart hale gelmiştir.

2. Veri Setinin Belirlenmesi
Projede "Turkish Sentiment Analysis Dataset” veri seti kullanılmıştır.
Veri seti, Twitter, Wikipedia ve çeşitli alışveriş siteleri üzerinden toplanmış, manuel olarak etiketlenmiş toplam 492.782 cümleden oluşmaktadır.
Veri seti, kullanıcı metinleri ve bu metinlere karşılık gelen duygu etiketlerinden (Positive, Negative, Notr) oluşmaktadır. Eğitim ve Test setleri, %90 ve %10 olarak önceden ayrılmıştır.

3. Yöntem ve Algoritma Seçimi 
Naive Bayes/SVM: Kelime sırasını ve aradaki bağlamı önemsemezler. "Hızlı değil ama güzel" cümlesindeki "değil" kelimesinin neyi nitelediğini anlamakta zorlanırlar.
RNN: Kısa süreli bellek sorunu yaşarlar.
LSTM (Long Short-Term Memory): Projede kullanılan algoritmadır. LSTM, "Unutma Kapısı" (Forget Gate) mekanizması sayesinde cümle içindeki uzun mesafeli kelime ilişkilerini hatırlar. Türkçe gibi cümlenin sonundaki ekin veya fiilin anlamı tamamen değiştirebildiği dillerde LSTM çok daha yüksek doğruluk sunar.



4. Model Eğitimi ve Değerlendirme
Ön İşleme (Preprocessing): Verisetindeki metinlere öncelikle ön işleme adımları uygulanmıştır.  Bunun için metinlerde büyük/küçük harf dönüşümü yapılmış, noktalama işaretleri, kullanıcı adları (@user) ve linkler temizlenerek modelin sadece "anlama" odaklanması sağlanmıştır.

Model Mimarisi:
Embedding Katmanı: 15,000 kelimelik hazne ile kelimeler vektörleştirilmiştir.
LSTM Katmanı: 128 birimlik LSTM ile bağlamsal öğrenme gerçekleştirilmiştir.
Softmax Output: 3 sınıfa ait olasılık dağılımı için kullanılmıştır.

Performans: Model, 3 epoch sonunda yaklaşık %94.88 Accuracy (Doğruluk) seviyesine ulaşmıştır. Test verilerinde de %93.88 Accuracy değeri elde etmiştir. Modelin eğitim sürecinde, doğrulama kaybı (val_loss) değerinin 3. epoch sonunda minimum seviyeye ulaştığı gözlemlenmiştir. Modelin ezberleme (Overfitting) durumunu engelleyerek genelleme yeteneğini sağlamak için eğitim bu noktada sonlandırılmıştır.

