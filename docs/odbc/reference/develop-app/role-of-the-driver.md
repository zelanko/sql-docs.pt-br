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
manager: craigg
ms.openlocfilehash: b940eac1548582285e7d41e0014cfe911dfb1137
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254187"
---
# <a name="role-of-the-driver"></a>Função do driver
O driver verifica todos os erros e avisos não verificados pelo Gerenciador de Driver e ordena os registros de status que ele gera. (Um ODBC 2. *x* driver não ordena os registros de status.) Isso inclui erros e avisos em truncamento de dados, a conversão de dados, a sintaxe e alguns transições de estado. O driver também pode verificar erros e avisos parcialmente verificados pelo Gerenciador de Driver. Por exemplo, embora o Gerenciador de Driver verifica se o valor de *operação* na **SQLSetPos** é legal, o driver deve verificar se ele é compatível.  
  
 O driver também mapeia *erros nativos* - ou seja, os erros retornados pela fonte de dados - para SQLSTATEs. Por exemplo, o driver pode mapear um número de erros nativos diferentes de SQL sintaxe inválida para o SQLSTATE 42000 (sintaxe ou violação de acesso). O driver retorna o número de erro nativo no campo SQL_DIAG_NATIVE do registro de status. Documentação do driver deve mostrar como erros e avisos são mapeados da fonte de dados para argumentos **SQLGetDiagRec** e **SQLGetDiagField**.
