---
description: Invocação de procedimento
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2643a36c834b577dfcecdcc81fd938a3a7d1018
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340442"
---
# <a name="procedure-invocation"></a>Invocação de procedimento
Quando o driver do Microsoft Access é usado, os procedimentos podem ser invocados por meio do driver usando a função **SQLExecDirect** ou **SQLPrepare** com a seguinte sintaxe: {chamar *procedure-name* [(*parâmetro*[,*Parameter*]...)]}. Observe que não há suporte para expressões como parâmetros para um procedimento chamado.  
  
 Se um nome de procedimento incluir um traço, o nome deverá ser delimitado com aspas de retorno (').  
  
 Uma consulta parametrizada pode ser chamada usando a instrução anterior.
