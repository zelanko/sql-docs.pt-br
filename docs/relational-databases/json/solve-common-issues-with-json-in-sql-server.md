---
description: Solucionar problemas comuns com JSON no SQL Server
title: Solucionar problemas comuns com JSON no SQL Server
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, FAQ
ms.assetid: feae120b-55cc-4601-a811-278ef1c551f9
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 30e1204a188c4b71c001bd4c0d00c0df3ce9200f
ms.sourcegitcommit: 28fecbf61ae7b53405ca378e2f5f90badb1a296a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2020
ms.locfileid: "96595100"
---
# <a name="solve-common-issues-with-json-in-sql-server"></a>Solucionar problemas comuns com JSON no SQL Server
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sqlserver2016-asdb.md)]

 Encontre respostas para perguntas comuns sobre o suporte interno a JSON no SQL Server.  
 
## <a name="for-json-and-json-output"></a>Saída de FOR JSON e JSON

### <a name="for-json-path-or-for-json-auto"></a>FOR JSON PATH ou FOR JSON AUTO?  
 **Pergunta.** Quero criar um resultado de texto JSON de uma consulta SQL simples em uma única tabela. FOR JSON PATH e FOR JSON AUTO produzem a mesma saída. Qual dessas duas opções deve usar?  
  
 **Resposta.** Use FOR JSON PATH. Embora não haja diferença na saída JSON, o modo AUTO aplica lógica adicional que verifica se as colunas devem ser aninhadas. Considere a opção padrão PATH.  

### <a name="create-a-nested-json-structure"></a>Criar uma estrutura aninhada de JSON  
 **Pergunta.** Quero produzir JSON complexo com várias matrizes no mesmo nível. FOR JSON PATH pode criar objetos aninhados usando caminhos e FOR JSON AUTO cria o nível de aninhamento para cada tabela. Nenhuma dessas duas opções me permite gerar a saída que eu desejo. Como posso criar um formato JSON personalizado que as opções existentes não suportam diretamente?  
  
 **Resposta.** É possível criar qualquer estrutura de dados adicionando consultas FOR JSON como expressões de coluna que retornam texto JSON. Você também pode criar JSON manualmente usando a função JSON_QUERY. O exemplo a seguir demonstra essas técnicas.  
  
```sql  
SELECT col1, col2, col3,  
     (SELECT col11, col12, col13 FROM t11 WHERE t11.FK = t1.PK FOR JSON PATH) as t11,  
     (SELECT col21, col22, col23 FROM t21 WHERE t21.FK = t1.PK FOR JSON PATH) as t21,  
     (SELECT col31, col32, col33 FROM t31 WHERE t31.FK = t1.PK FOR JSON PATH) as t31,  
     JSON_QUERY('{"'+col4'":"'+col5+'"}') as t41  
FROM t1  
FOR JSON PATH  
```  
  
Todos os resultados de uma consulta FOR JSON ou a função JSON_QUERY nas expressões de coluna são formatados como um sub-objeto JSON aninhado separado e incluídos no resultado principal.  

### <a name="prevent-double-escaped-json-in-for-json-output"></a>Evitar JSON de escape duplo na saída FOR JSON  
 **Pergunta.** Tenho um texto JSON armazenado em uma coluna de tabela. Desejo incluí-lo na saída do FOR JSON. Contudo, FOR JSON realiza o escape de todos os caracteres em JSON, por isso estou recebendo uma cadeia de caracteres JSON em vez de um objeto aninhado, como mostrado no exemplo a seguir.  
  
```sql  
SELECT 'Text' AS myText, '{"day":23}' AS myJson  
FOR JSON PATH  
```  
  
 Essa consulta gera a saída a seguir.  
  
```json  
[{"myText":"Text", "myJson":"{\"day\":23}"}]  
```  
  
 Como impedir esse comportamento? Desejo que `{"day":23}` seja retornado como um objeto JSON e não como texto de escape.  
  
 **Resposta.** O JSON armazenado em uma coluna de texto ou um literal é tratado como qualquer texto. Isso é, ele é colocado entre aspas duplas e em escape. Se você quiser retornar um objeto JSON sem escape, passe a coluna JSON como um argumento para a função JSON_QUERY, conforme mostrado no exemplo a seguir.  
  
```sql  
SELECT col1, col2, col3, JSON_QUERY(jsoncol1) AS jsoncol1  
FROM tab1  
FOR JSON PATH  
```  
  
 JSON_QUERY sem seu segundo parâmetro opcional retorna somente o primeiro argumento como resultado. Como JSON_QUERY sempre retorna um JSON válido, FOR JSON sabe que esse resultado não precisa de escape.

