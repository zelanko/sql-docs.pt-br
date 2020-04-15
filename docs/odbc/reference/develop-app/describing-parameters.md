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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f4d9284294707da0a469bf75ff9812ad5f7855bb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305937"
---
# <a name="describing-parameters"></a>Descrever parâmetros
**SQLBindParameter** tem argumentos que descrevem o parâmetro: seu tipo, precisão e escala SQL. O driver usa essas informações, ou *metadados,* para converter o valor do parâmetro para o tipo necessário pela fonte de dados. À primeira vista, pode parecer que o motorista está em melhor posição para conhecer os metadados do parâmetro do que o aplicativo; afinal, o driver pode facilmente descobrir os metadados para uma coluna de conjunto de resultados. Como se vê, este não é o caso. Primeiro, a maioria das fontes de dados não fornece uma maneira para o motorista descobrir metadados de parâmetros. Em segundo lugar, a maioria dos aplicativos já conhece os metadados.  
  
 Se uma declaração SQL for codificada no aplicativo, o autor do aplicativo já sabe o tipo de cada parâmetro. Se uma declaração SQL for construída pelo aplicativo em tempo de execução, o aplicativo poderá determinar os metadados à medida que ele constrói a declaração. Por exemplo, quando o aplicativo constrói a cláusula  
  
```  
WHERE OrderID = ?  
```  
  
 ele pode chamar **SQLColumns** para a coluna OrderID.  
  
 A única situação em que o aplicativo não pode determinar facilmente os metadados do parâmetro é quando o usuário entra em uma declaração parametrizada. Neste caso, o aplicativo chama **SQLPrepare** para preparar a declaração, **SQLNumParams** para determinar o número de parâmetros e **SQLDescribeParam** para descrever cada parâmetro. No entanto, como foi observado anteriormente, a maioria das fontes de dados não fornece uma maneira para o driver descobrir metadados de parâmetros, de modo que **o SQLDescribeParam** não é amplamente suportado.
