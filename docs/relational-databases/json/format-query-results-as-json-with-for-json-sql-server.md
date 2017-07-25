---
title: Formatar os resultados da consulta como JSON com o FOR JSON (SQL Server) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON
- JSON, exporting
- exporting JSON
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 50ef4db2a3c9eebcdf63ec9329eb22f1e0f001c0
ms.openlocfilehash: e59b0e12e0ee47a5ac8a68e539144401d80fb649
ms.contentlocale: pt-br
ms.lasthandoff: 07/19/2017

---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>Formatar os resultados da consulta como JSON com o FOR JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Formate os resultados da consulta ou exporte os dados do SQL Server como JSON adicionando a cláusula **FOR JSON** a uma instrução **SELECT**. Use a cláusula **FOR JSON** para simplificar os aplicativos cliente ao delegar a formatação da saída JSON do aplicativo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
 Ao usar a cláusula **FOR JSON**, é possível especificar explicitamente a estrutura da saída JSON ou permitir que a estrutura da instrução SELECT determine a saída.  
  
-   Use **FOR JSON PATH** para manter controle total sobre o formato da saída JSON. Você pode criar objetos wrapper e aninhar propriedades complexas.  
  
-   Use **FOR JSON AUTO** para formatar a saída JSON automaticamente com base na estrutura da instrução SELECT.  
  
Aqui está um exemplo de uma instrução **SELECT** com a cláusula **FOR JSON** e sua saída.
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png "FOR JSON")  
  
## <a name="option-1---you-control-output-with-for-json-path"></a>Opção 1 – Controle de saída com FOR JSON PATH
No modo **PATH** , você pode usar a sintaxe de ponto, por exemplo, `'Item.Price'` , para formatar a saída aninhada.  

Veja um exemplo de consulta que usa o modo **PATH** com a cláusula **FOR JSON** . O exemplo a seguir também usa a opção **ROOT** para especificar um elemento de raiz nomeado. 
  
 ![Diagrama de fluxo da saída FOR JSON](../../relational-databases/json/media/forjson-example1.png "Diagrama de fluxo da saída FOR JSON")  

