---
title: "Prólogo do XQuery | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
- namespaces [XQuery]
- default namespace declarations
ms.assetid: 03924684-c5fd-44dc-8d73-c6ab90f5e069
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 38b0c622448c2a46e9b7ecbe38c01b7e522c4ec6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="modules-and-prologs---xquery-prolog"></a>Módulos e Prólogos - prólogo do XQuery
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Uma consulta XQuery é composta de prólogo e corpo. O prólogo do XQuery é uma série de declarações e definições que juntas criam o ambiente exigido para o processamento de consulta. No SQL Server, o prólogo do Xquery pode incluir declarações de namespace. O corpo do XQuery é constituído de uma sequência de expressões que especificam o resultado da consulta desejada.  
  
 Por exemplo, o XQuery a seguir é especificado na coluna Instructions de **xml** tipo que armazena instruções de fabricação como XML. A consulta recupera as instruções de produção para o local de centro de trabalho `10`. O `query()` método o **xml** tipo de dados é usado para especificar o XQuery.  
  
```  
SELECT Instructions.query('declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') AS Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O prólogo do XQuery inclui uma declaração de prefixo (AWMI) do namespace, `(namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";`.  
  
-   A palavra-chave `declare namespace` define um prefixo de namespace que depois é usado no corpo da consulta.  
  
-   `/AWMI:root/AWMI:Location[@LocationID="10"]` é o corpo da consulta.  
  
## <a name="namespace-declarations"></a>Declarações de namespace  
 Uma declaração de namespace define um prefixo e o associa a um namespace URI, como mostrado na consulta a seguir. Na consulta, `CatalogDescription` é um **xml** coluna de tipo.  
  
 Ao especificar o XQuery nessa coluna, o prólogo da consulta especifica a declaração `declare namespace` para associar o prefixo `PD`, descrição de produto, ao namespace URI. Esse prefixo é então usado no corpo da consulta em vez do namespace URI. Os nós no XML resultante estão no namespace associado com o namespace URI.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /PD:ProductDescription/PD:Summary   
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Para melhorar a legibilidade da consulta, você pode declarar namespaces usando WITH XMLNAMESPACES em vez de declarar o prefixo e a associação de namespace no prólogo da consulta utilizando `declare namespace`.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
  
SELECT CatalogDescription.query('  
         /PD:ProductDescription/PD:Summary   
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Para obter mais informações, consulte, [adicionar Namespaces a consultas com WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md).  
  
### <a name="default-namespace-declaration"></a>Declarações de namespace padrão  
 Em vez de declarar um prefixo de namespace usando a declaração `declare namespace`, você pode usar a declaração `declare default element namespace` para associar um namespace padrão a nomes de elemento. Nesse caso, você não especifica nenhum prefixo.  
  
 No exemplo a seguir, a expressão de caminho no corpo da consulta não especifica um prefixo de namespace. Por padrão, todos os nomes de elementos pertencem ao namespace padrão especificado no prólogo.  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace  "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
        /ProductDescription/Summary   
    ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=19   
```  
  
 Você pode declarar um namespace padrão usando WITH XMLNAMESPACES:  
  
```  
WITH XMLNAMESPACES (DEFAULT 'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription')  
SELECT CatalogDescription.query('  
        /ProductDescription/Summary   
    ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=19   
```  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)  
  
  

