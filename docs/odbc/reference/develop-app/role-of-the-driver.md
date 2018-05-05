---
title: Função do Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e0ef812cb4c397beeb5778c4e4764b7e79f5d0a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="role-of-the-driver"></a>Função do Driver
O driver verifica todos os erros e avisos não verificados pelo Gerenciador de Driver e ordena os registros de status que ele gera. (Um ODBC 2. *x* driver não ordena os registros de status.) Isso inclui erros e avisos em truncamento de dados, a conversão de dados, a sintaxe e algumas transições de estado. O driver também pode verificar erros e avisos parcialmente verificados pelo Gerenciador de Driver. Por exemplo, embora o Gerenciador de Driver verifica se o valor de *operação* na **SQLSetPos** for válido, o driver deve verificar se há suporte.  
  
 O driver também mapeia *erros nativos* — ou seja, os erros retornados pela fonte de dados — para SQLSTATEs. Por exemplo, o driver pode mapear um número de diferentes erros nativos para SQL sintaxe inválida para SQLSTATE 42000 (sintaxe ou violação de acesso). O driver retorna o número de erro nativo no campo SQL_DIAG_NATIVE do registro de status. Documentação do driver deve mostrar como erros e avisos são mapeados da fonte de dados para argumentos em **SQLGetDiagRec** e **SQLGetDiagField**.
