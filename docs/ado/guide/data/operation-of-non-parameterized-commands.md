---
title: Operação de comandos não parametrizados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3512b484425749ed027f6533dab7398765c1af2e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924743"
---
# <a name="operation-of-non-parameterized-commands"></a>Operação de comandos não parametrizados
Para comandos não parametrizados, todos os comandos do provedor são executados e os **conjuntos de registros** são criados durante a execução do comando. Se o comando for executado de forma síncrona, todos os **conjuntos de registros** serão totalmente preenchidos. Se um modo de população assíncrona tiver sido selecionado, o estado preenchido dos **conjuntos de registros** dependerá do modo de população e do tamanho dos **conjuntos de registros**.  
  
 Por exemplo, o *comando pai* pode retornar um **conjunto de registros** de clientes para uma empresa de uma tabela de clientes, e o *comando filho* poderia retornar um **conjunto de registros** de pedidos para todos os clientes de uma tabela de pedidos.  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 Para relações pai-filho não parametrizadas, cada objeto de conjunto de **registros** pai e filho deve ter uma coluna em comum para associá-los. As colunas são nomeadas na cláusula relate, primeiro *pai-Column* e depois *filho-Column*. As colunas podem ter nomes diferentes em seus respectivos objetos **Recordset** , mas devem se referir às mesmas informações para especificar uma relação significativa. Por exemplo, os objetos do conjunto de registros **Customers** e **Orders** podem ter um campo CustomerID. Como a associação do conjunto de **registros** filho é determinada pelo comando do provedor, o **conjunto de registros** filho pode conter linhas órfãs. Essas linhas órfãs são inacessíveis sem remodelagem adicional.  
  
 A modelagem de dados acrescenta uma coluna de capítulo ao **conjunto de registros**pai. Os valores na coluna capítulo são referências a linhas no **conjunto de registros**filho, que satisfazem a cláusula relate. Ou seja, o mesmo valor está na *coluna pai* de uma determinada linha pai como está na *coluna filho* de todas as linhas do filho do capítulo. Quando várias cláusulas TO são usadas na mesma cláusula relate, elas são implicitamente combinadas usando um operador AND. Se as colunas pai na cláusula relate não constituem uma chave para o conjunto de **registros**pai, uma única linha filho pode ter várias linhas pai.  
  
 Quando você acessa a referência na coluna capítulo, o ADO recupera automaticamente o **conjunto de registros** representado pela referência. Observe que em um comando não parametrizado, embora todo o conjunto de **registros** filho tenha sido recuperado, o capítulo apresenta apenas um subconjunto de linhas.  
  
 Se a coluna acrescentada não tiver um *alias de Chapter*, um nome será gerado automaticamente. Um objeto de [campo](../../../ado/reference/ado-api/field-object.md) para a coluna será anexado à coleção de [campos](../../../ado/reference/ado-api/fields-collection-ado.md) do objeto **Recordset** e seu tipo de dados será **adChapter**.  
  
 Para obter informações sobre como navegar em um **conjunto de registros**hierárquico, consulte [acessando linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de formatação de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
