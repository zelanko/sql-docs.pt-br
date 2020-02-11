---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5521fb11cad064cf487d38562f4146fd32587993
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898792"
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
