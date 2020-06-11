---
title: XQueries manipulando dados relacionais | Microsoft Docs
description: 'Saiba como associar dados relacionais não XML a XML usando as extensões XQuery SQL: Column () e SQL: variable ().'
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
ms.openlocfilehash: e9f1e69c10e4930a4a039528cffc4dbb13a67548
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689478"
---
# <a name="xqueries-handling-relational-data"></a>XQueries que manipulam dados relacionais
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Você especifica XQuery em uma coluna ou variável de tipo **XML** usando um dos [métodos de tipo de dados XML](../t-sql/xml/xml-data-type-methods.md). Isso inclui **Query ()**, **Value ()**, **exist ()** ou **Modify ()**. A XQuery é executada na instância de XML identificada na consulta que está gerando o XML.  
  
 O XML gerado pela execução de XQuery pode incluir valores recuperados de outras variáveis ou colunas de conjunto de linhas Transact-SQL. Para associar os dados relacionais não XML ao XML resultante, o SQL Server fornece as pseudofunções seguintes como extensões XQuery:  
  
-   **sql:column()** function  
  
-   **SQL: função Variable ()**  
  
 Você pode usar essas extensões XQuery ao especificar um XQuery no método **Query ()** do tipo de dados **XML** . Como resultado, o método **Query ()** pode produzir XML que combina dados de tipos de dados XML e não**XML** .  
  
 Você também pode usar essas funções ao usar os métodos de tipo de dados **XML** **Modify ()**, **Value ()**, **Query ()** e **exist ()** para expor um valor relacional dentro de XML.  
  
 Para obter mais informações, consulte a função [SQL: Column () (XQuery)](../xquery/xquery-extension-functions-sql-column.md) e [SQL: variable () (XQuery)](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;de dados XML SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Construção XML &#40;&#41;XQuery](../xquery/xml-construction-xquery.md)  
  
  
