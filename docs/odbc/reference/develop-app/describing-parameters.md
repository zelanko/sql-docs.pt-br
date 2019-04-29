---
title: Descrevendo parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bc752afc0cb5214e629a343c35464e612b57c36
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049836"
---
# <a name="describing-parameters"></a>Descrever parâmetros
**SQLBindParameter** tem argumentos que descrevem o parâmetro: o tipo SQL, precisão e escala. O driver usa essas informações, ou *metadados,* para converter o valor do parâmetro para o tipo necessário pela fonte de dados. À primeira vista, pode parecer que o driver está em uma posição melhor para conhecer os metadados de parâmetro que o aplicativo; Afinal de contas, o driver pode facilmente descobrir os metadados para um resultado de coluna do conjunto. Na verdade, isso não for o caso. Em primeiro lugar, a maioria das fontes de dados não fornecem uma maneira para o driver descobrir os metadados de parâmetro. Segundo, a maioria dos aplicativos já conhece os metadados.  
  
 Se uma instrução SQL é embutido no código do aplicativo, o gravador de aplicativos já conhece o tipo de cada parâmetro. Se uma instrução SQL é criada pelo aplicativo em tempo de execução, o aplicativo pode determinar os metadados ao criar a instrução. Por exemplo, quando o aplicativo constrói a cláusula  
  
```  
WHERE OrderID = ?  
```  
  
 ele pode chamar **SQLColumns** para a coluna OrderID.  
  
 A única situação em que o aplicativo não é possível determinar facilmente os metadados de parâmetro é quando o usuário insere uma instrução parametrizada. Nesse caso, o aplicativo chama **SQLPrepare** para preparar a instrução **SQLNumParams** para determinar o número de parâmetros, e **SQLDescribeParam** para descrever cada parâmetro. No entanto, conforme observado anteriormente, a maioria das fontes de dados não fornecem uma maneira para descobrir os metadados de parâmetro, portanto, o driver **SQLDescribeParam** não tem amplo suporte.
