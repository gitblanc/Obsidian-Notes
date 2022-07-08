Shodan es un motor de búsqueda que escanea distintos tipos de recursos publicados en internet. Se puede encontrar en:

```
https://www.shodan.io
```

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1714/#filtros)Filtros

Existen distintos tipos de filtros para poder hacer búsquedas más detalladas:

**_city:_** busca dispositivos filtrando por la ciudad.

**_country:_** dispositivos de un país en particular.

**_geo:_** se le pueden pasar coordenadas y el radio máximo a su alrededor.

**_hostname:_** busca valores que coincidan con el hostname indicado.

**_net:_** búsqueda basada en una IP o /x CIDR.

**_os:_** filtrado por sistema operativo.

**_port:_** busca puertos abiertos en particular.

**_before/after:_** búsqueda de resultado en un intervalo de tiempo.

#### [](https://openwebinars.net/academia/aprende/ethical-hacking-introduccion/1714/#api-script)API Script

Será necesaria una API Key para las requests que se obtendrá con el registro. Se pueden utilizar distintos lenguajes de programación para usarla. A continuación se expone un ejemplo de uso de esta API escrito en Python:

```
import os
import sys
import shodan

SHODAN_API_KEY = "your_API_key_here"

api = shodan.Shodan(SHODAN_API_KEY)
searchItem = sys.argv[1]

try:
    # Search Shodan
    results = api.search(searchItem)

    # Show the results
    print 'results found: %s' % results['total']
    for result in results['matches']:
        print 'IP: %s' % result['ip_str']
        print result['data']
        print ''

except shodan.APIError, e:
    print 'Error: %s' % e
```