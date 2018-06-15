---
title: Referência da linguagem XQuery (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XQuery
- XQuery, about XQuery
- xml data type [SQL Server], XQuery
- XML [SQL Server], XQuery
- queries [XML in SQL Server], XQuery
ms.assetid: 8a69344f-2990-4357-8160-cb26aac95b91
caps.latest.revision: 51
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 759904d735b754d9f51314b92c3d7763a0aa4ef2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33078163"
---
# <a name="xquery-language-reference-sql-server"></a>Referência de linguagem Xquery (SQL Server)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../includes/tsql-md.md)] oferece suporte a um subconjunto da linguagem XQuery que é usado para consultar o **xml** tipo de dados. Essa implementação da XQuery está alinhada com o Working Draft de julho de 2004 da XQuery. Essa linguagem está sendo desenvolvida pela World Wide Web Consortium (W3C), com a participação de todos os principais fornecedores de banco de dados e também da Microsoft. Como as especificações da W3C podem passar por revisões futuras antes de se tornarem recomendações da W3C, essa implementação pode ser diferente da recomendação final. Este tópico descreve a semântica e a sintaxe do subconjunto da XQuery com suporte no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Para obter mais informações, consulte o [W3C XQuery 1.0 Language Specification](http://go.microsoft.com/fwlink/?LinkId=48846).  
  
 A XQuery é uma linguagem que pode consultar dados XML estruturados ou semiestruturados. Com o **xml** suporte fornecido em tipo de dados de [!INCLUDE[ssDE](../includes/ssde-md.md)], documentos podem ser armazenados em um banco de dados e consultados usando XQuery.  
  
 A XQuery é baseada na linguagem XPath existente, com suporte adicional para uma melhor iteração, melhores resultados de classificação e com a capacidade de construir o XML necessário. A XQuery opera no modelo de dados XQuery. Essa é uma abstração de documentos XML e de resultados da XQuery podem ser com tipo ou sem-tipo. As informações de tipo são baseadas nos tipos fornecidos pela linguagem de esquema XML da W3C. Se nenhuma informação de tipo estiver disponível, a XQuery controlará os dados como sendo sem-tipo. Isso é semelhante ao modo como a versão 1.0 do XPath trata o XML.  
  
 Para consultar uma instância XML armazenada em uma variável ou coluna de **xml** tipo, use o [métodos de tipo de dados xml](../t-sql/xml/xml-data-type-methods.md). Por exemplo, você pode declarar uma variável de **xml** digite e consultá-la usando o **Query ()** método o **xml** tipo de dados.  
  
```  
DECLARE @x xml  
SET @x = '<ROOT><a>111</a></ROOT>'  
SELECT @x.query('/ROOT/a')  
```  
  
 No exemplo a seguir, a consulta é especificada na coluna Instructions de **xml** tipo na tabela ProductModel no banco de dados AdventureWorks.  
  
```  
SELECT Instructions.query('declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 O XQuery inclui a declaração de namespace, `declare namespace``AWMI=...`e a expressão de consulta, `/AWMI:root/AWMI:Location[@LocationID=10]`.  
  
 Observe que o XQuery é especificado na coluna Instructions de **xml** tipo. O [método Query ()](../t-sql/xml/query-method-xml-data-type.md) dos dados xml tipo é usado para especificar o XQuery.  
  
 A tabela a seguir lista os tópicos relacionados que podem ajudar a entender a implementação da XQuery no [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)|Explica o suporte para o **xml**no tipo de dados a [!INCLUDE[ssDE](../includes/ssde-md.md)] e os métodos que você pode usar em relação a esse tipo de dados. O **xml** formulários de modelo de dados XQuery de entrada na qual as expressões XQuery são executadas de tipo de dados.|  
|[Coleções de esquemas XML &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)|Descreve quais podem ser os tipos das instâncias XML armazenadas em um banco de dados. Isso significa que você pode associar uma coleção de esquemas XML com o **xml** coluna de tipo. Todas as instâncias armazenadas na coluna são validadas e verificadas quanto ao tipo em relação ao esquema na coleção e fornecem a informação de tipo para a XQuery.|  
|||  
  
> [!NOTE]  
>  A organização dessa seção é baseada na especificação de working draft da XQuery da World Wide Web Consortium (W3C). Alguns dos diagramas fornecidos nesta seção foram obtidos nessa especificação. Esta seção compara a implementação XQuery da Microsoft com a especificação da W3C, descreve as diferenças entre a XQuery da Microsoft e da W3C e indica quais recursos da W3C não têm suporte. A especificação do W3C está disponível em [ http://www.w3.org/TR/2004/WD-xquery-20040723 ](http://go.microsoft.com/fwlink/?LinkId=48846).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Fundamentos de XQuery](../xquery/xquery-basics.md)|Fornece uma visão geral básica dos conceitos da XQuery, além da avaliação de expressão (contexto estático e dinâmico), atomização, valor booliano efetivo, sistema de tipo XQuery, correspondência de tipo de sequência e tratamento de erros.|  
|[Expressões XQuery](../xquery/xquery-expressions.md)|Descreve expressões primárias da XQuery, expressões de caminho, expressões de sequência, comparações aritméticas e expressões lógicas, construção da XQuery, expressão FLWOR, expressões quantificadas e condicionais e várias expressões em tipos de sequência.|  
|[Módulos e Prólogos &#40;XQuery&#41;](../xquery/modules-and-prologs-xquery.md)|Descreve o prólogo da XQuery.|  
|[Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)|Descreve uma lista das funções XQuery que têm suporte.|  
|[Operadores XQuery em relação ao Tipo de Dados XML](../xquery/xquery-operators-against-the-xml-data-type.md)|Descreve os operadores XQuery que têm suporte.|  
|[Exemplos Adicionais de XQueries em relação ao Tipo de Dados XML](../xquery/additional-sample-xqueries-against-the-xml-data-type.md)|Fornece exemplos adicionais de XQuery.|  
  
## <a name="see-also"></a>Consulte também  
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Coleções de esquemas XML &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
