---
layout: post
title:  "Algoritmalar (Kitap Özet vs)"
date:   2015-06-29 17:32:40
image: /assets/book.jpg
categories: jekyll update
---
<img src="{{ page.image }}" /><p>
[Kitap İncele][link]


Programlama öğrenmek isteyenlerin okuması ve hazmetmesi gereken bir kitaptan bahsedelim. Hatta başucu kitabıdır kendisi. İçinde teorik anlamda uygulamaya dökebileceğiniz, işin biraz daha metamatiğine
inebileceğiniz bilgiler mevcut. Ben kitaptan öğrendiklerimi ara ara yazmak istiyorum. 

`Sıralama Algoritmaları` ile başlayalım:

Algoritma kurarken sıralama fonksiyonunun kullanılmasıyla bu işlem üzerinde kafa yormuşlar ve hesaplama karmaşıklıklarını hesaba katarak en verimli yolu bulmaya çalışmışlar. Şimdi bu yollar üzerinden bir de biz gidelim.

1 - Yerleştirmeli Sıralama ( Insertion Sort)

Örneğin elimizde 10 sayıdan oluşan bir dizi olsun ve biz bu sayıları sıralayalım. Nasıl bir yöntem izlerdiniz? Beynimizdeki düşüncenin algoritmasını kurarak bunu bir dil sayesinde programlamamız gerekiyor.
sayilar = (3, 4, 1, 8, 2, 0, 9, 44, 22, 5, )

Şimdi Insert-Sort tekniğini uygulayarak bu sayıları sıralayalım.
Ben python kullanarak çözeceğim.

{% highlight ruby %}

numbers = [3, 4, 1, 8, 2, 0, 9, 44, 22, 5]
for i in range(1, len(numbers)):
	j = i
	while j>0:
		if numbers[j]< numbers[j-1]:
			numbers[j], numbers[j-1] = numbers[j-1], numbers[j]
		j = j - 1

print numbers

{% endhighlight %}
Burada yapılan şu, sırayla gitmek ve sürekli geri dönüp, bulunduğumuz bölüme kadar olan yeri düzenlemek. Program çalışmaya başladığı zaman hangi sıradaysak o sıraya kadar ilerliyor ve ileriye gitmiyor. 
Dizinin ikinci elemanından başlayarak kayıtlar sırayla kontrol edilir. Bir önceki kayıt o anki kayıttan büyükse bu iki elemanın yerleri değiştirilir ve dizide geriye doğru ilerlenir. Bu işleme seçilen dizi elemanından küçük kayıt kalmayıncaya kadar devam edilir.
Ayrıca bununla ilgili çok güzel hazırlanmış bir dans videosu var, [şuradan][link1] izleyebilirsiniz.

2 - Seçmeli Sıralama (Selection Sort):
Dizideki ilk elemandan başlanılır, seçilen dizi elemanıyla bu elemandan sonra gelen dizi elemanları karşılaştırılır, en küçük dizi elemanı bulunup seçilen dizi elemanıyla yer değiştirilir. Bu işlem sonucunda dizinin en küçük elemanı belirlenerek dizinin başına yazılmış olur.

{% highlight ruby %}
numbers = [3, 4, 1, 8, 2, 0, 9, 44, 22, 5]
for i in range(len(numbers)):
	min = numbers[i]
	for j in range(i+1, len(numbers)):
		if numbers[j] < min:
			min = numbers[j]
			numbers[j],numbers[i]=numbers[i],numbers[j]
	numbers[i] = min

print numbers
{% endhighlight %}
Bununla ilgili videoya [şuradan][link2] ulaşabilirsiniz.

3 - Kabarcık Sıralaması (Bubble Sort)
Kabarcık sıralaması olarak adlandırılmasının sebebi dizi içindeki büyük elemanların algoritmanın her adımında dizi sonuna doğru lineer olarak ilerlemesidir. Dizinin başından başlanarak dizi elemanları 
sırayla seçilir, seçilen dizi elemanı kendinden sonra gelen elemandan büyükse yerleri değiştirilir. Bu işlem sonunda dizinin en büyük elemanı dizi sonuna yerleştirildiğinden bir sonraki işlemde arama sınırı 
bir eleman geri çekilir.

{% highlight ruby %}
for i in range(len(numbers)):
	j = 0
	while j < len(numbers)-1:
		if numbers[j] > numbers[j+1]:
			numbers[j], numbers[j+1] = numbers[j+1], numbers[j]
		j= j + 1
print numbers
{% endhighlight %}

Bubble Sort videosunu [şuradan][link3] izleyebilirsniz.

4 - Hızlı Sıralama (Quick Sort)
Bu yaklaşım "parçala ve çözümle" ilkesine göre çalışmaktadır. Öncelikle sıralanacak diziden parçalayıcı görevini üstlenen bir pivot seçilir. Bu işlemin ardından seçilen elemanın solundaki
elemanlarla sağındaki elemanların yeri değiştirilerek parçalayıcı elemanın solundakilerden büyük, sağındakilerden ise küçük olması sağlanır.
Çözümü recursive(özyinelemeli) şekilde yapacağız.

{% highlight ruby %}
def quicksort(arr):
    if not arr:
        return []

    pivots = [x for x in arr if x == arr[0]]
    lesser = quicksort([x for x in arr if x < arr[0]])
    greater = quicksort([x for x in arr if x > arr[0]])

    return [lesser] + pivots + [greater]
{% endhighlight %}    
Quick Sort videosu [burada][link4]

