# Mikroservis Altyapı Servisleri

Bu repository, mikroservis mimarisinde kullanılan ortak altyapı servislerini içeren Docker Compose yapılandırmasını barındırmaktadır.

## Servisler

### Redis
- **Port**: 6379
- **Kullanım Amacı**: In-memory cache olarak kullanılmaktadır.
- **Özellikler**: Persistence için AOF (Append-Only File) aktif edilmiştir.

### RabbitMQ
- **Port**: 5672 (AMQP)
- **Management Port**: 15672
- **Kullanım Amacı**: Servisler arası asenkron iletişim için message broker olarak kullanılmaktadır.
- **Management UI**: http://localhost:15672
- **Default Kullanıcı**: guest/guest

### Elasticsearch
- **Port**: 9200
- **Kullanım Amacı**: Dağıtık ürün arama motoru olarak kullanılmaktadır.
- **Özellikler**: 
  - Single-node yapılandırması
  - X-Pack security devre dışı
  - JVM Heap size: 512MB

### Kibana
- **Port**: 5601
- **Kullanım Amacı**: Elasticsearch verilerini görselleştirme ve yönetim arayüzü
- **URL**: http://localhost:5601

## Kurulum

1. Repository'yi klonlayın
2. `.env.example` dosyasını `.env` olarak kopyalayın
3. `.env` dosyasındaki port değerlerini ihtiyacınıza göre düzenleyin
4. Aşağıdaki komutu çalıştırın:

```bash
docker-compose up -d
```

## Network

Tüm servisler `shared_network` adlı bir bridge network üzerinde çalışmaktadır. Bu sayede:
- Servisler birbirleriyle container isimleri, portlar üzerinden iletişim kurabilir
- İzole bir network ortamı sağlanır
- Diğer mikroservisler bu network'e bağlanarak altyapı servislerine erişebilir

## Notlar

- Tüm servisler `restart: always` politikası ile yapılandırılmıştır
- Elasticsearch için memory limitleri yapılandırılmıştır
- Servis portları `.env` dosyası üzerinden özelleştirilebilir
