---
title: 'Inicio rápido: Base de conocimientos de actualización de Java: QnA Maker'
titleSuffix: Azure Cognitive Services
description: Procedimientos para actualizar una base de conocimiento en Java para QnA Maker.
services: cognitive-services
author: diberry
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: quickstart
ms.date: 09/12/2018
ms.author: diberry
ms.openlocfilehash: fc2792086d93e584535389c8c0f162fc1e592cbd
ms.sourcegitcommit: f20e43e436bfeafd333da75754cd32d405903b07
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2018
ms.locfileid: "49388252"
---
# <a name="update-a-knowledge-base-in-java"></a>Actualización de una base de conocimiento en Java

El siguiente código actualiza una base de conocimiento existente con el método [Actualizar](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600).

[!INCLUDE [Code is available in Azure-Samples Github repo](../../../../includes/cognitive-services-qnamaker-java-repo-note.md)]

Si aún no tiene una base de conocimiento, puede crear una de ejemplo para usar en esta guía de inicio rápido: [Creación de una nueva base de conocimiento](create-new-kb-java.md).

1. Cree un nuevo proyecto de Java en su IDE favorito.
1. Agregue el código que se proporciona a continuación.
1. Reemplace el valor `key` con una clave de suscripción válida.
1. Reemplace el valor `kb` con un identificador de base de conocimiento válido. Encuentre este valor acudiendo a una de las [bases de conocimiento de QnA Maker](https://www.qnamaker.ai/Home/MyServices). Seleccione la base de conocimiento que desea actualizar. Una vez en esa página, busque el valor de "kdid =" en la dirección URL como se muestra a continuación. Utilice su valor para el ejemplo de código.

    ![Identificador de base de conocimiento de QnA Maker](../media/qnamaker-quickstart-kb/qna-maker-id.png)

1. Necesitará la biblioteca [apache httpclient](https://hc.apache.org/downloads.cgi). Por ejemplo, descargue el binario HttpClient 4.x.x.tar.gz para encontrar todos los archivos jar que necesita para importar en el proyecto.
1. La biblioteca [GSON](https://github.com/google/gson) también es necesaria. Puede agregarla mediante la [creación](https://stackoverflow.com/questions/5258159/how-to-make-an-executable-jar-file) e importación manual del archivo .jar o la incorporación de una dependencia a la herramienta de administración de proyecto preferida, como Maven.
1. Ejecute el programa.

```java
import java.io.*;
import java.lang.reflect.Type;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/**
 * Gson: https://github.com/google/gson
 * Maven info:
 *    <dependency>
 *      <groupId>com.google.code.gson</groupId>
 *      <artifactId>gson</artifactId>
 *      <version>2.8.1</version>
 *    </dependency>
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import com.google.gson.reflect.TypeToken;

/**
 * Java does not natively support HTTP PATCH requests; Apache HttpClient is required.
 * HttpClient: https://hc.apache.org/downloads.cgi
 * Maven info:
 *    <dependency>
 *      <groupId>org.apache.httpcomponents</groupId>
 *      <artifactId>httpclient</artifactId>
 *      <version>4.5.5</version>
 *    </dependency>
 */
import org.apache.commons.logging.LogFactory;
import org.apache.http.client.methods.HttpPatch;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.entity.ByteArrayEntity;
import org.apache.http.Header;
import org.apache.http.HttpEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;

/**
 * NOTE: To compile and run this code:
 * 1. Save this file as UpdateKB.java.
 * 2. Run:
 * javac UpdateKB.java -cp .;gson-2.8.1.jar;httpclient-4.5.5.jar;httpcore-4.4.9.jar;
 * commons-logging-1.2.jar -encoding UTF-8
 * 3. Run:
 * java -cp .;gson-2.8.1.jar;httpclient-4.5.5.jar;httpcore-4.4.9.jar;commons-logging
 * -1.2.jar UpdateKB
 */

public class UpdateKB {

    // **********************************************
    // *** Update or verify the following values. ***
    // **********************************************

    // Replace this with a valid subscription key.
    static String subscriptionKey = "ADD KEY HERE";

    // Replace this with a valid knowledge base ID.
    static String kb = "ADD ID HERE";

    // Represents the various elements used to create HTTP request URIs
    // for QnA Maker operations.
    static String host = "https://westus.api.cognitive.microsoft.com";
    static String service = "/qnamaker/v4.0";
    static String method = "/knowledgebases/";

    // We'll serialize these classes into JSON for our request to the server.
    // For the JSON request schema, see: 
    // https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/
    // operations/5ac266295b4ccd1554da7600
    public static class Request {
        Add add;
        Delete delete;
        Update update;
    }

    public static class Add {
        Question[] qnaList;
        String[] urls;
        File[] files;
    }

    public static class Delete {
        Integer[] ids;
    }

    public static class Update {
        String name;
        Question[] qnaList;
        String[] urls;
        File[] files;
    }

    public static class Question {
        Integer id;
        String answer;
        String source;
        String[] questions;
        Metadata[] metadata;
    }

    public static class Metadata {
        String name;
        String value;
    }

    public static class File {
        String fileName;
        String fileUri;
    }

    // This class contains the headers and body of the HTTP response.
    public static class Response {
        Map<String, List<String>> Headers;
        String Response;

        /**
         * Headers and response (body) of the HTTP request
         * @param headers A map containing the requested response
         * @param response The body of the requested response
         */
        public Response(Map<String, List<String>> headers, String response) {
            this.Headers = headers;
            this.Response = response;
        }
    }

    /**
     * Formats and indents JSON for display.
     * @param json_text The raw JSON input
     * @return String A string containing formatted and indented JSON.
     */
    public static String PrettyPrint (String json_text) {
        JsonParser parser = new JsonParser();
        JsonElement json = parser.parse(json_text);
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

    /**
     * Sends a GET HTTP request.
     * @param url The string URL request
     * @return A Response object with the header and body of the response
     */
    public static Response Get (URL url) throws Exception {
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
        connection.setRequestMethod("GET");
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);
        connection.setDoOutput(true);

        StringBuilder response = new StringBuilder ();
        BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream(), "UTF-8"));

        String line;
        while ((line = in.readLine()) != null) {
            response.append(line);
        }
        in.close();

        return new Response (connection.getHeaderFields(), response.toString());
    }

   /**
     * Sends an HTTP PATCH request. We use Apache HttpClient, as HttpsURLConnection 
     * does not support PATCH.
     * @param url The string request
     * @param content The body of the request
     * @return Response Returns a Response object with the headers and body
     */
    public static Response Patch (URL url, String content) throws Exception {
        HttpPatch patch = new HttpPatch(url.toString());
        // HttpPatch implements HttpMessage, which includes addHeader.
        // See: <a href="https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/
        // apache/http/client/methods/HttpPatch.html">HttpPatch</a>
        // See: <a href="https://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/
        // HttpMessage.html">HttpMessage</a>
        patch.addHeader("Content-Type", "application/json");
        // Note: Adding the Content-Length header causes the exception:
        // "Content-Length header already present."
        patch.addHeader("Ocp-Apim-Subscription-Key", subscriptionKey);
        // HttpPatch implements HttpEntityEnclosingRequest, which includes setEntity.
        // See: <a href="https://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/
        // HttpEntityEnclosingRequest.html">HttpEntityEnclosingRequest</a>
        HttpEntity entity = new ByteArrayEntity(content.getBytes("UTF-8"));
        patch.setEntity(entity);

        CloseableHttpClient httpClient = HttpClients.createDefault();
        CloseableHttpResponse response = httpClient.execute(patch);

        // CloseableHttpResponse implements HttpMessage, which includes getAllHeaders.
        // See: <a href="https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/
        // client/methods/CloseableHttpResponse.html">CloseableHttpResponse</a>
        // Header implements NameValuePair.
        // See: <a href="https://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/Header.html">
        // Header</a>
        // See: <a href="https://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/
        // NameValuePair.html">NameValuePair</a>
        Map<String, List<String>> headers = new HashMap<String, List<String>>();
        for (Header header : response.getAllHeaders()) {
            List<String> list = new ArrayList<String>() {
                {
                    add(header.getValue());
                }
            };
            headers.put(header.getName(), list);
        }

        // CloseableHttpResponse implements HttpResponse, which includes getEntity.
        // See: <a href="https://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/
        // HttpResponse.html">HttpResponse</a>
        // HttpEntity implements getContent, which returns an InputStream.
        // See: <a href="https://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/org/apache/http/
        // HttpEntity.html">HttpEntity</a>
        StringBuilder output = new StringBuilder ();
        BufferedReader reader = new BufferedReader(new InputStreamReader(response.getEntity()
                                                                        .getContent(), "UTF-8"));
        String line;
        while ((line = reader.readLine()) != null) {
            output.append(line);
        }
        reader.close();

        return new Response (headers, output.toString());
    }

    /**
     * Sends the request to update the knowledge base.
     * @param kb The ID for the existing knowledge base
     * @param req The data source for the updated knowledge base
     * @return Reponse Returns the response from a PATCH request
     */
    public static Response UpdateKB (String kb, Request req) throws Exception {
        URL url = new URL(host + service + method + kb);
        System.out.println("Calling " + url.toString() + ".");
        String content = new Gson().toJson(req);
        return Patch(url, content);
    }

    /** 
     * Checks on the status of the request to update the knowledge base.
     * @param operation The QnA Maker operation to check
     * @return The Response object that represents the HTTP response
     */
    public static Response GetStatus (String operation) throws Exception {
        URL url = new URL(host + service + operation);
        System.out.println("Calling " + url.toString() + ".");
        return Get(url);
    }

    /**
     * Compiles the details of the request.
     * @return The Request object with request details.
     */
    public static Request GetRequest () {
        Request req = new Request ();

        Question q = new Question();
        q.id = 0;
        q.answer = "You can use our REST APIs to manage your Knowledge Base."
        + "See here for details: https://westus.dev.cognitive.microsoft.com/docs/services/"
        + "58994a073d9e04097c7ba6fe/operations/58994a073d9e041ad42d9baa";
        q.source = "Custom Editorial";
        q.questions = new String[]{"How do I programmatically update my Knowledge Base?"};

        Metadata md = new Metadata();
        md.name = "category";
        md.value = "api";
        q.metadata = new Metadata[]{md};

        req.add = new Add ();
        req.add.qnaList = new Question[]{q};
        req.add.urls = new String[]{"https://docs.microsoft.com/azure/cognitive-services"
        + "/qnamaker/faqs", "https://docs.microsoft.com/bot-framework/resources-bot-"
        + "framework-faq"};

        return req;
    }

    public static void main(String[] args) {
        try {
            // Send the request to update the knowledge base.
            Response response = UpdateKB(kb, GetRequest ());
            String operation = response.Headers.get("Location").get(0);
            System.out.println(PrettyPrint(response.Response));
            // Loop until the request is completed.
            Boolean done = false;
            while (true != done) {
                // Check on the status of the request.
                response = GetStatus (operation);
                System.out.println (PrettyPrint (response.Response));
                Type type = new TypeToken<Map<String, String>>(){}.getType();
                Map<String, String> fields = new Gson().fromJson(response.Response, type);
                String state = fields.get ("operationState");
                // If the request is still running, the server tells us how long to wait
                // before checking the status again.
                if (state.equals("Running") || state.equals("NotStarted")) {
                    String wait = response.Headers.get("Retry-After").get(0);
                    System.out.println("Waiting " + wait + " seconds...");
                    Thread.sleep(Integer.parseInt(wait) * 1000);
                }
                else {
                    done = true;
                }
            }
        }
        catch (Exception e) {
            System.out.println (e.getCause().getMessage());
        }
    }
}
```

## <a name="understand-what-qna-maker-returns"></a>Descripción de lo que devuelve QnA Maker

Se devuelve una respuesta correcta en JSON, como se muestra en el ejemplo a continuación. Los resultados pueden ser ligeramente diferentes. Si la llamada final devuelve un estado "Correcto", la base de conocimiento se ha actualizado correctamente. Para solucionar problemas, consulte a los códigos de respuesta de [Update Knowledgebase](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) (Actualización de base de conocimiento) de la API QnA Maker.

```json
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:48Z",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
...
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-04-13T01:49:48Z",
  "lastActionTimestamp": "2018-04-13T01:49:50Z",
  "resourceLocation": "/knowledgebases/140a46f3-b248-4f1b-9349-614bfd6e5563",
  "userId": "2280ef5917bb4ebfa1aae41fb1cebb4a",
  "operationId": "5156f64e-e31d-4638-ad7c-a2bdd7f41658"
}
Press any key to continue.
```

Una vez actualizada la base de conocimiento, puede verla en el portal de QnA Maker en la página [My knowledge bases](https://www.qnamaker.ai/Home/MyServices) (Mis bases de conocimiento). Tenga en cuenta que la base de conocimiento ha cambiado de acuerdo a su solicitud personalizada.

Para modificar otros elementos de la base de conocimiento, consulte el [esquema JSON](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da7600) de QnA Maker y modifique el objeto `req` en el método `getRequest()`.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Referencia de QnA Maker (V4) REST API](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)