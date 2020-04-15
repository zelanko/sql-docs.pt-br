---
title: Parâmetros de ligação ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e314bb9e3a1a979976a450e2a45a286ec54dfe7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306377"
---
# <a name="binding-parameters-odbc"></a>Associar parâmetros ODBC
Cada parâmetro em uma declaração SQL deve ser associado, ou *vinculado,* a uma variável no aplicativo antes da declaração ser executada. Quando o aplicativo vincula uma variável a um parâmetro, ele descreve essa variável - endereço, tipo de dados C, e assim por diante - ao driver. Ele também descreve o parâmetro em si - tipo de dados SQL, precisão, e assim por diante. O motorista armazena essas informações na estrutura que mantém para essa declaração e usa as informações para recuperar o valor da variável quando a declaração é executada.  
  
 Os parâmetros podem ser limitados ou ressurgir a qualquer momento antes que uma declaração seja executada. Se um parâmetro for recuperado após a execução de uma declaração, a vinculação não se aplicará até que a declaração seja executada novamente. Para vincular um parâmetro a uma variável diferente, um aplicativo simplesmente religa o parâmetro com a nova variável; a vinculação anterior é liberada automaticamente.  
  
 Uma variável permanece vinculada a um parâmetro até que uma variável diferente esteja vinculada ao parâmetro, até que todos os parâmetros sejam desvinculados ligando para **SQLFreeStmt** com a opção SQL_RESET_PARAMS, ou até que a declaração seja liberada. Por essa razão, a aplicação deve ter certeza de que as variáveis não são liberadas até que elas sejam desvinculadas. Para obter mais informações, consulte [Alocando e Liberando Buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Como as ligações de parâmetros são apenas informações armazenadas na estrutura mantida pelo motorista para a declaração, elas podem ser definidas em qualquer ordem. Eles também são independentes da declaração SQL que é executada. Por exemplo, suponha que um aplicativo vincule três parâmetros e execute a seguinte declaração SQL:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Se o aplicativo executar imediatamente a declaração SQL  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 na mesma alça de instrução, as amarras dos parâmetros para a instrução **INSERT** são usadas porque essas são as amarras armazenadas na estrutura da declaração. Na maioria dos casos, esta é uma prática de programação ruim e deve ser evitada. Em vez disso, o aplicativo deve chamar **SQLFreeStmt** com a opção SQL_RESET_PARAMS de desvincular todos os parâmetros antigos e, em seguida, vincular novos.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Marcadores de parâmetro de associação](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Parâmetros de associação por nome (parâmetros nomeados)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Deslocamentos de associação de parâmetro](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descrever parâmetros](../../../odbc/reference/develop-app/describing-parameters.md)
