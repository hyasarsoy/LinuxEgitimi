# TechCorp Geliştirme Ortamı

TechCorp, geliştirme iş akışları için `devtool` adında özel bir script kullanmaktadır. Bu aracın sistemde her yerden erişilebilir olması gerekmektedir. Ayrıca, ekip tarafından kullanılan belirli bir yapılandırma dosyasının bir ortam değişkeni aracılığıyla referans edilmesi gerekmektedir.

## Görevler

1. Ana dizininizde `techcorp_tools` adında bir dizin oluşturun.
2. `techcorp_tools` dizininde `devtool` adında basit bir bash script oluşturun ve bu script çalıştırıldığında "TechCorp DevTool v1.0" yazdırmasını sağlayın.
3. `devtool` scriptini çalıştırılabilir hale getirin.
4. `techcorp_tools` dizinini PATH'inize ekleyin, böylece `devtool` komutu herhangi bir yerden çalıştırılabilir olsun. Bu değişikliği mevcut oturuma hemen uygulayın.
5. Ana dizininizde `techcorp_config.json` adında bir dosya oluşturun ve içerisine `{"env": "development"}` yazın.
6. `techcorp_config.json` dosyasının tam yolunu gösteren `TECHCORP_CONFIG` adında bir ortam değişkeni oluşturun.
7. `TECHCORP_CONFIG` ortam değişkeninin yeni tüm terminal oturumlarında kullanılabilir olduğundan emin olun.

### İpuçları

- Ortam değişkenleri tanımlarken `export` kullanmayı unutmayın.
- Scripti çalıştırılabilir yapmak için `chmod` komutunu kullanmayı unutmayın.
- Yolları ayarlarken `$HOME` veya `~` ifadesini ana dizininize referans vermek için kullanabilirsiniz.

## Örnek

Bu görevleri tamamladıktan sonra aşağıdaki komutları herhangi bir dizinden çalıştırabilmelisiniz:

```bash
$ devtool
TechCorp DevTool v1.0

$ echo $TECHCORP_CONFIG
/home/user/techcorp_config.json
```
```

Bu adımları tamamladıktan sonra `devtool` komutunu her yerden çalıştırabilirsiniz ve `TECHCORP_CONFIG` ortam değişkenini görebilirsiniz.