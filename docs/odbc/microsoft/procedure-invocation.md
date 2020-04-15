---
title: Invocação de Procedimento | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32617cdb753f5fc1b9c52520cb609d2902137b54
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290767"
---
# <a name="procedure-invocation"></a>Invocação de procedimento
Quando o driver Microsoft Access é usado, os procedimentos podem ser invocados do driver usando a função **SQLExecDirect** ou **SQLPrepare** com a seguinte sintaxe: *{CALL procedure-name* [(parâmetro [,*parâmetro*]...)}.*parameter* Observe que as expressões não são suportadas como parâmetros para um procedimento chamado.  
  
 Se um nome de procedimento incluir um traço, o nome deve ser delimitado com aspas traseiras (').  
  
 Uma consulta parametrizada pode ser chamada usando a declaração anterior.
