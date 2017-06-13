---
title: Solucionar problemas comuns com JSON no SQL Server | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, FAQ
ms.assetid: feae120b-55cc-4601-a811-278ef1c551f9
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 94435e9fb466887a00c8d22076f229481a83f280
ms.contentlocale: pt-br
ms.lasthandoff: 06/09/2017

---
# <a name="solve-common-issues-with-json-in-sql-server"></a>Solucionar problemas comuns com JSON no SQL Server
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Encontre respostas para perguntas comuns sobre o suporte interno a JSON no SQL Server.  
 
## <a name="for-json-and-json-output"></a>Saída de FOR JSON e JSON

### <a name="for-json-path-or-for-json-auto"></a>FOR JSON PATH ou FOR JSON AUTO?  
 **Pergunta.** Quero criar um resultado de texto JSON de uma consulta SQL simples em uma única tabela. FOR JSON PATH e FOR JSON AUTO produzem a mesma saída. Qual dessas duas opções deve usar?  
  
 **Resposta.** Use FOR JSON PATH. Embora não haja nenhuma diferença na saída JSON, o modo AUTO se aplica a lógica adicional que verifica se as colunas devem ser aninhadas. Considere a opção padrão PATH.  

### <a name="create-a-nested-json-structure"></a>Criar uma estrutura aninhada de JSON  
 **Pergunta.** Quero produzir JSON complexo com várias matrizes no mesmo nível. FOR JSON PATH pode criar objetos aninhados usando caminhos e FOR JSON AUTO cria o nível de aninhamento para cada tabela. Nem uma destas duas opções me permite gerar a saída desejada. Como posso criar um formato JSON personalizado que as opções existentes não suportam diretamente?  
  
 **Resposta.** Você pode criar qualquer estrutura de dados Adicionando consultas FOR JSON como expressões de coluna que retornam texto JSON. Você também pode criar JSON manualmente usando a função JSON_QUERY. O exemplo a seguir demonstra essas técnicas.  
  
```sql  
SELECT col1, col2, col3,  
     (SELECT col11, col12, col13 FROM t11 WHERE t11.FK = t1.PK FOR JSON PATH) as t11,  
     (SELECT col21, col22, col23 FROM t21 WHERE t21.FK = t1.PK FOR JSON PATH) as t21,  
     (SELECT col31, col32, col33 FROM t31 WHERE t31.FK = t1.PK FOR JSON PATH) as t31,  
     JSON_QUERY('{"'+col4'":"'+col5+'"}' as t41  
FROM t1  
FOR JSON PATH  
```  
  
Todos os resultados de uma consulta FOR JSON ou a função JSON_QUERY nas expressões de coluna são formatados como um sub-objeto JSON aninhado separado e incluídos no resultado principal.  

### <a name="prevent-double-escaped-json-in-for-json-output"></a>Evitar JSON de escape duplo na saída FOR JSON  
 **Pergunta.** Tenho um texto JSON armazenado em uma coluna de tabela. Desejo incluí-lo na saída do FOR JSON. Mas, FOR JSON ignora todos os caracteres em JSON, portanto, estou recebendo uma string JSON em vez de um objeto aninhado, como mostrado no exemplo a seguir.  
  
```sql  
SELECT 'Text' AS myText, '{"day":23}' AS myJson  
FOR JSON PATH  
```  
  
 Essa consulta gera a saída a seguir.  
  
```json  
[{"myText":"Text", "myJson":"{\"day\":23}"}]  
```  
  
 Como impedir esse comportamento? Desejo que `{"day":23}` seja retornado como um objeto JSON e não como texto de escape.  
  
 **Resposta.** O JSON armazenado em uma coluna de texto ou um literal é tratado como qualquer texto. Ou seja, ele foi colocado entre aspas duplas e escape. Se você quiser retornar um objeto JSON sem escape, passe a coluna JSON como um argumento para a função JSON_QUERY, conforme mostrado no exemplo a seguir.  
  
```sql  
SELECT col1, col2, col3, JSON_QUERY(jsoncol1) AS jsoncol1  
FROM tab1  
FOR JSON PATH  
```  
  
 JSON_QUERY sem seu segundo parâmetro opcional retorna somente o primeiro argumento como resultado. Como JSON_QUERY sempre retorna um JSON válido, FOR JSON sabe que esse resultado não precisa de escape.

### <a name="json-generated-with-the-withoutarraywrapper-clause-is-escaped-in-for-json-output"></a>O JSON gerado com a cláusula WITHOUT_ARRAY_WRAPPER tem escape na saída FOR JSON  
 **Pergunta.** Estou tentando formatar uma expressão de coluna usando FOR JSON e a opção WITHOUT_ARRAY_WRAPPER.  
  
