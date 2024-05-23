---
title: "SVG'ler"
---

### Giriş

SVG'ler web üzerinde yaygın bir görüntü formatıdır. İlk başta biraz kafa karıştırıcı olabilir, ancak nasıl kullanılacağını bildikten sonra, web siteniz için yüksek kaliteli, dinamik görüntüler oluşturmak için son derece güçlü bir araçtır.

Bu derste SVG'lerin tam olarak ne olduğunu, ne için kullanıldığını ve web sitelerinize nasıl gömebileceğinizi öğreneceğiz.

### Derse genel bakış

Bu bölüm, bu derste öğreneceğiniz konuların genel bir özetini içerir.

- SVG'ler, Vektör Grafikleri ve XML nedir?
- Basit SVG'ler nasıl oluşturulur ve web sitenize nasıl eklenir?
- SVG'ler ne zaman kullanılmalı ve ne zaman farklı bir görüntü formatı kullanmak daha uygun olacaktır?

### SVG'ler nedir?

SVG'ler, boyutları kolayca *ölçeklenebilen* bir görüntü formatıdır, bu da onların kalitesini artırmadan herhangi bir boyuta kolayca ölçeklenebileceği anlamına gelir. Ayrıca, CSS ve JavaScript aracılığıyla özelliklerini değiştirebileceğiniz için programatik olarak görüntüler oluşturmanız veya değiştirmeniz gerekiyorsa çok kullanışlıdır.

SVG'ler genellikle şu amaçlar için kullanılır:

1. İkonlar
1. Grafikler/Çizelgeler
1. Büyük, basit görüntüler
1. Desenli arka planlar
1. Diğer öğelere SVG filtreleri aracılığıyla efektler uygulama

### Tamam, ama bunlar nedir?


"SVG", "Scalable Vector Graphics(Ölçeklenebilen Vektör Grafikleri)" kelimelerinin kısaltmasıdır. Vektör grafikleri, görüntünüzün bir piksel ızgarasıyla tanımlandığı geleneksel “raster grafiklerinin” aksine, basitçe matematikle tanımlanan görüntülerdir. Raster grafiklerde ayrıntılar bu piksel ızgarasının boyutuyla sınırlıdır. Görüntünün boyutunu artırmak (*ölçeklendirmek*) istiyorsanız, bu ızgaranın boyutunu artırmanız gerekir. Tüm bu yeni piksellerin neye benzemesi gerektiğine nasıl karar verirsiniz? Bunun basit bir çözümü yok. Ayrıca, ızgara ne kadar büyük olursa, dosya boyutunuz da o kadar büyür.

Öte yandan, vektör grafiklerinde bir ızgara bulunmaz. Bunun yerine, farklı şekil ve çizgiler için matematiksel formüller vardır. Bu formüller sadece matematiksel ifadeler olduğu için, bunları istediğiniz büyüklükte veya küçüklükte kullanabilirsiniz. Bu durum, kalite veya dosya boyutu üzerinde herhangi bir etki yapmaz.

