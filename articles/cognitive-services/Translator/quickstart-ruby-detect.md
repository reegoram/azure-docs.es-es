---
title: 'Guía de inicio rápido: Identificación del idioma del texto - Translator Text, Ruby'
titleSuffix: Azure Cognitive Services
description: En esta guía de inicio rápido se identifica el idioma del texto de origen mediante Translator Text API con Ruby.
services: cognitive-services
author: noellelacharite
manager: cgronlun
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/22/2018
ms.author: nolachar
ms.openlocfilehash: e2b138b5c28047487da2ca7a72169a10a125eaf5
ms.sourcegitcommit: f10653b10c2ad745f446b54a31664b7d9f9253fe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2018
ms.locfileid: "46121710"
---
# <a name="quickstart-identify-language-from-text-with-ruby"></a>Guía de inicio rápido: identificación del idioma del texto con Ruby

En esta guía de inicio rápido se identifica el idioma del texto de origen mediante Translator Text API.

## <a name="prerequisites"></a>Requisitos previos

Se requiere [Ruby 2.4](https://www.ruby-lang.org/en/downloads/) o una versión posterior para ejecutar el código.

Para usar Translator Text API, también necesita una clave de suscripción; consulte [Cómo suscribirse a Translator Text API](translator-text-how-to-signup.md).

## <a name="detect-request"></a>Solicitud Detect

El siguiente código identifica el idioma del texto de origen mediante el método [Detect](./reference/v3-0-detect.md).

1. Cree un nuevo proyecto de Ruby en el editor de código que prefiera.
2. Agregue el código que se proporciona a continuación.
3. Reemplace el valor `key` por una clave de acceso válida para la suscripción.
4. Ejecute el programa.

```ruby
require 'net/https'
require 'uri'
require 'cgi'
require 'json'
require 'securerandom'

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the key string value with your valid subscription key.
key = 'ENTER KEY HERE'

host = 'https://api.cognitive.microsofttranslator.com'
path = '/detect?api-version=3.0'

uri = URI (host + path)

text = 'Salve, mondo!'

content = '[{"Text" : "' + text + '"}]'

request = Net::HTTP::Post.new(uri)
request['Content-type'] = 'application/json'
request['Content-length'] = content.length
request['Ocp-Apim-Subscription-Key'] = key
request['X-ClientTraceId'] = SecureRandom.uuid
request.body = content

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request (request)
end

result = response.body.force_encoding("utf-8")

json = JSON.pretty_generate(JSON.parse(result))
puts json
```

## <a name="detect-response"></a>Respuesta de Detect

Se devuelve una respuesta correcta en JSON, tal como se muestra en el siguiente ejemplo:

```json
[
  {
    "language": "it",
    "score": 1.0,
    "isTranslationSupported": true,
    "isTransliterationSupported": false,
    "alternatives": [
      {
        "language": "pt",
        "score": 1.0,
        "isTranslationSupported": true,
        "isTransliterationSupported": false
      },
      {
        "language": "en",
        "score": 1.0,
        "isTranslationSupported": true,
        "isTransliterationSupported": false
      }
    ]
  }
]
```

## <a name="next-steps"></a>Pasos siguientes

Explore el código de ejemplo de esta guía de inicio rápido y otros, incluida la traducción y la transliteración, así como otros proyectos de Translator Text de ejemplo de GitHub.

> [!div class="nextstepaction"]
> [Explorar ejemplos de Ruby en GitHub](https://aka.ms/TranslatorGitHub?type=&language=ruby)