Şimdi de özel sayıları inceleyelim ve bunları bulmak için gereken koda bakalım.

<h3>Özel Sayılar</h3>

1 - Arkadaş Sayılar
Sayının kendisi hariç diğer bölenlerine `gerçek bölenler` denir. Örnek olarak 220 ve 284 verilmiş. 
220 Bölenleri = 1 + 2 + 4 + 5 + 10 + 11 + 20 + 22 + 44 + 55 + 110 = 284 
284 Bölenleri =  1 + 2 + 4 + 71 + 142 = 220

Peki bize kafadan 2 sayı verildiği zaman biz bunların arkadaş olup olmadığını nerden bileceğiz? Tabi ki kod yazarak. Deneyelim.

{% highlight ruby %}
top1 = 0
top2 = 0
numb = int(raw_input("1.sayi"))
numb2 = int(raw_input("2.sayi"))

for i in range(1, numb/2+1):
	if numb%i == 0:
		top1 = top1 + i

for i in range(1, numb2/2+1):
	if numb2%i == 0:
		top2 = top2 + i

if top1 == numb2 and top2 == numb:
	print "arkadas sayilar"
else:
	print "arkadas degiller"
{% endhighlight %} 

Armstrong Sayılar
Bir sayının basamak sayısı ile sayıların kuvvetleri alınıp toplandığı zaman sayının kendisi çıkıyorsa bu sayı armstrong sayı oluyor. Örneğin
{% highlight ruby %}
153 = 1^3 + 5^3 + 3^3
{% endhighlight %}


{% highlight ruby %}
def find(numb):
	top = 0
	for i in str(numb):
		top = top + pow(int(i), len(str(numb)))
	return top

for i in range(1000):
	if i == find(i):
		print i

{% endhighlight %} 

Özel sayıları anlatırken asal sayıları atlamak olmaz. Asal sayıları bulan ya da verilen bir sayının asal olup olmadığını bulan koda bakalım:
Öncelikle asal sayıyı kendi yöntemimizle bulurken şunu biliyoruz, 1'den ve kendisinden başka sayıya bölünemeyen sayılar asal sayıdır. Düşündüğümüz şeyi düz bir şekilde performans kaygısı duymadan koda dökersek 
şöyle bir şey çıkıyor:

{% highlight ruby %}
def list():
	for i in range(3, 1000):
		asal = True
		for j in range(2, i):
			if i % j == 0:
				asal = False
		if asal == True:
			print i

list()
{% endhighlight %} 
Burda yapılan işlem şudur: 3'ten başlayarak 1000'e kadar olan her sayı kendisinden küçük olan sayılara bölünmeye çalışılır. Eğer sayı 1 kere tam bölünmüşse asal olmadığı anlaşılır. Burada göze çarpan 
şey: Çift sayıların asal olmadığını biliyoruz. Ama 3'ten 1000'e kadar olan sayıları denerken arada çift sayılar da var ve onları boş yere kontrol ediyoruz. İkinci algoritmada çift sayıları kontrol etmeyi bırakıyoruz.
{% highlight ruby %}
def list():
	for i in range(3, 1000, 2):
		asal = True
		for j in range(2, i):
			if i % j == 0:
				asal = False
		if asal == True:
			print i

list()
{% endhighlight %} 
Burda göze çarpan diğer nokta şu oluyor: Burada i sayısı diyelim ki 20 olsun ve for j in range(2, 20) derken aslında i'yi bölmeye çalıştığımız son sayı 10 olmalıdır çünkü 10'dan sonra 11, 12, 13 .. bu sayılara zaten bölünemeyeceğini biliyoruz. Bir de tek sayıları aldığımız için tek sayıların çift sayılara bölünemeyeceğini biliyoruz. Artık bölen kısmını da tek sayılardan oluşturmaya başlıyoruz. Kodumuzun o bölümünü düzeltelim : 

{% highlight ruby %}
def list():
	for i in range(3, 1000, 2):
		asal = True
		for j in range(3, (i/2)+1, 2):
			if i % j == 0:
				asal = False
		if asal == True:
			print i

list()
{% endhighlight %} 

En son olarak da bir sayının kendi kareköküne kadar olan sayılarla bölünüp bölünmediğini kontrol etmenin yeterli olduğunu anlıyoruz. 3. adıma bakarsanız sayıyı numb%2 sayısına kadar bölmeye çalışmıştık. Örneğin 3. adımda 20 sayısını 11'e kadar bölerken şimdi 20'nin kareköküne yakın olan 5 sayısına kadar bölmemizin yeterli olduğunu anlıyoruz.
Kodumuza ekleme yapalım:

{% highlight ruby %}
def list():
	for i in range(3, 10, 2):
		asal = True
		for j in range(2, int((i**0.5)+1)):
			if i % j == 0:
				asal = False
		if asal == True:
			print i
list()
{% endhighlight %} 

[link]: http://www.idefix.com/kitap/algoritmalar-vasif-vagifoglu-nabiyev/tanim.asp?sid=AYU2EB7PR6D92OP4GRBN
[link1]: https://www.youtube.com/watch?v=ROalU379l3U
[link2]: https://www.youtube.com/watch?v=Ns4TPTC8whw
[link3]:https://www.youtube.com/watch?v=lyZQPjUT5B4
[link4]:https://www.youtube.com/watch?v=ywWBy6J5gz8