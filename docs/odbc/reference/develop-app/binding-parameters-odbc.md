---
title: Associando parâmetros ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d62c0864678e116e30a0673bdf2625d70de0cedd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501779"
---
# <a name="binding-parameters-odbc"></a>Associar parâmetros ODBC
Cada parâmetro em uma instrução SQL deve ser associado, ou *associado,* a uma variável no aplicativo antes da instrução é executada. Quando o aplicativo é associado a uma variável a um parâmetro, ele descreve o endereço, tipo de dados C e assim por diante - essa variável para o driver. Ele também descreve o próprio parâmetro - tipo de dados SQL, precisão e assim por diante. O driver armazena essas informações na estrutura, ele mantém para essa instrução e usa as informações para recuperar o valor da variável quando a instrução é executada.  
  
 Parâmetros podem ser associados ou se a qualquer momento antes de uma instrução é executada. Se um parâmetro é ligado novamente depois que uma instrução é executada, a associação não se aplica até que a instrução é executada novamente. Para associar um parâmetro a uma variável diferente, um aplicativo simplesmente associa novamente o parâmetro com a nova variável; a associação anterior é liberada automaticamente.  
  
 Uma variável permanece associada a um parâmetro até que uma variável diferente é associada ao parâmetro, até que todos os parâmetros são desassociados chamando **SQLFreeStmt** com a opção SQL_RESET_PARAMS, ou até que a instrução seja liberada. Por esse motivo, o aplicativo deve ser-se de que as variáveis não são liberadas até depois que eles serão desvinculados. Para obter mais informações, consulte [alocando e liberando Buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Como as associações de parâmetro são apenas as informações armazenadas na estrutura mantida pelo driver para a instrução, elas podem ser definidas em qualquer ordem. Eles também são independentes da instrução SQL que é executada. Por exemplo, suponha que um aplicativo associa três parâmetros e, em seguida, executa a instrução SQL a seguir:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Se o aplicativo imediatamente executa a instrução SQL  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 no mesmo identificador de instrução, associações de parâmetro para o **inserir** instrução são usados porque essas são as associações armazenadas na estrutura da instrução. Na maioria dos casos, isso é uma prática inadequada de programação e deve ser evitado. Em vez disso, o aplicativo deve chamar **SQLFreeStmt** com a opção SQL_RESET_PARAMS desvincular todos os parâmetros antigos e, em seguida, associar novas.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Marcadores de parâmetro de associação](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Parâmetros de associação por nome (parâmetros nomeados)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Deslocamentos de associação de parâmetro](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descrevendo parâmetros](../../../odbc/reference/develop-app/describing-parameters.md)
