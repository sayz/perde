# Ve Perde!

.notes: Animasyon makineyi yoruyorsa "`.fx: plain`" ile kapatın.

Recai Oktaş `<roktas@bil.omu.edu.tr>`

[http://roktas.me/](http://roktas.me/)

Kasım 2010

---

# Perde?

Etkinliklerde yapılan sunumlar ve bu sunumların bulunduğu dizini anlatan bir
terim.

- Sunum bir "eser" türüdür; kod, kitap, günlük, makale, kısa teknik notlar
  gibi
- "Yazmak" değerlidir, "kodlamak" gibi; zaman, emek, tasarım, özen gerektirir
- Eserleri belirli bir programa bağlı "ikili" biçimlere emanet etmiyoruz
- Mümkün her yerde açık standartları, özelde "düz metin"i tercih ediyoruz
- Diğerlerinde olduğu gibi sunumlar için de
  [Markdown](http://daringfireball.net/projects/markdown/) kullanıyoruz

Şimdilik [Landslide](https://github.com/adamzap/landslide) yazılımını
kullanıyoruz

- Python ile yazılan açık kaynak bir komut satırı aracı
- Düz yazılarda [Jekyll](http://jekyllrb.com/), sunumlarda Landslide

---

# Kur

.notes: Liste maddelerinde kod yazacaksınız en az 8 boşluk içeriden başlayın.

- Gerekli (ve önerilen) paketleri kurun

        sudo apt-get install \
            rake imagemagick jpegoptim pngnq chromium-browser \
            python-jinja2 python-markdown python-docutils python-pygments
        wget --no-check-certificate \
            https://github.com/downloads/19/tepsi/landslide_0.0_all.deb
        sudo dpkg -i landslide_0.0_all.deb

- Önerilen paketleri kurun (bu aşamada hata oluşmuşsa göz ardı edin)

        sudo apt-get install ttf-bitstream-vera ttf-liberation ttf-ubuntu-title 

----

# Hazırla

- GitHub hesabınızda `tepsi` adında bir depo açın.

        mkdir tepsi && cd tepsi
        git init
        git remote add origin git@github.com:<kullanıcı>/tepsi.git
        git symbolic-ref HEAD refs/heads/gh-pages
        rm -f .git/index && git clean -fdx
        git push origin gh-pages

- 19 `tepsi` deposundan ilkleme yapın

        git remote add upstream git://github.com/19/tepsi.git
        git pull upstream/master
        git push origin master

---

# Başla

Deponuzda sunum konusuna uygun bir dizin ve bu dizinde (tercihen) dizinle aynı
isimde "`.md`" uzantılı bir açın.  Örneğin "Debian Kurulumu" konulu bir sunum
için:

    mkdir debian-kur
    cd debian-kur
    $EDITOR debian-kur.md

Tutarlılık için aşağıda konvansiyonlara lütfen uyun:

- Dizin ve sunum isimleri aynı olmalı
- Sunum konusundan yararlanarak anahtar kelimeler oluşturun
- Bu anahtar kelimeleri "`-`" ile birleştirin
- Büyük harf yok, hepsi küçük harf olmalı
- Türkçe karakter kullanabilirsiniz, fakat boşluk karakteri kullanmayın

---

# Düzenle

Gayet basit!  [Markdown](http://daringfireball.net/projects/markdown/)
sözdizimini kullanıyorsunuz.

- Slaytlar "`---`" ile ayrılıyor
- Slaytta birinci seviye bir başlık slayt başlığı oluyor
- İlk slayt bir "kapak", sunum başlığını girin, kendinizi tanıtın
- Kod renklendirmesi için ilk satırda "`!`**dil**" ile dili tanıtıyorsunuz
- Daha fazla bilgi için [Landslide](https://github.com/adamzap/landslide)

**Bu sunumun kaynağını inceleyin.  `s` tuşuna basarak kaynak linkini
görebilirsiniz.**

---

# Üret

Düzenlemeniz tamamlandığında slayt dosyasını üretmek için aşağıdaki komutu
çalıştırın:

    rake

İlgili sunum dizininde sunumla aynı isimde "`.html`" uzantılı bir dosya
oluşacaktır.  Sunumu izlemek için:

    chromium-browser debian-kur/debian-kur.html &

**Dikkat!  `rake` komutu sadece değiştirdiğiniz slaytı değil, eğer varsa
depoda tekrar üretilmesi gereken tüm slaytları da üretir.**

---

# Oynat

**Sunumu tam ekran yapmak için "`F11`" tuşuna basın**

- Ok tuşlarıyla ileri-geri veya boşluk tuşuyla sadece ileri
- "`Esc`" tuşuna basarak tüm slaytları görebilir, birini seçebilir veya tekrar
  aynı tuşa basarak geri dönebilirsiniz
- "`t`" "içindekiler" listesi
- "`n`" slayt numaralarını göster/gizle
- "`2`" slayt notlarını göster/gizle
- "`3`" 3d efekti
- "`h`" yardım

---

# Dikkat!

.fx: dikkat

**Sunum için WebKit tabanlı bir tarayıcıyı, örneğin Chromium'u tavsiye
ediyoruz!**

- Firefox da (ön sayfa canlandırması dışında) problemsiz çalışır.
- IE'yi unutun.

Bu slayt da örneklendiği gibi önemli noktalara değindiğiniz slaytlarda
`dikkat` makrosunu kullanabilirsiniz!

Fakat çok sık yapılması halinde dinleyiciden beklediğiniz dikkati
alamayabilirsiniz.  Hangi durumlarda "dikkat" çekmelisiniz?

- Bir uygulama anı geldiğinde
- "Sunumu 3 slayta indirmen gerekseydi hangilerini seçerdin?"e cevap olacak
  slaytlarda

---

# Sergile

Sunumlarınızın bir GitHub deposunda olduğunu varsayıyoruz.  O halde aynı
noktadan bunları web üzerinden sunabilirsiniz.

- Jekyll tabanlı GitHub sayfalarından farklı olarak bu sunumlar sunucu
  tarafında oluşturulamıyor

- Yukarıdaki komutlarla sunumu siz oluşturuyorsunuz

- Sunumu tamamladığınızda ilgili dosyaları depoya eklemeniz yeterli

        git add debian-kur
        git commit -m "yeni sunum: debian-kur"
        git push

- **Ön sayfada (`index.html`) sunuma bir bağlantı vermeyi unutmayın!**

---

# Sergile

.fx: dikkat

**Dikkat!  Sunum dosyalarının depoda `gh-pages` dalında olması gerekiyor.**

Aksi halde web sayfası üretilmeyecektir.

---

# Bölümle

Slaytta bölümler kullanabilirsiniz.  Deneyelim...

## Alt Bölüm 1

Integer in dignissim ipsum. Integer pretium nulla at elit facilisis eu feugiat
velit consectetur.

## Alt Bölüm 2

Donec risus tortor, dictum sollicitudin ornare eu, egestas at purus. Cras
consequat lacus vitae lectus faucibus et molestie nisl gravida. Donec tempor,
tortor in varius vestibulum, mi odio laoreet magna, in hendrerit nibh neque eu
eros.

---

# [Elvis](http://www.youtube.com/watch?v=7e3inLcUbjg)

.notes: Andy Warhol'un bu resmi özgün haliyle 1173x1174 2.391 MB idi.  Ön işlemeden sonra 599x600 297 KB'a indi.

![Elvis](media/elvis.png)

---

# Resim

.fx: dikkat

Lütfen sunumda kullandığınız resimleri ilgili sunum dizininde "`media`" alt
dizininde tutun ve resim adresini de buna uygun verin.  Örneğin "`debian-kur`"
isimli sunumda kullanılan "`swirl.png`" isimli bir resim için:

- resmi "`debian-kur/media/swirl.png`" olarak saklayın.

- "`debian-kur/debian-kur.md`" dosyasında resim adresini şu şekilde verin:

        ![girdap](media/swirl.png)

---

# Ara Başlık

---

Başlıksız bir slayt da olabilir.

---

# Sunum Notları

.notes: Bu bir not

Slayt notları alabilirsiniz.  Notları görmek (veya kapatmak) için "`2`" tuşuna
basın.

---

# Kod

Bir kod bloğu:

    !python
    while True:
        print "Herşey çok güzel olacak"

Bir başka kod bloğu:

    !php
    <?php exec('python render.py --help'); ?>

Başka:

    !xml
    <?xml version="1.0" encoding="UTF-8"?>
    <painting>
      <img src="madonna.jpg" alt='Foligno Madonna, by Raphael'/>
      <caption>This is Raphael's "Foligno" Madonna, painted in
        <date>1511</date>–<date>1512</date>.
      </caption>

---

# Gist

GitHub'a yapıştırdığınız kod parçalarını (gist) sunumda kullanabilirsiniz.
İlgili gist sayfasında "Embed" butonuna basarak elde ettiğiniz JavaScript
kodunu slayta ekleyin.

<script src="https://gist.github.com/643575.js?file=.irbrc"></script>

**Dikkat!**  Gist bağlantısı eklemişseniz sunum sırasında ağ bağlantısına
ihtiyacınız olacak.  Gist kullanılması sunumun çok yavaş yüklenmesine neden
olabilir.

---

# Uzun Kod?

Aşağıda bir slayta sığmayan uzun bir kod var.  Kodun tamamını görmek için
yandaki kaydırma çubuğunu veya yukarı/aşağı ok tuşlarını kullanın.

    !c
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    static void
    dohelp(void)
    {
    	fprintf(stderr, "imdaaaaaaaaat\n");
    }
    
    static void
    doexit(void)
    {
    	fprintf(stderr, "çıkıyorum\n");
    	exit(EXIT_SUCCESS);
    }
    
    static struct command_t {
    	const char *name;
    	void (*action)(void);
    } commands[] = {
    	{ "help", dohelp, },
    	{ "exit", doexit, },
    	{ NULL, NULL,     },
    };
    
    int
    main(void)
    {
    	(*commands[1].action)();
    	return 0;
    }
