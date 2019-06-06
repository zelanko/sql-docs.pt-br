---
title: Exemplo de Data Shaping | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5690b104cea4cf29cb51c77d8dc8554dd5a31d50
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701108"
---
# <a name="data-shaping-example"></a>Exemplo de data shaping
Os dados moldando o comando a seguir demonstra como criar um hierárquica **conjunto de registros** da **clientes** e **pedidos** tabelas no banco de dados Northwind.  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 Quando esse comando é usado para abrir um **conjunto de registros** objeto (como mostrado na [exemplo de Visual Basic de Data Shaping](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)), ele cria um capítulo (**chapOrders**) para cada registro retornado dos **clientes** tabela. Este capítulo consiste em um subconjunto do **conjunto de registros** retornados da **pedidos** tabela. O **chapOrders** capítulo contém todas as informações solicitadas sobre os pedidos feitos pelo cliente determinado. Neste exemplo, o capítulo consiste em três colunas: **OrderID**, **OrderDate**, e **CustomerID**.  
  
 As duas primeiras entradas do resultante em forma **Recordset** são da seguinte maneira:  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 Em um comando de forma, ACRÉSCIMO é usado para criar um filho **conjunto de registros** relacionados para o pai **Recordset** (conforme retornado do comando específico do provedor imediatamente após a palavra-chave forma que foi discutida anteriormente) pela cláusula RELATE. O pai e filho normalmente têm pelo menos uma coluna em comum: O valor da coluna em uma linha do pai é o mesmo que o valor da coluna em todas as linhas do filho.  
  
 Há outra maneira de usar comandos de forma: ou seja, para gerar um pai **conjunto de registros** de um filho **conjunto de registros**. Os registros do filho **conjunto de registros** são agrupados, normalmente usando a cláusula BY e uma linha é adicionada ao pai **Recordset** para cada grupo resultante do filho. Se a cláusula BY for omitida, o filho **conjunto de registros** será o formulário de um único grupo e o pai **Recordset** irá conter exatamente uma linha. Isso é útil para computar agregações de "total geral" sobre o filho todo **conjunto de registros**.  
  
 A construção do comando de forma também permite que você criar programaticamente um moldado **conjunto de registros**. Em seguida, você pode acessar os componentes do **Recordset** programaticamente ou por meio de um controle visual apropriado. Um comando de forma é emitido como qualquer outro texto de comando do ADO. Para obter mais informações, consulte [comandos de forma em geral](../../../ado/guide/data/shape-commands-in-general.md).  
  
 Independentemente de qual modo o pai **conjunto de registros** é formado, ele conterá uma coluna de capítulo que é usada para relacioná-la a um filho **conjunto de registros**. Se você quiser, o pai **Recordset** também pode ter colunas que contêm agregações (SUM, MIN, MAX e assim por diante) em relação às linhas filho. O pai e filho **conjunto de registros** podem ter colunas que contêm uma expressão na linha a **conjunto de registros**, bem como as colunas que são novos e inicialmente vazio.  
  
 Esta seção continua com o tópico a seguir.  
  
-   [Exemplo de data shaping do Visual Basic](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
