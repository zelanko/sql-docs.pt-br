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
manager: craigg
ms.openlocfilehash: 7b33bc399646a6d274c875abd36d53219a2814e1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833774"
---
# <a name="procedure-invocation"></a>Invocação de procedimento
Quando o driver do Microsoft Access for usado, os procedimentos podem ser chamados do driver usando o **SQLExecDirect** ou **SQLPrepare** função com a seguinte sintaxe: {chamar *nome do procedimento*  [(*parâmetro*[,*parâmetro*]...)]}. Observe que não há suporte para expressões como parâmetros para um procedimento chamado.  
  
 Se um nome de procedimento inclui um traço, o nome deve ser delimitado com o back-aspas (').  
  
 Uma consulta parametrizada pode ser chamada usando a instrução anterior.
