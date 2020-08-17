---
description: SQLGetStmtOption (Driver ODBC do Visual FoxPro)
title: SQLGetStmtOption (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e57456ca05e39c12b83da80cd19c34f482c3d8df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340082"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível um  
  
 Retorna a configuração atual de uma opção de instrução.  
  
|*FOption*|Retornos|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|valor inteiro de 32 bits que é o indicador para o número do registro atual|  
|SQL_ROW_NUMBER|inteiro de 32 bits especificando a posição da linha atual no conjunto de resultados|  
|SQL_TRANSLATE_DLL|Erro: "driver não compatível"|  
  
 O driver ODBC do Visual FoxPro não tem DLLs de tradução.  
  
 Para obter mais informações, consulte [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) na *referência do programador de ODBC*.