```sql  
SELECT 'Text' as myText,  
   (SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) as myJson  
FOR JSON PATH   
```  
  
 Parece que o texto retornado pela consulta FOR JSON tem escape como texto sem formatação. Isso ocorre somente se a opção WITHOUT_ARRAY_WRAPPER for especificada. Por que ele não é tratado como um objeto JSON e incluído sem escape no resultado?  
  
 **Resposta.** Se você especificar o `WITHOUT_ARRAY_WRAPPER` opção interna `FOR JSON`, o texto JSON resultante não é necessariamente válido JSON. Portanto, externa `FOR JSON` pressupõe que ele é um texto sem formatação e ignora a cadeia de caracteres. Se você tiver certeza de que o JSON de saída é válido, colocá-los com o `JSON_QUERY` na função para promovê-lo para corretamente formatado JSON, conforme mostrado no exemplo a seguir.  
  
```sql  
SELECT 'Text' as myText,  
      JSON_QUERY((SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER)) as myJson  
FOR JSON PATH    
```  

## <a name="openjson-and-json-input"></a>Entrada de OPENJSON e JSON

### <a name="return-a-nested-json-sub-object-from-json-text-with-openjson"></a>Retornar um sub-objeto JSON aninhado de texto JSON com OPENJSON  
 **Pergunta.** Não consigo abrir uma matriz de objetos JSON complexos que contém valores escalares, objetos e matrizes usando OPENJSON com um esquema explícito. Quando faço referência a uma chave na cláusula WITH, somente valores escalares são retornados. Objetos e matrizes são retornados como valores nulos. Como extrair objetos ou matrizes como objetos JSON?  
  
 **Resposta.** Se você quiser retornar um objeto ou uma matriz como uma coluna, use a opção AS JSON na definição de coluna, conforme mostrado no exemplo a seguir.  
  
```sql  
SELECT scalar1, scalar2, obj1, obj2, arr1  
FROM OPENJSON(@json)  
    WITH ( scalar1 int,  
        scalar2 datetime2,  
        obj1 NVARCHAR(MAX) AS JSON,  
        obj2 NVARCHAR(MAX) AS JSON,  
        arr1 NVARCHAR(MAX) AS JSON)  
```  

### <a name="return-long-text-value-with-openjson-instead-of-jsonvalue"></a>Retornar o valor de texto longo com OPENJSON em vez de JSON_VALUE
 **Pergunta.** Tenho uma chave de descrição em texto JSON que contém texto longo. `JSON_VALUE(@json, '$.description')` retorna NULL em vez de um valor.  
  
 **Resposta.** JSON_VALUE foi projetado para retornar valores escalares pequenos. Geralmente, a função retorna NULL em vez de um erro de estouro. Se quiser retornar valores maiores, use OPENJSON, que oferece suporte a valores de NVARCHAR(MAX), conforme é mostrado no exemplo a seguir.  
  
```sql  
SELECT myText FROM OPENJSON(@json) WITH (myText NVARCHAR(MAX) '$.description')  
```  

### <a name="handle-duplicate-keys-with-openjson-instead-of-jsonvalue"></a>Lidar com chaves duplicadas com OPENJSON em vez de JSON_VALUE
 **Pergunta.** Tenho chaves duplicadas no texto JSON. JSON_VALUE retorna apenas a primeira chave encontrada no caminho. Como retornar todas as chaves que têm o mesmo nome?  
  
 **Resposta.** Funções escalares internas do JSON retornam somente a primeira ocorrência do objeto referenciado. Se você precisar de mais de uma chave, use a função com valor de tabela OPENJSON, conforme é mostrado no exemplo a seguir.  
  
```sql  
SELECT value FROM OPENJSON(@json, '$.info.settings')  
WHERE [key] = 'color'  
```  

### <a name="openjson-requires-compatibility-level-130"></a>OPENJSON requer o nível de compatibilidade 130  
 **Pergunta.** Estou tentando executar OPENJSON no SQL Server 2016 e estou recebendo o erro a seguir.  
  
 `Msg 208, Level 16, State 1 ‘Invalid object name OPENJSON’`  
  
 **Resposta.** A função OPENJSON está disponível somente no nível de compatibilidade 130. Se o nível de compatibilidade do seu banco de dados for inferior a 130, a função OPENJSON será ocultada. Outras funções JSON estão disponíveis em todos os níveis de compatibilidade.  
 
## <a name="other-questions"></a>Outras perguntas

### <a name="reference-keys-that-contain-non-alphanumeric-characters-in-json-text"></a>Chaves de referência que contêm caracteres não alfanuméricos em texto JSON  
 **Pergunta.** Tenho caracteres não alfanuméricos em chaves em texto JSON. Como posso fazer referência a essas propriedades?  
  
 **Resposta.** Coloque-os entre aspas em caminhos JSON. Por exemplo, `JSON_VALUE(@json, '$."$info"."First Name".value')`.
 
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Saiba mais sobre o suporte interno a JSON no SQL Server  
Para muitas soluções específicas, casos de uso e recomendações, consulte o [postagens no blog sobre o suporte interno a JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) no SQL Server e no banco de dados SQL Azure por Jovan Popovic, gerente de programas da Microsoft.