### <a name="more-info-about-for-json-path"></a>Mais informações sobre o FOR JSON PATH
Para obter mais informações e exemplos, consulte [formato de saída de JSON aninhada com modo PATH &#40; SQL Server &#41; ](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).

Para sintaxe e uso, consulte [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  

## <a name="option-2---select-statement-controls-output-with-for-json-auto"></a>Opção 2 – Saída dos controles de instrução SELECT com FOR JSON AUTO
No modo **AUTO** , a estrutura da instrução SELECT determina o formato da saída JSON.

Por padrão, os valores **nulos** não são incluídos na saída. Você pode usar o **INCLUDE_NULL_VALUES** para alterar esse comportamento.  

Veja um exemplo de consulta que usa o modo **AUTO** com a cláusula **FOR JSON** .
 
**Consulta:**  
  
```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO  
```  
  
 **Resultados**  
  
```json  
[{
    "name": "John"
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```
 
### <a name="more-info-about-for-json-auto"></a>Mais informações sobre o FOR JSON AUTO
Para obter mais informações e exemplos, consulte [formato JSON saída automaticamente com o modo AUTO &#40; SQL Server &#41; ](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).

Para sintaxe e uso, consulte [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  
  
## <a name="control-other-json-output-options"></a>Controlar outras opções de saída JSON  
Controlar a saída de **FOR JSON** cláusula usando as seguintes opções adicionais.  
  
-   **RAIZ**. Para adicionar um único elemento de nível superior à saída JSON, especifique a opção **ROOT** . Se você não especificar essa opção, a saída JSON não tem um elemento raiz. Para obter mais informações, consulte [Add a Root Node to JSON Output with the ROOT Option &#40;SQL Server&#41; (Adicionar um nó raiz à saída JSON com a opção ROOT &#40;SQL Server&#41;)](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
-   **INCLUDE_NULL_VALUES**. Para incluir valores nulos na saída JSON, especifique a opção **INCLUDE_NULL_VALUES** . Se você não especificar essa opção, a saída não incluirá propriedades JSON para valores NULL nos resultados da consulta. Para obter mais informações, consulte [incluir valores nulos na saída JSON com a opção INCLUDE_NULL_VALUES &#40; SQL Server &#41; ](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).   

-   **WITHOUT_ARRAY_WRAPPER**. Para remover, por padrão, os colchetes que envolvem a saída JSON da cláusula **FOR JSON** , especifique a opção **WITHOUT_ARRAY_WRAPPER** . Use esta opção para gerar um único objeto JSON como saída de um resultado de linha única. Se você não especificar essa opção, a saída JSON é formatada como uma matriz - ou seja, ela é colocada entre colchetes. Para obter mais informações, consulte [Remove Square Brackets from JSON Output with the WITHOUT_ARRAY_WRAPPER Option &#40;SQL Server&#41; (Remover os colchetes da saída JSON com a opção WITHOUT_ARRAY_WRAPPER &#40;SQL Server&#41;)](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md). 
   
## <a name="output-of-the-for-json-clause"></a>Saída da cláusula FOR JSON  
A saída da cláusula **FOR JSON** tem as seguintes características:  
  
1.  O conjunto de resultados contém uma única coluna.
    -   Um conjunto de resultados pequeno pode conter uma única linha.
    -   Um conjunto de resultados grande divide a cadeia de caracteres JSON longa em várias linhas.
        -   Por padrão, o SQL Server Management Studio (SSMS) concatena os resultados em uma única linha quando a configuração de saída é **resultados em grade**. A barra de status do SSMS exibe a contagem de linhas real.
        -   Outros aplicativos cliente podem exigir o código para recombinar os resultados longos em uma cadeia de caracteres JSON única e válida, concatenando os conteúdos de várias linhas. Para obter um exemplo do código em um aplicativo c#, consulte [Use a saída JSON em um aplicativo cliente c#](https://docs.microsoft.com/en-us/sql/relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server#use-for-json-output-in-a-c-client-app).
  
     ![Exemplo de saída FOR JSON](../../relational-databases/json/media/forjson-example2.png "Exemplo de saída FOR JSON")  
  
2.  Os resultados são formatados como uma matriz de objetos JSON.  
  
    -   O número de elementos na matriz JSON é igual ao número de linhas nos resultados da instrução SELECT (antes que a cláusula FOR JSON é aplicada). 
  
    -   Cada linha nos resultados da instrução SELECT (antes que a cláusula FOR JSON é aplicada) se torna um objeto JSON separado na matriz.  
  
    -   Cada coluna nos resultados da instrução SELECT (antes da cláusula é aplicada do FOR JSON) se torna uma propriedade do objeto JSON.  
  
3.  Os dois os nomes das colunas e seus valores são escapados de acordo com a sintaxe JSON. Para obter mais informações, consulte [How FOR JSON escapes special characters and control characters &#40;SQL Server&#41; (Como o FOR JSON ignora os caracteres especiais e os caracteres de controle &#40;SQL Server&#41;)](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md).
  
### <a name="example"></a>Exemplo
Aqui está um exemplo que demonstra como o **FOR JSON** cláusula formata a saída JSON.  
  
**Resultados da consulta**  
  
|||||  
|-|-|-|-|  
|**A**|**B**|**C**|**D**|  
|10|11|12|X|  
|20|21|22|S|  
|30|31|32|Z|  
  
 **Saída JSON**  
  
```json  
[{
    "A": 10,
    "B": 11,
    "C": 12,
    "D": "X"
}, {
    "A": 20,
    "B": 21,
    "C": 22,
    "D": "Y"
}, {
    "A": 30,
    "B": 31,
    "C": 32,
    "D": "Z"
}] 
```  

 Para obter mais informações sobre o que você vê na saída da cláusula **FOR JSON**, consulte os seguintes tópicos.  
-   [How FOR JSON converts SQL Server data types to JSON data types &#40;SQL Server&#41; (Como FOR JSON converte tipos de dados do SQL Server para tipos de dados &#40;SQL Server&#41;)](../../relational-databases/json/how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server.md)  
A cláusula **FOR JSON** usa as regras descritas neste tópico para converter os tipos de dados SQL em tipos JSON na saída JSON.  

-   [How FOR JSON escapes special characters and control characters &#40;SQL Server&#41; (Como o FOR JSON ignora os caracteres especiais e os caracteres de controle &#40;SQL Server&#41;)](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)  
 A cláusula **FOR JSON** ignora os caracteres especiais e representa os caracteres de controle na saída JSON, conforme descrito neste tópico.  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Saiba mais sobre o suporte interno a JSON no SQL Server  
Para muitas soluções específicas, casos de uso e recomendações, consulte o [postagens no blog sobre o suporte interno a JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) no SQL Server e no banco de dados SQL Azure por Jovan Popovic, gerente de programas da Microsoft.
  
## <a name="see-also"></a>Consulte também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [Use FOR JSON output in SQL Server and in client apps &#40;SQL Server&#41; (Usar a saída FOR JSON no SQL Server e em aplicativos cliente &#40;SQL Server&#41;)](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  

