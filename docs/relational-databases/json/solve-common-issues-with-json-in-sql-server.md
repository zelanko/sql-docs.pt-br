---
title: "Perguntas frequentes sobre JSON no SQL Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "JSON, PERGUNTAS FREQUENTES"
ms.assetid: feae120b-55cc-4601-a811-278ef1c551f9
caps.latest.revision: 9
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Perguntas frequentes sobre JSON no SQL Server
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Encontre respostas para perguntas comuns sobre o suporte interno a JSON no SQL Server.  
 
## Saída de FOR JSON e JSON

### FOR JSON PATH ou FOR JSON AUTO?  
 **Pergunta.** Preciso criar um resultado de texto JSON de uma consulta SQL simples em uma única tabela. FOR JSON PATH e FOR JSON AUTO produzem a mesma saída. Qual dessas duas opções deve usar?  
  
 **Resposta.** Use FOR JSON PATH. Embora não haja diferença na saída JSON, o modo AUTO tem lógica adicional que verifica se as colunas devem ser aninhadas. Considere a opção padrão PATH.  

### Criar uma estrutura aninhada de JSON  
 **Pergunta.** Preciso produzir JSON complexo com várias matrizes no mesmo nível. FOR JSON PATH pode criar objetos aninhados usando caminhos e FOR JSON AUTO cria o nível de aninhamento para cada tabela. Nenhuma dessas duas opções me permite gerar a saída desejada. Como posso criar um formato JSON personalizado que as opções existentes não suportam diretamente?  
  
 **Resposta.** Você pode criar qualquer estrutura de dados adicionando consultas FOR JSON como expressões de coluna que retornam texto JSON ou criar JSON manualmente usando a função JSON_QUERY, conforme é mostrado no exemplo a seguir.  
  
```tsql  
SELECT col1, col2, col3,  
             (SELECT col11, col12, col13 FROM t11 WHERE t11.FK = t1.PK FOR JSON PATH) as t11,  
             (SELECT col21, col22, col23 FROM t21 WHERE t21.FK = t1.PK FOR JSON PATH) as t21,  
             (SELECT col31, col32, col33 FROM t31 WHERE t31.FK = t1.PK FOR JSON PATH) as t31,  
             JSON_QUERY('{"'+col4'":"'+col5+'"}' as t41  
FROM t1  
FOR JSON PATH  
```  
  
Todos os resultados de uma consulta FOR JSON ou a função JSON_QUERY nas expressões de coluna são formatados como um sub-objeto JSON aninhado separado e incluídos no resultado principal.  

### Evitar JSON de escape duplo na saída FOR JSON  
 **Pergunta.** Tenho um texto JSON armazenado em uma coluna de tabela. Desejo incluí-lo na saída do FOR JSON. FOR JSON realiza o escape de todos os caracteres em JSON, estou recebendo uma string JSON em vez de um objeto aninhado, como mostrado no exemplo a seguir.  
  
```tsql  
SELECT 'Text' as myText, '{"day":23}' as myJson  
FOR JSON PATH  
```  
  
 Essa consulta gera a saída a seguir.  
  
```json  
[{"myText":"Text","myJson":"{\"day\":23}"}]  
```  
  
 Como impedir esse comportamento? Desejo que `{"day":23}` seja retornado como um objeto JSON e não como texto de escape.  
  
 **Resposta.** O JSON armazenado em uma coluna de texto ou um literal é tratado como qualquer texto. Ele é colocado entre aspas duplas e inclui escape. Se você quiser retornar um objeto JSON sem escape, é preciso passar essa coluna como um argumento para a função JSON_QUERY, conforme é mostrado no exemplo a seguir.  
  
```tsql  
SELECT col1, col2, col3, JSON_QUERY(jsoncol1) AS jsoncol1  
FROM tab1  
FOR JSON PATH  
```  
  
 JSON_QUERY sem seu segundo parâmetro opcional retorna somente o primeiro argumento como resultado. Como JSON_QUERY retorna um JSON válido, FOR JSON sabe que esse resultado não precisa de escape.

### O JSON gerado com a cláusula WITHOUT_ARRAY_WRAPPER tem escape na saída FOR JSON  
 **Pergunta.** Estou tentando formatar uma expressão de coluna usando FOR JSON e a opção WITHOUT_ARRAY_WRAPPER.  
  
