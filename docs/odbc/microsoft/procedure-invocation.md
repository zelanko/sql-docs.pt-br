---
title: "Invocação de procedimento | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd42836285c29e36e6bb64ebe594df570876ff6e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="procedure-invocation"></a>Invocação de procedimento
Quando o driver do Microsoft Access for usado, os procedimentos podem ser chamados do driver usando o **SQLExecDirect** ou **SQLPrepare** função com a seguinte sintaxe: {CALL *nome do procedimento * [(*parâmetro*[,*parâmetro*]...)]}. Observe que as expressões não têm suporte como parâmetros para um procedimento chamado.  
  
 Se um nome de procedimento inclui um traço, o nome deve ser delimitado por aspas back (').  
  
 Uma consulta parametrizada pode ser chamada usando a instrução anterior.

