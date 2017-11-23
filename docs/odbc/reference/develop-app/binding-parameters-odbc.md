---
title: "Associação de parâmetros ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e0994006c2e99c8f1e454eaf07b74fffcee70e9f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="binding-parameters-odbc"></a>Associação de parâmetros ODBC
Cada parâmetro em uma instrução SQL deve ser associado, ou *associado,* a uma variável no aplicativo antes da instrução é executada. Quando o aplicativo associa uma variável para um parâmetro, ele descreve essa variável, endereço, tipo de dados C e assim por diante — para o driver. Ele também descreve o próprio parâmetro — dados SQL tipo, precisão e assim por diante. O driver armazena essas informações na estrutura, ele mantém para essa instrução e usa as informações para recuperar o valor da variável quando a instrução é executada.  
  
 Parâmetros podem ser associados ou reassociados a qualquer momento antes de uma instrução é executada. Se um parâmetro é vinculada outra vez depois de uma instrução é executada, a associação não se aplica até que a instrução é executada novamente. Para associar um parâmetro a uma variável diferente, um aplicativo simplesmente reconecta o parâmetro com a nova variável; a associação anterior é liberada automaticamente.  
  
 Uma variável permanece associada a um parâmetro até que uma variável diferente está associada ao parâmetro, até que todos os parâmetros são desassociados chamando **SQLFreeStmt** com a opção SQL_RESET_PARAMS ou até que a instrução seja liberada. Por esse motivo, o aplicativo deve ser-se de que variáveis não são liberadas até depois que eles serão desvinculados. Para obter mais informações, consulte [Allocating e liberar Buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Como as associações de parâmetro são apenas informações armazenadas na estrutura da mantidas pelo driver para a instrução, eles podem ser definidos em qualquer ordem. Eles também são independentes da instrução SQL que é executada. Por exemplo, suponha que um aplicativo associa três parâmetros e, em seguida, executa a instrução SQL a seguir:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Se o aplicativo imediatamente executa a instrução SQL  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 no mesmo identificador de instrução, associações de parâmetro para o **inserir** instrução são usados porque essas são as associações armazenadas na estrutura de instrução. Na maioria dos casos, isso é uma prática de programação ruim e deve ser evitado. Em vez disso, o aplicativo deve chamar **SQLFreeStmt** com a opção SQL_RESET_PARAMS desassociar todos os parâmetros antigos e, em seguida, associe novos.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Marcadores de parâmetro de associação](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Parâmetros de associação por nome (parâmetros nomeados)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Deslocamentos de associação de parâmetro](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descrevendo parâmetros](../../../odbc/reference/develop-app/describing-parameters.md)
