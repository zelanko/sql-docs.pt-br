---
title: "Manipulação de dados relacionais de XQueries | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 447ffa853f8a5b6a257cc7e2918feaddcbde8a0f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="xqueries-handling-relational-data"></a>XQueries que manipulam dados relacionais
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Você especifica XQuery em uma **xml** coluna de tipo ou variável, usando uma da [métodos de tipo de dados XML](../t-sql/xml/xml-data-type-methods.md). Isso inclui **Query ()**, **Value ()**, **exist ()**, ou **Modify ()**. A XQuery é executada na instância de XML identificada na consulta que está gerando o XML.  
  
 O XML gerado pela execução de XQuery pode incluir valores recuperados de outras variáveis ou colunas de conjunto de linhas Transact-SQL. Para associar os dados relacionais não XML ao XML resultante, o SQL Server fornece as pseudofunções seguintes como extensões XQuery:  
  
-   **SQL: Column** função  
  
-   **SQL: Variable** função  
  
 Você pode usar essas extensões XQuery ao especificar um XQuery no **Query ()** método o **xml** tipo de dados. Como resultado, o **Query ()** método pode produzir XML que combina dados de XML e não-**xml** tipos de dados.  
  
 Você também pode usar essas funções quando você usa o **xml** métodos de tipo de dados **Modify ()**, **Value ()**, **Query ()**, e  **exist ()**para expor um valor relacional dentro do XML.  
  
 Para obter mais informações, consulte [função SQL: Column (XQuery)](../xquery/xquery-extension-functions-sql-column.md) e [função SQL: Variable (XQuery)](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="see-also"></a>Consulte também  
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Construção XML &#40; XQuery &#41;](../xquery/xml-construction-xquery.md)  
  
  
