---
title: XQueries manipulando dados relacionais | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67946164"
---
# <a name="xqueries-handling-relational-data"></a>XQueries que manipulam dados relacionais
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Você especifica XQuery em uma coluna ou variável de tipo **XML** usando um dos [métodos de tipo de dados XML](../t-sql/xml/xml-data-type-methods.md). Isso inclui **Query ()**, **Value ()**, **exist ()** ou **Modify ()**. A XQuery é executada na instância de XML identificada na consulta que está gerando o XML.  
  
 O XML gerado pela execução de XQuery pode incluir valores recuperados de outras variáveis ou colunas de conjunto de linhas Transact-SQL. Para associar os dados relacionais não XML ao XML resultante, o SQL Server fornece as pseudofunções seguintes como extensões XQuery:  
  
-   função **SQL: Column ()**  
  
-   **SQL: função Variable ()**  
  
 Você pode usar essas extensões XQuery ao especificar um XQuery no método **Query ()** do tipo de dados **XML** . Como resultado, o método **Query ()** pode produzir XML que combina dados de tipos de dados XML e não**XML** .  
  
 Você também pode usar essas funções ao usar os métodos de tipo de dados **XML** **Modify ()**, **Value ()**, **Query ()** e **exist ()** para expor um valor relacional dentro de XML.  
  
 Para obter mais informações, consulte a função [SQL: Column () (XQuery)](../xquery/xquery-extension-functions-sql-column.md) e [SQL: variable () (XQuery)](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Construção XML &#40;&#41;XQuery](../xquery/xml-construction-xquery.md)  
  
  
