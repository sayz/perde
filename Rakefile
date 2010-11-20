# İzin verilen resim boyutları
SIZES = [800, 600]
THEME = '_themes/default'

# Slaytları resim gömerek üret.
rule '.html' => ['.md', *FileList["#{THEME}/**/**"]] do |f|
  sh "landslide -t #{THEME} #{f.source} -i -d #{f.name}"
end

desc "Resimleri boyutlandır ve optimize et"
task :optim do
  pngs, jpgs = FileList["**/*.png"], FileList["**/*.jpg", "**/*.jpeg"]

  # Optimize edilmişleri çıkar.
  [pngs, jpgs].each do |a|
    a.reject! { |f| %x{identify -format '%c' #{f}} =~ /[Rr]aked/ }
  end

  # Boyut düzeltmesi yap.
  (pngs + jpgs).each do |f|
    w, h = %x{identify -format '%[fx:w] %[fx:h]' #{f}}.split.map { |e| e.to_i }
    size, i = [w, h].each_with_index.max
    if size > SIZES[i]
      arg = (i > 0 ? 'x' : '') + SIZES[i].to_s
      sh "mogrify -resize #{arg} #{f}"
    end
  end
  pngs.each do |f|
    system "pngnq -f -e .png-nq #{f}"
    out = "#{f}-nq"
    if File.exist?(out)
      $?.success? ? File.rename(out, f) : File.delete(out)
    end
  end
  jpgs.each { |f| sh "jpegoptim -q -m80 #{f}" }

  # Optimize edilmiş resimlerin kullanıldığı slaytları, bu resimler slayta
  # gömülü olabileceğinden tekrar üretelim.  Nasıl?  Aşağıdaki berbat
  # numarayla.  Resim'e ilşik bir referans varsa dosyaya dokun.
  (pngs + jpgs).each do |f|
    # İşlendiğini belirtmek için not düş.
    sh "mogrify -comment 'raked' #{f}"

    name = File.basename f
    FileList["*/*.md"].each do |src|
      system "grep -q '(.*#{name})' #{src} && touch #{src}"
    end
  end
end

desc "Değişen slaytları üret"
task :default => [:optim,
  # sadece alt dizinlerdeki markdown dosyalar
  *FileList["*/*.md"].map { |f| f.sub(/[.]md$/, '.html') }
]
