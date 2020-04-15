---
title: Papel do Motorista | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c683d990aaa3fd6892369e734c06fd1c356bd0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304277"
---
# <a name="role-of-the-driver"></a>Função do driver
O motorista verifica todos os erros e avisos não verificados pelo Driver Manager e encomenda registros de status que ele gera. (Um ODBC 2. *x* driver não encomenda registros de status.) Isso inclui erros e avisos em truncamento de dados, conversão de dados, sintaxe e algumas transições de estado. O motorista também pode verificar erros e avisos parcialmente verificados pelo Driver Manager. Por exemplo, embora o Driver Manager verifique se o valor da *operação* em **SQLSetPos** é legal, o motorista deve verificar se ele é suportado.  
  
 O driver também mapeia *erros nativos* - ou seja, erros retornados pela fonte de dados - para SQLSTATEs. Por exemplo, o driver pode mapear uma série de erros nativos diferentes para sintaxe SQL ilegal para SQLSTATE 42000 (erro de sintaxe ou violação de acesso). O driver retorna o número de erro nativo no campo SQL_DIAG_NATIVE do registro de status. A documentação do driver deve mostrar como erros e avisos são mapeados da fonte de dados para argumentos no **SQLGetDiagRec** e **no SQLGetDiagField**.
