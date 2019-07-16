---
title: Função do Driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7c344c1d8b3a4702728807af9dae7ed9ca7c5cd0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020386"
---
# <a name="role-of-the-driver"></a>Função do driver
O driver verifica todos os erros e avisos não verificados pelo Gerenciador de Driver e ordena os registros de status que ele gera. (Um ODBC 2. *x* driver não ordena os registros de status.) Isso inclui erros e avisos em truncamento de dados, a conversão de dados, a sintaxe e alguns transições de estado. O driver também pode verificar erros e avisos parcialmente verificados pelo Gerenciador de Driver. Por exemplo, embora o Gerenciador de Driver verifica se o valor de *operação* na **SQLSetPos** é legal, o driver deve verificar se ele é compatível.  
  
 O driver também mapeia *erros nativos* - ou seja, os erros retornados pela fonte de dados - para SQLSTATEs. Por exemplo, o driver pode mapear um número de erros nativos diferentes de SQL sintaxe inválida para o SQLSTATE 42000 (sintaxe ou violação de acesso). O driver retorna o número de erro nativo no campo SQL_DIAG_NATIVE do registro de status. Documentação do driver deve mostrar como erros e avisos são mapeados da fonte de dados para argumentos **SQLGetDiagRec** e **SQLGetDiagField**.
