---
layout: post
title: BEM, BEMIT ve VueJS
tags: [frontpage, blog, bulutuzer, bem, bemit, vuejs]
image: "/images/posts/post-2.jpg"
---

VueJS projelerinde ölçeklenebilir bir yapı kurmak her developer için olmazsa olmazdır. VueJS tarafında geliştirme yaptığım projeler için iletilen UI bileşenlerde, bu durum çoğu zaman göz ardı ediliyor. İşte BEMIT bu noktada devreye giriyor. Tabii bunun için bir çok farklı metodoloji var fakat benim tercihim BEMIT’den yana.

# BEM Nedir

CSS’de bir çok metodoloji vardır. Ve bunlardan biri geliştirme ortamımıza BEM isminde dahil oldu. BEM (Block Element Modifier) çok basit mantık ile stil adlandırma kuralı. Hepimizin bildiği gibi bir sınıf isimlendirmesi yaparken bunun için çok fazla düşünebiliyoruz ve bunu daha iyi hale getirmek bir yana dursun, bir standart altında da yapmamız gerekiyor. BEM işte burada devreye girdi.

Örnek bir card örneği ile block element modifier metodolojisini anlamaya çalışalım.

### Block

Bir card hazırlarken ana kapsayıcı için ".card" isimlendirmesini kullanırız. Card sınıfı burada bizim block yapımızı oluşturuyor. Ve hepimizin bildiği gibi block yapıları bir çok öğeyi barındırırlar.

### Elements

Card block içerisinde barınan öğeler aslında bizim için elementleri oluşturuyor. Ve elementleri BEM'de "**" ile tanımlıyoruz. Örneğin ".card**aside", ".card**figure" ya da ".card**image" gibi öğeler bizim elementlerimizi oluşturmaktadır.

### Modifier

Peki tanımladığımız block ve elementler için ek stil tanımlamaları yaptığımızı düşünelim. Bunlar ise BEM de modifiers anlamına geliyor. Örneğin ".card**image--radius" ya da ".card**image--large" gibi ek stil tanımlamaları bizim modifiers yapımızı oluşturmaktadır.

# BEMIT

Peki, BEM variken BEMIT’e neden ihtiyaç duyuyoruz? Aslında bunun için önce ITCSS açıklamam daha doğru olacaktır. ITCSS bir metodolojidir ve Harry Roberts tarafından yapılmıştır.

İşte BEMIT ise kısaca BEM + ITCSS’dir ve BEMIT, BEM’in yaratıcısı Harry Roberts’ın kendisinden geldi. Yani BEMIT sadece ITCSS hiyerarşisini, BEM’e eklemekten ibaretti. Yukarıdaki BEM örneğindeki gibi geliştiriciler sınıfları birbiriyle ilişkilendiriyorlar.

Şimdi BEMIT, BEM gibi, projelerimizde sınıfları tanımlamak için bir adlandırma yöntemi ama prefix ile kullanıyoruz. Bu da bize bir sınıfın tam olarak ne tür işler yapabileceğini, onu nasıl kullanacağımızı ve tanımlı kuralları nerede bulacağımızı belirlememizi sağlıyor.

## BEMIT Prefiksler

Dedik ki block her zaman bir kapsayıcıdır ve içinde bir çok öğe bulundurmaktadır. Ayrıca bir block aynı zamanda kendi başına bir bileşendir "component". Card örneği ile birlikte kullanırsak aşağıdaki yapıyı oluşturuyoruz.

**c-** prefix ile card sıfını bir bileşen haline getirdim ve bu sayede yapacağım değişiklikler sadece bu bileşeni etkileyecek. Ayrıca bu yol ile bileşenin hangi katmanda ve hazırlanan hiyerarşide hangi dosyada olduğunu bulmamızı da kolaylaştırıyor.

```html
<article class="c-card">
  <div class="c-card__header">
    <figure class="c-card__figure c-card__figure--rounded">
      <img
        src="https://satyr.io/400x200?text=card__image"
        alt=""
        class="c-card__image c-card__image--large"
      />
    </figure>
  </div>
</article>
```

**o-** prefix bir object "nesne" tanımlarken kullanılmaktadır. Bu sınıflar, projede yeniden kullanılabilir sınıflardır. Bir nesnenin uygulamamızın birkaç yerinde kullanılabileceği ve belirli bir bağlamdan yoksun olabileceği anlamına gelir. Dolayısıyla hepimizin bildiği gibi bunları değiştirmek risklidir. Yani, -o prefix sayesinde, nesnenin kurallarını değiştireceksek, uygulamamızın birkaç bölümünün etkilenebileceğini bileceğiz. Kulağa ne kadar iyi geliyor değil mi? Ayrıca nesne örneğini responsive suffixes "sonekler" ile kullandım.

```html
<article class="c-card">
  <div class="c-card__body o-media__body@md">
    <h2 class="c-card__title o-media__titley@md"></h2>
  </div>
</article>
```

**u-** prefix ise bizim yardımcı araçlarımızdır. Block, elements ve modifiers ile ilgisi yoktur. Aslında bu araçlar daha çok "!important" sahip genel sınıfları kapsıyorlar.

```html
<article class="c-card">
  <div class="c-card__body u-block u-none@sm">
    <h2 class="c-card__title u-hiden@sm"></h2>
  </div>
</article>
```

### Responsive Suffixes

Aslında örneklerde kullandığım soneklerin tek bir işlevi var. "@" koşullu durumları daha okunabilir ve mantıklı kılmasıdır. Developer için utilities "araçların" ve objects de olası permütasyonları veya görünümleri daha kolay bulmasını, öğrenmesini sağlar.

Kısaca BEM, BEM + ITCSS için bize sağladığı faydalar bunlar. Peki VueJS ile ilgisi ne? VueJS de components, utilities, objects gibi bir hiyerarşimiz oluyor. Bir layout structure oluşturduğumuzda bu bizim için sadece VueJS de değil aslında CSS dosya hiyerarşisinde de fayda sağlamaktadır. Uzun bir zaman önce BEM ve VueJS için bir örnek hazırlamıştım. İşte bu örneği BEMIT ile hazırladığımızı düşünelim. Çok basit bir buton bileşeninde bile props ile ne kadar işimize yarayacağını az çok ön görebiliyoruz değil mi?

[BEM + VueJS ile Basic Navbar Component](https://github.com/bulutuzer/vue-bem-navbar-component)

### Kaynaklar

[ITCSS: Scalable and Maintainable CSS Architecture](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/)

[BEMIT: Taking the BEM Naming Convention a Step Further](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/)

[BEM Cheet Sheet](https://bem-cheat-sheet.9elements.com/)
