---
title: Parâmetros de associação ODBC | Microsoft Docs
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
ms.openlocfilehash: 1bc40d4800e7cd013b7ac908400c0492286314e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107631"
---
# <a name="binding-parameters-odbc"></a>Associar parâmetros ODBC
Cada parâmetro em uma instrução SQL deve ser *associado ou associado* a uma variável no aplicativo antes que a instrução seja executada. Quando o aplicativo associa uma variável a um parâmetro, ele descreve o endereço de variável, o tipo de dados C e assim por diante – para o driver. Ele também descreve o próprio parâmetro-tipo de dados SQL, precisão e assim por diante. O driver armazena essas informações na estrutura que ela mantém para essa instrução e usa as informações para recuperar o valor da variável quando a instrução é executada.  
  
 Os parâmetros podem ser associados ou reassociados a qualquer momento antes de uma instrução ser executada. Se um parâmetro for reassociado depois que uma instrução for executada, a associação não se aplicará até que a instrução seja executada novamente. Para associar um parâmetro a uma variável diferente, um aplicativo simplesmente reassocia o parâmetro à nova variável; a Associação anterior é liberada automaticamente.  
  
 Uma variável permanece associada a um parâmetro até que uma variável diferente seja associada ao parâmetro, até que todos os parâmetros sejam desassociados chamando **SQLFreeStmt** com a opção SQL_RESET_PARAMS ou até que a instrução seja liberada. Por esse motivo, o aplicativo deve ter certeza de que as variáveis não serão liberadas até que elas sejam desassociadas. Para obter mais informações, consulte [alocando e liberando buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Como as associações de parâmetro são apenas informações armazenadas na estrutura mantida pelo driver para a instrução, elas podem ser definidas em qualquer ordem. Eles também são independentes da instrução SQL que é executada. Por exemplo, suponha que um aplicativo associe três parâmetros e execute a seguinte instrução SQL:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Se o aplicativo executar imediatamente a instrução SQL  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 no mesmo identificador de instrução, as associações de parâmetro para a instrução **Insert** são usadas porque essas são as associações armazenadas na estrutura da instrução. Na maioria dos casos, essa é uma prática de programação ruim e deve ser evitada. Em vez disso, o aplicativo deve chamar **SQLFreeStmt** com a opção SQL_RESET_PARAMS para desassociar todos os parâmetros antigos e, em seguida, associar novos.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Marcadores de parâmetro de associação](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Parâmetros de associação por nome (parâmetros nomeados)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Deslocamentos de associação de parâmetro](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descrever parâmetros](../../../odbc/reference/develop-app/describing-parameters.md)
