---
title: "Operação de comandos sem parâmetros | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a025cf381bdf5a51cb825294bf5a5399fc033b2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="operation-of-non-parameterized-commands"></a>Operação de comandos sem parâmetros
Para comandos sem parâmetros, todos os comandos do provedor são executados e o **conjuntos de registros** são criados durante a execução do comando. Se o comando é executado de forma síncrona, todos os **conjuntos de registros** será totalmente preenchida. Se um modo de população assíncrona foi selecionado, o estado preenchido do **conjuntos de registros** dependerá do modo de preenchimento e o tamanho do **conjuntos de registros**.  
  
 Por exemplo, o *comando pai* poderia retornar um **registros** de clientes para uma empresa de uma tabela de clientes e o *filho comando* poderia retornar um **Registros** de pedidos para todos os clientes de uma tabela de pedidos.  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 Para relações pai-filho sem parâmetros, cada pai e filho **registros** objeto deve ter uma coluna em comum para associá-los. As colunas são nomeadas na cláusula RELATE, *coluna pai* primeiro e, em seguida, *coluna filho*. As colunas podem ter nomes diferentes em suas respectivas **registros** objetos, mas deve se referir às mesmas informações para especificar uma relação significativa. Por exemplo, o **clientes** e **pedidos Recordset** objetos poderia ter um campo customerID. Porque a associação do filho **registros** é determinado pelo comando de provedor, o filho **registros** pode conter linhas órfãs. Essas linhas órfãos podem ser acessadas sem reformatação adicionais.  
  
 Modelagem de dados acrescenta uma coluna de capítulo pai **registros**. Os valores na coluna de capítulo são referências às linhas no filho **registros**, que atendem a cláusula RELATE. Ou seja, o mesmo valor é no *coluna pai* de uma linha pai especificado já está no *coluna filho* de todas as linhas do filho capítulo. Quando várias cláusulas TO são usadas na mesma cláusula RELATE, eles são implicitamente combinados usando um operador AND. Se as colunas pai na cláusula RELATE não constituem uma chave para o pai **registros**, uma linha filho único pode ter várias linhas pai.  
  
 Quando você acessa a referência da coluna de capítulo, ADO automaticamente recupera o **registros** representado pela referência de. Observe que em um comando sem parâmetros, embora o filho todo **registros** foi recuperado, o capítulo apresenta somente um subconjunto de linhas.  
  
 Se não tiver nenhuma coluna acrescentada *capítulo alias*, um nome será gerado para que ele automaticamente. Um [campo](../../../ado/reference/ado-api/field-object.md) do objeto para a coluna será acrescentada ao **registros** do objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleta e seu tipo de dados será **adChapter**.  
  
 Para obter informações sobre como navegar hierárquico **registros**, consulte [acessar linhas em um conjunto de registros hierárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelagem de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
