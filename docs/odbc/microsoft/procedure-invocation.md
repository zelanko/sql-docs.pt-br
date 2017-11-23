---
title: "Invocação de procedimento | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 793209ab716d720266e834fcbbb846dea56950ed
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="procedure-invocation"></a>Invocação de procedimento
Quando o driver do Microsoft Access for usado, os procedimentos podem ser chamados do driver usando o **SQLExecDirect** ou **SQLPrepare** função com a seguinte sintaxe: {CALL *nome do procedimento*  [(*parâmetro*[,*parâmetro*]...)]}. Observe que as expressões não têm suporte como parâmetros para um procedimento chamado.  
  
 Se um nome de procedimento inclui um traço, o nome deve ser delimitado por aspas back (').  
  
 Uma consulta parametrizada pode ser chamada usando a instrução anterior.
