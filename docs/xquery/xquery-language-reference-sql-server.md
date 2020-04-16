---
title: XQuery Language Reference (SQL Server) | Microsoft Docs
description: Aprenda sobre o idioma XQuery para SQL Server e visualize uma referência completa de idioma.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
helpviewer_keywords:
- XQuery
- XQuery, about XQuery
- xml data type [SQL Server], XQuery
- XML [SQL Server], XQuery
- queries [XML in SQL Server], XQuery
ms.assetid: 8a69344f-2990-4357-8160-cb26aac95b91
author: rothja
ms.author: jroth
ms.openlocfilehash: 35a1418e416e32ab5b8dc9647c4a9aa24700b624
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388613"
---
# <a name="xquery-language-reference-sql-server"></a>Referência de linguagem Xquery (SQL Server)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../includes/tsql-md.md)]suporta um subconjunto da linguagem XQuery que é usado para consultar o tipo de dados **xml.** Essa implementação da XQuery está alinhada com o Working Draft de julho de 2004 da XQuery. Essa linguagem está sendo desenvolvida pela World Wide Web Consortium (W3C), com a participação de todos os principais fornecedores de banco de dados e também da Microsoft. Como as especificações da W3C podem passar por revisões futuras antes de se tornarem recomendações da W3C, essa implementação pode ser diferente da recomendação final. Este tópico descreve a semântica e a sintaxe do subconjunto da XQuery com suporte no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Para obter mais informações, consulte a [especificação de idioma W3C XQuery 1.0](https://go.microsoft.com/fwlink/?LinkId=48846).  
  
 A XQuery é uma linguagem que pode consultar dados XML estruturados ou semiestruturados. Com o suporte ao tipo de [!INCLUDE[ssDE](../includes/ssde-md.md)]dados **xml** fornecido no , os documentos podem ser armazenados em um banco de dados e, em seguida, consultados usando XQuery.  
  
 A XQuery é baseada na linguagem XPath existente, com suporte adicional para uma melhor iteração, melhores resultados de classificação e com a capacidade de construir o XML necessário. A XQuery opera no modelo de dados XQuery. Essa é uma abstração de documentos XML e de resultados da XQuery podem ser com tipo ou sem-tipo. As informações de tipo são baseadas nos tipos fornecidos pela linguagem de esquema XML da W3C. Se nenhuma informação de tipo estiver disponível, a XQuery controlará os dados como sendo sem-tipo. Isso é semelhante ao modo como a versão 1.0 do XPath trata o XML.  
  
 Para consultar uma instância XML armazenada em uma variável ou coluna do tipo **xml,** você usa os [métodos de tipo de dados xml](../t-sql/xml/xml-data-type-methods.md). Por exemplo, você pode declarar uma variável do tipo **xml** e quernitá-la usando o método **de consulta()** do tipo de dados **xml.**  
  
```sql
DECLARE @x xml  
SET @x = '<ROOT><a>111</a></ROOT>'  
SELECT @x.query('/ROOT/a')  
```  
  
 No exemplo a seguir, a consulta é especificada na coluna Instruções do tipo **xml** na tabela ProductModel no banco de dados AdventureWorks.  
  
```sql
SELECT Instructions.query('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 O XQuery inclui a declaração namespace `declare namespace``AWMI=...`e `/AWMI:root/AWMI:Location[@LocationID=10]`a expressão de consulta, .  
  
 Observe que o XQuery é especificado com a coluna Instruções do tipo **xml.** O [método de consulta()](../t-sql/xml/query-method-xml-data-type.md) do tipo de dados xml é usado para especificar o XQuery.  
  
 A tabela a seguir lista os tópicos relacionados que podem ajudar a entender a implementação da XQuery no [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)|Explica o suporte para o tipo [!INCLUDE[ssDE](../includes/ssde-md.md)] de dados **xml**no e os métodos que você pode usar contra este tipo de dados. O tipo de dados **xml** forma o modelo de dados XQuery de entrada no qual as expressões XQuery são executadas.|  
|[Coleções de esquemas XML &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)|Descreve quais podem ser os tipos das instâncias XML armazenadas em um banco de dados. Isso significa que você pode associar uma coleção de esquemas XML com a coluna do tipo **xml.** Todas as instâncias armazenadas na coluna são validadas e verificadas quanto ao tipo em relação ao esquema na coleção e fornecem a informação de tipo para a XQuery.|  
|||  
  
> [!NOTE]  
>  A organização dessa seção é baseada na especificação de working draft da XQuery da World Wide Web Consortium (W3C). Alguns dos diagramas fornecidos nesta seção foram obtidos nessa especificação. Esta seção compara a implementação XQuery da Microsoft com a especificação da W3C, descreve as diferenças entre a XQuery da Microsoft e da W3C e indica quais recursos da W3C não têm suporte. A especificação W3C [http://www.w3.org/TR/2004/WD-xquery-20040723](https://go.microsoft.com/fwlink/?LinkId=48846)está disponível em .  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Fundamentos de XQuery](../xquery/xquery-basics.md)|Fornece uma visão geral básica dos conceitos da XQuery, além da avaliação de expressão (contexto estático e dinâmico), atomização, valor booliano efetivo, sistema de tipo XQuery, correspondência de tipo de sequência e tratamento de erros.|  
|[Expressões XQuery](../xquery/xquery-expressions.md)|Descreve expressões primárias da XQuery, expressões de caminho, expressões de sequência, comparações aritméticas e expressões lógicas, construção da XQuery, expressão FLWOR, expressões quantificadas e condicionais e várias expressões em tipos de sequência.|  
|[Módulos e Prólogs &#40;&#41;xQuery](../xquery/modules-and-prologs-xquery.md)|Descreve o prólogo da XQuery.|  
|[Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)|Descreve uma lista das funções XQuery que têm suporte.|  
|[Operadores XQuery em relação ao tipo de dados xml](../xquery/xquery-operators-against-the-xml-data-type.md)|Descreve os operadores XQuery que têm suporte.|  
|[Exemplos adicionais de XQueries em relação ao tipo de dados xml](../xquery/additional-sample-xqueries-against-the-xml-data-type.md)|Fornece exemplos adicionais de XQuery.|  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;do servidor SQL de &#40;de dados XML](../relational-databases/xml/xml-data-sql-server.md)   
 [Coleções de esquemas XML &#40;&#41;do servidor SQL](../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
