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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924743"
---
# <a name="operation-of-non-parameterized-commands"></a>Operação de comandos não parametrizados
Para os comandos não parametrizados, todos os comandos do provedor são executados e o **conjuntos de registros** são criados durante a execução do comando. Se o comando é executado de forma síncrona, todos os **conjuntos de registros** será totalmente preenchida. Se um modo de população assíncrona tiver sido selecionado, o estado de preenchida do **conjuntos de registros** dependerá do modo de preenchimento e o tamanho do **conjuntos de registros**.  
  
 Por exemplo, o *comando pai* poderia retornar um **conjunto de registros** de clientes para uma empresa de uma tabela de clientes e o *filho comando* poderia retornar um **Recordset** de pedidos para todos os clientes de uma tabela Pedidos.  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 Para relações pai-filho sem parâmetros, cada pai e filho **Recordset** objeto deve ter uma coluna em comum para associá-los. As colunas são nomeadas na cláusula RELATE, *coluna pai* primeiro e, em seguida *coluna filho*. As colunas podem ter nomes diferentes em seus respectivos **Recordset** objetos, mas deve se referir às mesmas informações para especificar uma relação significativa. Por exemplo, o **clientes** e **conjunto de registros de ordens** objetos poderia têm um campo customerID. Porque a associação do filho **conjunto de registros** é determinado pelo comando de provedor, o filho **Recordset** pode conter linhas órfãs. Essas linhas órfãs estão inacessíveis sem remodelagem adicionais.  
  
 Formatação de dados acrescenta uma coluna de capítulo para o pai **conjunto de registros**. Os valores na coluna de capítulo são referências às linhas no filho **Recordset**, que atendem a cláusula RELATE. Ou seja, o mesmo valor está no *coluna pai* de uma linha pai fornecido como está no *coluna filho* de todas as linhas do filho do capítulo. Quando várias cláusulas TO são usadas na mesma cláusula RELATE, eles implicitamente são combinados usando um operador AND. Se as colunas pai na cláusula RELATE não constituem uma chave para o pai **Recordset**, uma linha filho único pode ter várias linhas pai.  
  
 Quando você acessa a referência na coluna de capítulo, ADO recupera automaticamente a **Recordset** representado pela referência. Observe que, em um comando sem parâmetros, embora o filho todo **Recordset** tiver sido recuperado, o capítulo apresenta apenas um subconjunto de linhas.  
  
 Se não tiver nenhuma coluna acrescentada *capítulo alias*, um nome será gerado para ele automaticamente. Um [campo](../../../ado/reference/ado-api/field-object.md) do objeto para a coluna será acrescentada à **conjunto de registros** do objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleta e seu tipo de dados será **adChapter**.  
  
 Para obter informações sobre como navegar de modo hierárquico **conjunto de registros**, consulte [acessar linhas em um conjunto de registros hierárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