### <a name="json-generated-with-the-without_array_wrapper-clause-is-escaped-in-for-json-output"></a>O JSON gerado com a cláusula WITHOUT_ARRAY_WRAPPER tem escape na saída FOR JSON  
 **Pergunta.** Estou tentando formatar uma expressão de coluna usando FOR JSON e a opção WITHOUT_ARRAY_WRAPPER.  
  
```sql  
SELECT 'Text' as myText,  
   (SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) as myJson  
FOR JSON PATH   
```  
  
 Parece que o texto retornado pela consulta FOR JSON tem escape como texto sem formatação. Isso ocorre somente se a opção WITHOUT_ARRAY_WRAPPER for especificada. Por que ele não é tratado como um objeto JSON e incluído sem escape no resultado?  
  
 **Resposta.** Se você especificar a opção `WITHOUT_ARRAY_WRAPPER` no `FOR JSON` interno, o texto JSON resultante não será necessariamente um JSON válido. Portanto, o `FOR JSON` externo supõe que ele é um texto sem formatação e realiza o escape da cadeia de caracteres. Se você tiver certeza que a saída JSON é válida, encapsule-a na função `JSON_QUERY` para promovê-la a JSON com formato correto, conforme mostrado no exemplo a seguir.  
  
```sql  
SELECT 'Text' as myText,  
      JSON_QUERY((SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER)) as myJson  
FOR JSON PATH    
```  

## <a name="openjson-and-json-input"></a>Entrada de OPENJSON e JSON

### <a name="return-a-nested-json-sub-object-from-json-text-with-openjson"></a>Retornar um sub-objeto JSON aninhado de texto JSON com OPENJSON  
 **Pergunta.** Não consigo abrir uma matriz de objetos JSON complexos que contém valores escalares, objetos e matrizes usando OPENJSON com um esquema explícito. Quando faço referência a uma chave na cláusula WITH, somente valores escalares são retornados. Objetos e matrizes são retornados como valores nulos. Como extraio objetos ou matrizes como objetos JSON?  
  
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

### <a name="return-long-text-value-with-openjson-instead-of-json_value"></a>Retorne o valor de texto longo com OPENJSON em vez de JSON_VALUE
 **Pergunta.** Tenho uma chave de descrição em texto JSON que contém texto longo. `JSON_VALUE(@json, '$.description')` retorna NULL em vez de um valor.  
  
 **Resposta.** JSON_VALUE foi projetado para retornar valores escalares pequenos. Geralmente, a função retorna NULL em vez de um erro de estouro. Se quiser retornar valores maiores, use OPENJSON, que oferece suporte a valores de NVARCHAR(MAX), conforme é mostrado no exemplo a seguir.  
  
```sql  
SELECT myText FROM OPENJSON(@json) WITH (myText NVARCHAR(MAX) '$.description')  
```  

### <a name="handle-duplicate-keys-with-openjson-instead-of-json_value"></a>Use chaves duplicadas com OPENJSON em vez de JSON_VALUE
 **Pergunta.** Tenho chaves duplicadas no texto JSON. JSON_VALUE retorna apenas a primeira chave encontrada no caminho. Como retornar todas as chaves que têm o mesmo nome?  
  
 **Resposta.** As funções escalares JSON internas retornam somente a primeira ocorrência do objeto referenciado. Se você precisar de mais de uma chave, use a função com valor de tabela OPENJSON, conforme é mostrado no exemplo a seguir.  
  
```sql  
SELECT value FROM OPENJSON(@json, '$.info.settings')  
WHERE [key] = 'color'  
```  

### <a name="openjson-requires-compatibility-level-130"></a>OPENJSON requer o nível de compatibilidade 130  
 **Pergunta.** Estou tentando executar OPENJSON no SQL Server 2016 e estou recebendo o erro a seguir.  
  
 `Msg 208, Level 16, State 1 'Invalid object name OPENJSON'`  
  
 **Resposta.** A função OPENJSON está disponível somente no nível de compatibilidade 130. Se o nível de compatibilidade do seu banco de dados for inferior a 130, a função OPENJSON será ocultada. Outras funções JSON estão disponíveis em todos os níveis de compatibilidade.  
 
## <a name="other-questions"></a>Outras perguntas

### <a name="reference-keys-that-contain-non-alphanumeric-characters-in-json-text"></a>Chaves de referência que contêm caracteres não alfanuméricos em texto JSON  
 **Pergunta.** Tenho caracteres não alfanuméricos em chaves em texto JSON. Como posso fazer referência a essas propriedades?  
  
 **Resposta.** Coloque-os entre aspas em caminhos JSON. Por exemplo, `JSON_VALUE(@json, '$."$info"."First Name".value')`.
 
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
