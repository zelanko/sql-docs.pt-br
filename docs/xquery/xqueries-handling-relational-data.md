---
title: Manipulação de dados relacionais de XQueries | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
author: rothja
ms.author: jroth
ms.openlocfilehash: ed4583b30ed1e4538a36079f9f7794704b819cda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946164"
---
# <a name="xqueries-handling-relational-data"></a>XQueries que manipulam dados relacionais
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Especifique o XQuery em relação a um **xml** coluna de tipo ou variável, usando uma da [métodos de tipo de dados XML](../t-sql/xml/xml-data-type-methods.md). Eles incluem **Query ()** , **Value ()** , **exist ()** , ou **Modify ()** . A XQuery é executada na instância de XML identificada na consulta que está gerando o XML.  
  
 O XML gerado pela execução de XQuery pode incluir valores recuperados de outras variáveis ou colunas de conjunto de linhas Transact-SQL. Para associar os dados relacionais não XML ao XML resultante, o SQL Server fornece as pseudofunções seguintes como extensões XQuery:  
  
-   **sql:column()** function  
  
-   **SQL: Variable** função  
  
 Você pode usar essas extensões XQuery ao especificar um XQuery na **Query ()** método o **xml** tipo de dados. Como resultado, o **Query ()** método pode produzir XML que combina dados de XML e não-**xml** tipos de dados.  
  
 Você também pode usar essas funções quando você usa o **xml** métodos de tipo de dados **Modify ()** , **Value ()** , **Query ()** , e  **exist ()** para expor um valor relacional dentro do XML.  
  
 Para obter mais informações, consulte [função SQL: Column (XQuery)](../xquery/xquery-extension-functions-sql-column.md) e [função SQL: Variable (XQuery)](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="see-also"></a>Consulte também  
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Construção XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
