---
title: SQLGetStmtOption (Driver Visual FoxPro ODBC) | Microsoft Docs
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
ms.openlocfilehash: 2624783f7bd55903f5741c62190626e455a9096d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295136"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível Um  
  
 Retorna a configuração atual de uma opção de declaração.  
  
|*FOption*|Retornos|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|Valor inteiro de 32 bits que é o marcador para o número de registro atual|  
|SQL_ROW_NUMBER|Inteiro de 32 bits especificando a posição da linha atual dentro do conjunto de resultados|  
|SQL_TRANSLATE_DLL|Erro: "Driver não é capaz"|  
  
 O Visual FoxPro ODBC Driver não tem DLLs de tradução.  
  
 Para obter mais informações, consulte [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) na *referência do programador ODBC*.
