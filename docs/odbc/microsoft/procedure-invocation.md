---
title: Invocação de procedimento | Microsoft Docs
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
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97e86097ecb5e9a58e5a37a0ec02646e9dcf855a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="procedure-invocation"></a>Invocação de procedimento
Quando o driver do Microsoft Access for usado, os procedimentos podem ser chamados do driver usando o **SQLExecDirect** ou **SQLPrepare** função com a seguinte sintaxe: {CALL *nome do procedimento*  [(*parâmetro*[,*parâmetro*]...)]}. Observe que as expressões não têm suporte como parâmetros para um procedimento chamado.  
  
 Se um nome de procedimento inclui um traço, o nome deve ser delimitado por aspas back (').  
  
 Uma consulta parametrizada pode ser chamada usando a instrução anterior.
