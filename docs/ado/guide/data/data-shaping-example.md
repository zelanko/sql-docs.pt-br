---
title: "Exemplo de formatação de dados | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ac91d7a7e962443e9798b5b2ecf2daf80ee72eb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="data-shaping-example"></a>Exemplo de modelagem de dados
Os seguintes dados de formatação comando demonstra como criar um hierárquica **registros** do **clientes** e **pedidos** tabelas no banco de dados Northwind.  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 Quando esse comando é usado para abrir um **registros** objeto (conforme mostrado na [Visual Basic exemplo de modelagem de dados](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)), ele cria um capítulo (**chapOrders**) para cada registro retornado do **clientes** tabela. Este capítulo consiste em um subconjunto do **registros** retornado do **pedidos** tabela. O **chapOrders** capítulo contém todas as informações solicitadas sobre os pedidos feitos pelo cliente específico. Neste exemplo, o capítulo consiste em três colunas: **OrderID**, **OrderDate**, e **CustomerID**.  
  
 As duas primeiras entradas dos resultantes em forma de **registros** são da seguinte maneira:  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 Em um comando de forma, ACRESCENTAR é usado para criar um filho **registros** relacionadas ao pai **registros** (conforme retornado do comando específico do provedor imediatamente após a palavra-chave forma foi abordado anteriores) pela cláusula RELATE. O pai e filho normalmente têm pelo menos uma coluna em comum: O valor da coluna em uma linha do pai é igual ao valor da coluna em todas as linhas do filho.  
  
 Há uma segunda maneira de usar os comandos de forma: ou seja, para gerar um pai **registros** de filho **registros**. Os registros no filho **registros** são agrupados, normalmente usando a cláusula BY e uma linha é adicionada ao pai **registros** para cada grupo resultante do filho. Se a cláusula BY for omitida, o filho **registros** será o formulário de um único grupo e o pai **registros** irá conter exatamente uma linha. Isso é útil para computar agregações de "total geral" em todo filho **registros**.  
  
 A construção do comando de forma também permite que você criar programaticamente um moldado **registros**. Você pode acessar os componentes do **registros** programaticamente ou por meio de um controle visual apropriado. Um comando de forma é emitido como qualquer outro texto de comando do ADO. Para obter mais informações, consulte [forma comandos em geral](../../../ado/guide/data/shape-commands-in-general.md).  
  
 Independentemente da maneira como o pai **registros** é formado, ele conterá uma coluna de capítulo que é usada para relacioná-la a um filho **registros**. Se você quiser, o pai **registros** também pode ter colunas que contêm agregações (SUM, MIN, MAX e assim por diante) sobre as linhas filho. O pai e filho **registros** pode ter colunas que contêm uma expressão na linha a **Recordset**, bem como as colunas que são novos e inicialmente vazia.  
  
 Esta seção continua com o tópico a seguir.  
  
-   [Exemplo de data shaping do Visual Basic](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
