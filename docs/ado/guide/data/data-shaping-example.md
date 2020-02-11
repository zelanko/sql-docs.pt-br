---
title: Exemplo de modelagem de dados | Microsoft Docs
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
ms.openlocfilehash: a946329ad95a2b226f186e571152268baa5f37c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925665"
---
# <a name="data-shaping-example"></a>Exemplo de data shaping
O comando de formatação de dados a seguir demonstra como criar um **conjunto de registros** hierárquico das tabelas **Customers** e **Orders** no banco de dados Northwind.  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 Quando esse comando é usado para abrir um objeto **Recordset** (conforme mostrado na [Visual Basic exemplo de data Shaping](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)), ele cria um capítulo (**chapOrders**) para cada registro retornado da tabela **Customers** . Este capítulo consiste em um subconjunto do conjunto de **registros** retornado da tabela **Orders** . O capítulo **chapOrders** contém todas as informações solicitadas sobre os pedidos feitos pelo cliente determinado. Neste exemplo, o capítulo consiste em três colunas: **OrderID**, **OrderDate**e **CustomerID**.  
  
 As duas primeiras entradas do **conjunto de registros** moldado resultante são as seguintes:  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 Em um comando de forma, APPEND é usado para criar um **conjunto de registros** filho relacionado ao **conjunto de registros** pai (como retornado do comando específico do provedor imediatamente após a palavra-chave Shape que foi discutida anteriormente) pela cláusula relate. O pai e o filho normalmente têm pelo menos uma coluna em comum: o valor da coluna em uma linha do pai é o mesmo que o valor da coluna em todas as linhas do filho.  
  
 Há uma segunda maneira de usar comandos de forma: ou seja, para gerar um **conjunto de registros** pai de um **conjunto de registros**filho. Os registros no conjunto de **registros** filho são agrupados, normalmente usando a cláusula by, e uma linha é adicionada ao conjunto de **registros** pai para cada grupo resultante no filho. Se a cláusula BY for omitida, o **conjunto de registros** filho formará um único grupo e o **conjunto de registros** pai conterá exatamente uma linha. Isso é útil para computar agregações "total geral" em todo o **conjunto de registros**filho.  
  
 A construção de comando SHAPE também permite criar programaticamente um **conjunto de registros**moldado. Você pode acessar os componentes do conjunto de **registros** programaticamente ou por meio de um controle visual apropriado. Um comando de forma é emitido como qualquer outro texto de comando do ADO. Para obter mais informações, consulte os [comandos de forma em geral](../../../ado/guide/data/shape-commands-in-general.md).  
  
 Independentemente da forma como o **conjunto de registros** pai é formado, ele conterá uma coluna de capítulo que é usada para relacioná-la a um **conjunto de registros**filho. Se desejar, o conjunto de **registros** pai também poderá ter colunas que contêm agregações (Sum, min, Max e assim por diante) nas linhas filhas. O **conjunto de registros** pai e filho pode ter colunas que contêm uma expressão na linha no conjunto de **registros**, bem como colunas novas e inicialmente vazias.  
  
 Esta seção continua com o tópico a seguir.  
  
-   [Exemplo de data shaping do Visual Basic](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
