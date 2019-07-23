---
title: Formatar os resultados da consulta como JSON com o FOR JSON (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2019
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON
- JSON, exporting
- exporting JSON
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6ccdd995900f10b8d0a83f10795659e1a5050995
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909403"
---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>Formatar os resultados da consulta como JSON com o FOR JSON (SQL Server)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Formate os resultados da consulta ou exporte os dados do SQL Server como JSON adicionando a cláusula **FOR JSON** a uma instrução **SELECT**. Use a cláusula **FOR JSON** para simplificar os aplicativos cliente ao delegar a formatação da saída JSON do aplicativo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
 Ao usar a cláusula **FOR JSON**, é possível especificar explicitamente a estrutura da saída JSON ou permitir que a estrutura da instrução SELECT determine a saída.  
  
-   Use **FOR JSON PATH** para manter controle total sobre o formato da saída JSON. Você pode criar objetos wrapper e aninhar propriedades complexas.  
  
-   Use **FOR JSON AUTO** para formatar a saída JSON automaticamente com base na estrutura da instrução SELECT.  
  
Aqui está um exemplo de uma instrução **SELECT** com a cláusula **FOR JSON** e sua saída.
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png)
  
## <a name="option-1---you-control-output-with-for-json-path"></a>Opção 1 – Controle de saída com FOR JSON PATH
No modo **PATH**, você pode usar a sintaxe de ponto, por exemplo, `'Item.UnitPrice'`, para formatar a saída aninhada.  

Veja um exemplo de consulta que usa o modo **PATH** com a cláusula **FOR JSON** . O exemplo a seguir também usa a opção **ROOT** para especificar um elemento de raiz nomeado. 
  
 ![Diagrama de fluxo de saída PARA JSON](../../relational-databases/json/media/forjson-example1.png) 

### <a name="more-info-about-for-json-path"></a>Mais informações sobre o FOR JSON PATH
Para obter mais informações e exemplos, consulte [Formato de saída JSON aninhado com modo PATH &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).

