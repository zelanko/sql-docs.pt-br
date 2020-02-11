---
title: Invocação de procedimento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc37ef6d268dba71f8270909ea9c5b938ef3ee75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070489"
---
# <a name="procedure-invocation"></a>Invocação de procedimento
Quando o driver do Microsoft Access é usado, os procedimentos podem ser invocados por meio do driver usando a função **SQLExecDirect** ou **SQLPrepare** com a seguinte sintaxe: {chamar *procedure-name* [(*parâmetro*[,*Parameter*]...)]}. Observe que não há suporte para expressões como parâmetros para um procedimento chamado.  
  
 Se um nome de procedimento incluir um traço, o nome deverá ser delimitado com aspas de retorno (').  
  
 Uma consulta parametrizada pode ser chamada usando a instrução anterior.
