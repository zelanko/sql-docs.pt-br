---
title: Descrever parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f746b7df2ac3ef4de73e54c6d78df02e0c64ec34
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="describing-parameters"></a>Descrever parâmetros
**SQLBindParameter** tem argumentos que descrevem o parâmetro: seu tipo SQL, precisão e escala. O driver usa essas informações, ou *metadados,* para converter o valor do parâmetro para o tipo necessário pela fonte de dados. À primeira vista, pode parecer que o driver está em uma posição melhor para conhecer os metadados de parâmetro que o aplicativo; Afinal, o driver pode facilmente descobrir os metadados para um conjunto de resultados coluna. Na verdade, isso não for o caso. Primeiro, a maioria das fontes de dados não fornecem uma maneira para que o driver descobrir os metadados de parâmetro. Segundo, a maioria dos aplicativos já souber os metadados.  
  
 Se uma instrução SQL é embutido no aplicativo, o gravador de aplicativos já conhece o tipo de cada parâmetro. Se uma instrução SQL é construída pelo aplicativo em tempo de execução, o aplicativo pode determinar os metadados ao criar a instrução. Por exemplo, quando o aplicativo constrói a cláusula  
  
```  
WHERE OrderID = ?  
```  
  
 ele pode chamar **SQLColumns** para a coluna OrderID.  
  
 A única situação em que o aplicativo não pode determinar facilmente os metadados de parâmetro é quando o usuário insere uma instrução parametrizada. Nesse caso, o aplicativo chama **SQLPrepare** para preparar a instrução **SQLNumParams** para determinar o número de parâmetros, e **SQLDescribeParam** para descrever cada parâmetro. No entanto, conforme observado anteriormente, a maioria das fontes de dados não fornecem uma maneira para que o driver descobrir os metadados de parâmetro, portanto **SQLDescribeParam** não tem muito suporte.
