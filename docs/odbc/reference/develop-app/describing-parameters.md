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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305937"
---
# <a name="describing-parameters"></a>Descrever parâmetros
**SQLBindParameter** tem argumentos que descrevem o parâmetro: seu tipo, precisão e escala SQL. O driver usa essas informações, ou *metadados,* para converter o valor do parâmetro para o tipo necessário para a fonte de dados. À primeira vista, pode parecer que o driver está em uma posição melhor para saber os metadados do parâmetro do que o aplicativo; Afinal, o driver pode facilmente descobrir os metadados de uma coluna de conjunto de resultados. Acontece que esse não é o caso. Primeiro, a maioria das fontes de dados não fornece uma maneira para o driver descobrir os metadados do parâmetro. Segundo, a maioria dos aplicativos já conhecem os metadados.  
  
 Se uma instrução SQL for embutida em código no aplicativo, o gravador de aplicativos já saberá o tipo de cada parâmetro. Se uma instrução SQL for construída pelo aplicativo em tempo de execução, o aplicativo poderá determinar os metadados à medida que criar a instrução. Por exemplo, quando o aplicativo constrói a cláusula  
  
```  
WHERE OrderID = ?  
```  
  
 Ele pode chamar **SQLColumns** para a coluna OrderID.  
  
 A única situação na qual o aplicativo não pode determinar facilmente os metadados do parâmetro é quando o usuário insere uma instrução parametrizada. Nesse caso, o aplicativo chama **SQLPrepare** para preparar a instrução, **SQLNumParams** para determinar o número de parâmetros e **SQLDescribeParam** para descrever cada parâmetro. No entanto, como foi observado anteriormente, a maioria das fontes de dados não fornece uma maneira para o driver descobrir os metadados do parâmetro; portanto, não há suporte amplo para **SQLDescribeParam** .