SVGs'ın başka ilginç bir yönü daha vardır: XML kullanılarak tanımlanırlar. XML(Extensible Markup Language olarak da bilinir), bir HTML benzeri sözdizimidir ve [API's](https://en.wikipedia.org/wiki/API)'den [RSS](https://en.wikipedia.org/wiki/RSS)'e, [spreadsheet and word editor software](https://en.wikipedia.org/wiki/Office_Open_XML) kadar birçok alanda kullanılır.

SVG kaynak kodunun XML olması birkaç önemli avantaja sahiptir.

İlk olarak, bu, *insan tarafından okunabilir(human-readable)* olduğu anlamına gelir. Eğer bir JPEG dosyasını bir metin düzenleyicide açarsanız, anlamsız karakterlerle dolu bir şey göreceksiniz. Ancak bir SVG dosyasını açarsanız, şöyle bir şey göreceksiniz:

```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">
    <rect x=0 y=0 width=100 height=50 />
    <circle class="svg-circle" cx="50" cy="50" r="10"/>
</svg>
```

Hâlâ kafa karıştırıcı olabilir, ama işte orada kelimeler var! Etiketler! Nitelikler! JPEG gibi [binary file formats](https://en.wikipedia.org/wiki/Binary_file) ile karşılaştırıldığında, kesinlikle tanıdık bir alandayız.

İkinci avantajı ise XML'in HTML ile etkileşimli olacak şekilde tasarlanmış olmasıdır. Bu, yukarıdaki kodu herhangi bir değişiklik yapmadan doğrudan bir HTML dosyasına yerleştirebileceğiniz ve görüntünün görüntülenmesi gerektiği anlamına gelir. Ve çünkü bunlar HTML öğeleri gibi DOM'da öğe haline gelebilir, CSS ile hedef alabilir ve zaten kullandığınız [Element WebAPI](https://developer.mozilla.org/en-US/docs/Web/API/Element) ile oluşturabilirsiniz!

### Dezavantajları

Öyleyse, açıkça SVG'ler harika! Şimdi tüm görüntülerimizi SVG'ye dönüştürmeye mi gidiyoruz? Peki, tam olarak değil. SVG'ler, nispeten basit görüntüler için *harika* olsa da, görüntünün her ayrıntısının XML olarak yazılması gerektiği için karmaşık görüntülerin depolanması konusunda son derece verimsizdir. Eğer görüntünüz fotoğraf gerçekçiliğinde olmalı veya ince detaya veya dokuya sahip olmalıysa ("[grunge textures](https://unsplash.com/s/photos/grunge-texture)" harika bir örnek), o zaman SVG'ler iş için yanlış araçtır.

### SVG'nin anatomisi

Genellikle, SVG'leri kodunuzda sıfırdan oluşturmak istemeyeceksiniz. Çoğunlukla, dosyayı bir web sitesinden veya SVG oluşturabilen bir görüntü editöründen kopyalarsınız (Adobe Illustrator ve Figma, SVG oluşturabilen bunun için iki popüler uygulamadır). Ancak, genellikle bir SVG'yi indirirken biraz düzenleme veya ayarlama yapmak isteyebilirsiniz, bu nedenle tüm parçaların ne olduğunu ve nasıl çalıştığını bilmek oldukça faydalıdır.

<p class="codepen" data-height="300" data-theme-id="dark" data-default-tab="css,result" data-slug-hash="NWaGdmL" data-editable="true" data-user="TheOdinProjectExamples" style={{"height":"300px","boxSizing":"border-box","display":"flex","alignItems":"center","justifyContent":"center","border":"2px solid","margin":"1em 0","padding":"1em"}}>
<span><a href="https://codepen.io">CodePen</a>'deki TheOdinProject(<a href="https://codepen.io/TheOdinProjectExamples">@TheOdinProjectExamples</a>) tarafından yapılmış olan <a href="https://codepen.io/TheOdinProjectExamples/pen/NWaGdmL">Basit SVG Örneğine</a>bakınız</span>

</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. `xmlns` - "XML NameSpace" kısaltmasıdır. Bu, kullandığınız XML dilinin hangi *lehçe* olduğunu belirtir. Bizim durumumuzda, bu lehçe SVG dil spesifikasyonudur. Bu olmadan, bazı tarayıcılar görüntünüzü render etmeyebilir veya yanlış render edebilir. 
1. `viewBox` - SVG'nizin sınırlarını tanımlar. SVG'nizdeki öğelerin farklı noktalarının konumlarını tanımlamanız gerektiğinde, bu değerlere başvurulan yer burasıdır. Ayrıca, SVG'nin en/boy oranını *ve* orijinini de tanımlar. Yani oldukça önemli bir rolü vardır! Şekiller üzerindeki etkilerini anlamak için yukarıdaki örnekte farklı değerlerle oynamayı deneyin.
1. `class`, `id` - Bu özellikler HTML'deki gibi çalışır. Bunları SVG'lerde kullanmak, bir öğeyi CSS veya JavaScript ile kolayca hedeflemenize veya bir öğeyi [`use` element](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/use) ile yeniden kullanmanıza olanak tanır.
1.`<circle>`, `<rect>`, `<path>`, ve `<text>` gibi öğeler SVG ad alanı tarafından tanımlanır. Bunlar temel yapı taşlarımızdır. SVG ile son derece karmaşık görüntüler oluşturabilirsiniz, ancak bunlar genellikle sadece bir düzine veya daha az sayıda temel öğe kullanılarak oluşturulur. SVG öğelerinin tam listesini [burada](https://developer.mozilla.org/en-US/docs/Web/SVG/Element) görebilirsiniz.
1. Birçok SVG özelliği, örneğin `fill` ve `stroke` CSS dosyanızda değiştirilebilir. [SVG özellikleri ve CSS hakkında bu makaleye göz atın](https://css-tricks.com/svg-properties-and-css/).

Yukarıdaki kodla oynayın ve neler olduğunu anlamaya çalışın. viewBox boyutlarını değiştirdiğinizde veya bir öğenin niteliklerini değiştirdiğinizde neler olur?

### SVG'leri Gömmek

SVG'yi belgenize nasıl yerleştireceğinizi kararlaştırırken iki temel yaklaşım vardır: bağlantılı ve satır içi(inline).

SVG'leri bağlamak, temelde diğer herhangi bir görüntüyü bağlamak gibi çalışır. `<img>` gibi bir HTML görüntü öğesi kullanabilir veya CSS'nizde `background-image: url(./my-image.svg)` kullanarak bağlantı kurabilirsiniz. Hâlâ doğru bir şekilde ölçeklenirler, ancak SVG içeriği web sayfasından erişilemez.

Alternatif olarak, SVG'lerinize görüntü olarak bağlantı vermek yerine, içeriklerini doğrudan web sayfanızın koduna yapıştırarak SVG'lerinizi satır içi yapmaktır. Yine doğru şekilde oluşturulacaktır, ancak SVG'nin özellikleri kodunuz tarafından görülebilecek ve bu da görüntüyü CSS veya JavaScript aracılığıyla dinamik olarak değiştirme imkanı sağlayacaktır.

SVG'leri satır içine almak tüm potansiyellerini ortaya çıkarmanızı sağlar, ancak bazı ciddi dezavantajları da vardır: kodunuzun okunmasını zorlaştırır, sayfanızı daha az önbelleğe alınabilir hale getirir ve büyük bir SVG ise HTML'nizin geri kalanının yüklenmesini geciktirebilir.

React gibi bir ön yüz JavaScript kütüphanesi veya webpack gibi bir derleme aracı öğrendiğinizde SVG kodunu satır içine almanın bazı dezavantajlarından kaçınılabilir. Henüz bu konulara girmeye hazır değiliz, bu yüzden bunu aklınızın bir köşesinde tutun.

Şu anda, kullanım durumunuza en iyi uyanı yapın. Bağlamak genellikle daha temiz ve daha basittir, bu nedenle HTML'nizle birlikte SVG kodunu ayarlamaya ihtiyacınız yoksa bunu tercih edin.

### Bilgi ölçme

Aşağıdaki sorular, bu dersteki temel konular üzerinde tekrar düşünmek için bir fırsattır. Bir soruyu yanıtlayamazsanız, materyali gözden geçirmek için üzerine tıklayın, ancak bu bilgiyi ezberlemenizin veya ustalaşmanızın beklenmediğini unutmayın.

-  [What is the `xmlns` attribute?](#svgnin-anatomisi)
-  [What are some situations where you *wouldn't* want to use SVG?](#dezavantajları)
-  [What are the benefits of "inlining" your SVGs? What are the drawbacks?](#svgleri-gömmek)

### Ek kaynaklar

Bu alanda içerikle alakalı faydalı linkler bulunmaktadır. Zorunlu değildir, ek olarak düşünülmelidir.

- SVG ikonları için birçok ücretsiz kütüphaneler vardır. Göz atmaya değer olanlar: [Material icons](https://fonts.google.com/icons), [Feather icons](https://feathericons.com/)

- Kendi SVG'lerinizi oluşturmaya veya SVG'leri düzenlemeye başlamak istiyorsanız, [Yann Armelin'in SVG editörü](https://yqnn.github.io/svg-path-editor) gibi bir tür görsel düzenleyiciye ihtiyacınız olacaktır. Daha basit SVG'lerle uğraşmak için harikadır ancak karmaşık grafikler için tasarlanmamıştır.
    