```tsql  
SELECT 'Text' as myText,  
       (SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) as myJson  
FOR JSON PATH   
```  
  
 Parece que o texto retornado pela consulta FOR JSON tem escape como texto sem formatação. Isso ocorre somente se a opção WITHOUT_ARRAY_WRAPPER for especificada. Por que ele não é tratado como um objeto JSON e incluído sem escape no resultado?  
  
 **Resposta.** Se você especificar a opção WITHOUT_ARRAY_WRAPPER, o texto JSON gerado não é necessariamente válido. Portanto, a consulta FOR JSON externa pressupõe que ele é um texto sem formatação e realiza o escape da string. Se você tiver certeza de que a saída JSON é válida, insira-a na função JSON_QUERY para promovê-la a JSON com formato correto, conforme é mostrado no exemplo a seguir.  
  
```tsql  
SELECT 'Text' as myText,  
      JSON_QUERY((SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER)) as myJson  
FOR JSON PATH    
```  

## Entrada de OPENJSON e JSON

### Retornar um sub-objeto JSON aninhado de texto JSON com OPENJSON  
 **Pergunta.** Não consigo abrir uma matriz de objetos JSON complexos que contém valores escalares, objetos e matrizes usando OPENJSON com um esquema explícito. Quando faço referência a uma chave na cláusula WITH, somente valores escalares são retornados. Objetos e matrizes são retornados como valores nulos. Como extrair objetos ou matrizes de objetos JSON?  
  
 **Resposta.** Se você quiser retornar um objeto ou uma matriz como uma coluna, use a opção AS JSON na definição de coluna, conforme mostrado no exemplo a seguir.  
  
```tsql  
SELECT scalar1, scalar2, obj1, obj2, arr1  
FROM OPENJSON(@json)  
             WITH ( scalar1 int,  
                          scalar2 datetime2,  
                          obj1 NVARCHAR(MAX) AS JSON,  
                          obj2 NVARCHAR(MAX) AS JSON,  
                          arr1 NVARCHAR(MAX) AS JSON)  
```  

### Use OPENJSON no lugar de JSON_VALUE para retornar valores de texto longos  
 **Pergunta.** Tenho uma chave de descrição em texto JSON que contém texto longo. `JSON_VALUE(@json, '$.description')` retorna NULL em vez de um valor.  
  
 **Resposta.** JSON_VALUE foi projetado para retornar valores escalares pequenos. Geralmente, a função retorna NULL em vez de um erro de estouro. Se quiser retornar valores maiores, use OPENJSON, que oferece suporte a valores de NVARCHAR(MAX), conforme é mostrado no exemplo a seguir.  
  
```tsql  
SELECT myText FROM OPENJSON(@json) WITH (myText NVARCHAR(MAX) '$.description')  
```  

### Use OPENJSON no lugar de JSON_VALUE para tratar chaves duplicadas  
 **Pergunta.** Tenho chaves duplicadas no texto JSON. JSON_VALUE retorna apenas a primeira chave encontrada no caminho. Como retornar todas as chaves que têm o mesmo nome?  
  
 **Resposta.** As funções escalares internas do JSON retornam somente a primeira ocorrência do objeto referenciado. Se você precisar de mais de uma chave, use a função com valor de tabela OPENJSON, conforme é mostrado no exemplo a seguir.  
  
```tsql  
SELECT value FROM OPENJSON(@json, '$.info.settings')  
WHERE [key] = 'color'  
```  

### OPENJSON requer o nível de compatibilidade 130  
 **Pergunta.** Estou tentando executar OPENJSON no SQL Server 2016 e estou recebendo o erro a seguir.  
  
 `Msg 208, Level 16, State 1 ‘Invalid object name OPENJSON’`  
  
 **Resposta.** A função OPENJSON está disponível somente no nível de compatibilidade 130. Se o nível de compatibilidade do seu banco de dados for inferior a 130, a função OPENJSON será ocultada. Outras funções JSON estão disponíveis em todos os níveis de compatibilidade.  
 
## Outras perguntas

### Chaves de referência que contêm caracteres não alfanuméricos em texto JSON  
 **Pergunta.** Tenho caracteres não alfanuméricos em chaves em texto JSON. Como posso fazer referência a essas propriedades?  
  
 **Resposta.** Coloque-os entre aspas em caminhos JSON. Por exemplo, `JSON_VALUE(@json, '$."$info"."First Name".value')`.
 