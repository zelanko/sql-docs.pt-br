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
ms.openlocfilehash: 2687e1a68789566fd7b660a8241d65ff4714a933
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633564"
---
# <a name="role-of-the-driver"></a>Função do driver
O driver verifica todos os erros e avisos não verificados pelo Gerenciador de Driver e ordena os registros de status que ele gera. (Um ODBC 2. *x* driver não ordena os registros de status.) Isso inclui erros e avisos em truncamento de dados, a conversão de dados, a sintaxe e alguns transições de estado. O driver também pode verificar erros e avisos parcialmente verificados pelo Gerenciador de Driver. Por exemplo, embora o Gerenciador de Driver verifica se o valor de *operação* na **SQLSetPos** é legal, o driver deve verificar se ele é compatível.  
  
 O driver também mapeia *erros nativos* — ou seja, os erros retornados pela fonte de dados — para SQLSTATEs. Por exemplo, o driver pode mapear um número de erros nativos diferentes de SQL sintaxe inválida para o SQLSTATE 42000 (sintaxe ou violação de acesso). O driver retorna o número de erro nativo no campo SQL_DIAG_NATIVE do registro de status. Documentação do driver deve mostrar como erros e avisos são mapeados da fonte de dados para argumentos **SQLGetDiagRec** e **SQLGetDiagField**.