Para sintaxe e uso, consulte [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  

## <a name="option-2---select-statement-controls-output-with-for-json-auto"></a>Opção 2 – Saída dos controles de instrução SELECT com FOR JSON AUTO
No modo **AUTO** , a estrutura da instrução SELECT determina o formato da saída JSON.

Por padrão, os valores **nulos** não são incluídos na saída. Você pode usar o **INCLUDE_NULL_VALUES** para alterar esse comportamento.  

Veja um exemplo de consulta que usa o modo **AUTO** com a cláusula **FOR JSON** .

```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO;
```  

E aqui está o JSON retornado.

```json  
[{
    "name": "John"
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```

### <a name="2b---example-with-join-and-null"></a>2.b – exemplo de JOIN e NULL

O exemplo a seguir de `SELECT...FOR JSON AUTO` inclui uma exibição de como seria a aparência dos resultados JSON quando há um relacionamento de 1:Muitos entre os dados de tabelas com `JOIN`.

A ausência do valor nulo no JSON retornado também é ilustrada. No entanto, você pode substituir esse comportamento padrão usando a palavra-chave `INCLUDE_NULL_VALUES` na cláusula `FOR`.

```sql
go

DROP TABLE IF EXISTS #tabStudent;
DROP TABLE IF EXISTS #tabClass;

go

CREATE TABLE #tabClass
(
   ClassGuid   uniqueIdentifier  not null  default newid(),
   ClassName   nvarchar(32)      not null
);

CREATE TABLE #tabStudent
(
   StudentGuid   uniqueIdentifier  not null  default newid(),
   StudentName   nvarchar(32)      not null,
   ClassGuid     uniqueIdentifier      null   -- Foreign key.
);

go

INSERT INTO #tabClass
      (ClassGuid, ClassName)
   VALUES
      ('DE807673-ECFC-4850-930D-A86F921DE438', 'Algebra Math'),
      ('C55C6819-E744-4797-AC56-FF8A729A7F5C', 'Calculus Math'),
      ('98509D36-A2C8-4A65-A310-E744F5621C83', 'Art Painting')
;

INSERT INTO #tabStudent
      (StudentName, ClassGuid)
   VALUES
      ('Alice Apple', 'DE807673-ECFC-4850-930D-A86F921DE438'),
      ('Alice Apple', 'C55C6819-E744-4797-AC56-FF8A729A7F5C'),
      ('Betty Boot' , 'C55C6819-E744-4797-AC56-FF8A729A7F5C'),
      ('Betty Boot' , '98509D36-A2C8-4A65-A310-E744F5621C83'),
      ('Carla Cap'  , null)
;

go

SELECT
      c.ClassName,
      s.StudentName
   from
                       #tabClass   as c
      RIGHT OUTER JOIN #tabStudent as s ON s.ClassGuid = c.ClassGuid
   --where
   --   c.ClassName LIKE '%Math%'
   order by
      c.ClassName,
      s.StudentName
   FOR
      JSON AUTO
      --, INCLUDE_NULL_VALUES
;

go

DROP TABLE IF EXISTS #tabStudent;
DROP TABLE IF EXISTS #tabClass;

go
```

E, em seguida, está o JSON gerado pelo SELECT anterior.

```json
JSON_F52E2B61-18A1-11d1-B105-00805F49916B

[
   {"s":[{"StudentName":"Carla Cap"}]},
   {"ClassName":"Algebra Math","s":[{"StudentName":"Alice Apple"}]},
   {"ClassName":"Art Painting","s":[{"StudentName":"Betty Boot"}]},
   {"ClassName":"Calculus Math","s":[{"StudentName":"Alice Apple"},{"StudentName":"Betty Boot"}]}
]
```

### <a name="more-info-about-for-json-auto"></a>Mais informações sobre o FOR JSON AUTO

Para obter informações e exemplos mais detalhados, consulte [Formato de saída JSON automático com o modo AUTO &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).

Para sintaxe e uso, consulte [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  
  
## <a name="control-other-json-output-options"></a>Controlar outras opções de saída JSON  
Controlar a saída da cláusula **FOR JSON** usando as seguintes opções adicionais.  
  
-   **ROOT**. Para adicionar um único elemento de nível superior à saída JSON, especifique a opção **ROOT** . Se você não especificar essa opção, a saída JSON não terá um elemento raiz. Para obter mais informações, consulte [Add a Root Node to JSON Output with the ROOT Option &#40;SQL Server&#41; (Adicionar um nó raiz à saída JSON com a opção ROOT &#40;SQL Server&#41;)](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
-   **INCLUDE_NULL_VALUES**. Para incluir valores nulos na saída JSON, especifique a opção **INCLUDE_NULL_VALUES** . Se você não especificar essa opção, a saída não incluirá propriedades JSON para valores NULL nos resultados da consulta. Para obter mais informações, consulte [Incluir valores Null na saída JSON com a opção INCLUDE_NULL_VALUES &#40;SQL Server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).   

-   **WITHOUT_ARRAY_WRAPPER**. Para remover, por padrão, os colchetes que envolvem a saída JSON da cláusula **FOR JSON** , especifique a opção **WITHOUT_ARRAY_WRAPPER** . Use esta opção para gerar um único objeto JSON como saída de um resultado de linha única. Se você não especificar essa opção, a saída JSON será formatada como uma matriz, ou seja, ela será colocada entre colchetes. Para obter mais informações, consulte [Remove Square Brackets from JSON Output with the WITHOUT_ARRAY_WRAPPER Option &#40;SQL Server&#41; (Remover os colchetes da saída JSON com a opção WITHOUT_ARRAY_WRAPPER &#40;SQL Server&#41;)](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md). 
   
## <a name="output-of-the-for-json-clause"></a>Saída da cláusula FOR JSON  
A saída da cláusula **FOR JSON** tem as seguintes características:  
  
1.  O conjunto de resultados contém uma única coluna.
    -   Um conjunto de resultados pequeno pode conter uma única linha.
    -   Um conjunto de resultados grande divide a cadeia de caracteres JSON longa em várias linhas.
        -   Por padrão, o SSMS (SQL Server Management Studio) concatena os resultados em uma única linha quando a configuração de saída é **Resultados em Grade**. A barra de status do SSMS exibe a contagem de linhas real.
        -   Outros aplicativos cliente podem exigir o código para recombinar os resultados longos em uma cadeia de caracteres JSON única e válida, concatenando os conteúdos de várias linhas. Para obter um exemplo do código em um aplicativo C#, consulte [Usar a saída FOR JSON em um aplicativo cliente C#](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md#use-for-json-output-in-a-c-client-app).
  
     ![Exemplo de saída PARA JSON](../../relational-databases/json/media/forjson-example2.png)  
  
2.  Os resultados são formatados como uma matriz de objetos JSON.  
  
    -   O número de elementos na matriz JSON é igual ao número de linhas nos resultados da instrução SELECT (antes da cláusula FOR JSON ser aplicada). 
  
    -   Cada linha nos resultados da instrução SELECT (antes da cláusula FOR JSON ser aplicada) se torna um objeto JSON separado na matriz.  
  
    -   Cada coluna nos resultados da instrução SELECT (antes da cláusula FOR JSON ser aplicada) se torna uma propriedade do objeto JSON.  
  
3.  Os dois os nomes das colunas e seus valores são escapados de acordo com a sintaxe JSON. Para obter mais informações, consulte [How FOR JSON escapes special characters and control characters &#40;SQL Server&#41; (Como o FOR JSON ignora os caracteres especiais e os caracteres de controle &#40;SQL Server&#41;)](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md).

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="example"></a>Exemplo
Veja este exemplo que demonstra como a cláusula **FOR JSON** formata a saída JSON.  
  
**Resultados da consulta**  
  
|||||  
|-|-|-|-|  
|**A**|**B**|**C**|**D**|  
|10|11|12|X|  
|20|21|22|S|  
|30|31|32|Z|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Consulte Também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [Use FOR JSON output in SQL Server and in client apps &#40;SQL Server&#41; (Usar a saída FOR JSON no SQL Server e em aplicativos cliente &#40;SQL Server&#41;)](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  
