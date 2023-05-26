## Настройка событий электронной торговли для Facebook Pixel
### Размещение кода пикселя на всех страницах сайта
#### Head
```
<script>
  !function(f,b,e,v,n,t,s)
  {if(f.fbq)return;n=f.fbq=function(){n.callMethod?
  n.callMethod.apply(n,arguments):n.queue.push(arguments)};
  if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
  n.queue=[];t=b.createElement(e);t.async=!0;
  t.src=v;s=b.getElementsByTagName(e)[0];
  s.parentNode.insertBefore(t,s)}(window, document,'script',
  'https://connect.facebook.net/en_US/fbevents.js');
  fbq('init', 'TRACKER_NUMBER');
  fbq('track', 'PageView');
</script>
```
#### Body
```
<noscript><img height="1" style="display:none"
  src="https://www.facebook.com/tr?id=TRACKER_NUMBER&ev=PageView&noscript=1"
/></noscript>
```
**TRACKER_NUMBER** - идентификатор пикселя

### События просмотра товара (ViewContent)
Необходимо на всех страницах товара разместить следующий код:
```
<script>
  fbq('track', 'ViewContent', {
    value: {{ Цена товара, переменная – число }}, 
    currency: '{{ Код валюты, переменная - строка (RUB, USD, EUR ...) }}',
    content_ids: '{{ ID товара }},',
    content_type: 'product',
  });
</script>
```
### Событие добавления товара в корзину (AddToCart)
При добавлении товара в корзину (клик на кнопку), необходимо выполнение следующего кода
```
<script>
  fbq('track', 'AddToCart', {
    value: {{ Цена товара, переменная – число }}, 
    currency: '{{ Код валюты, переменная - строка (RUB, USD, EUR ...) }}',
    content_ids: '{{ ID товара }},',
    content_type: 'product',
  });
</script>
```
### Событие заказа (Purchase)
Код ниже необходимо выполнить после успешного заказа товара (попадание на страницу успешного заказа, клик на кнопке "оформить заказ")
```
<script>
  fbq('track', 'Purchase', {
    value: {{ Цена товара, переменная – число }}, 
    currency: '{{ Код валюты, переменная - строка (RUB, USD, EUR ...) }}',
    contents: [ // Массив товаров
        {
            id: '{{ Идентификатор товара, переменная - строка }}',
            quantity: {{ Количество заказанного товара, переменная - число}},
            price: {{ Цена товара, переменная - число }},
            content_category: '{{ Категория товара, переменная - строка (опционально) }}'
        },
        {
            id: '{{ Идентификатор товара, переменная - строка }}',
            price: {{ Цена товара, переменная - число }},
            quantity: {{ Количество заказанного товара, переменная - число}},
            content_category: '{{ Категория товара, переменная - строка (опционально) }}'
        },
        ...
    ],
    content_type: 'product',
  });
</script>
```
