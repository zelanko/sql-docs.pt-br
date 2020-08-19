---
description: Revogar e conceder direitos ao usar procedimentos armazenados
title: Revogando e concedendo direitos ao usar procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad59f18f040dd1fefec606c99e3cce5f1002c22a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449268"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revogar e conceder direitos ao usar procedimentos armazenados
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Microsoft ODBC driver for Oracle retorna a seguinte mensagem de erro quando os direitos de usuário são concedidos e, em seguida, revogados em uma tabela acessada por um procedimento armazenado:  
  
 SQL_ERROR =-1  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] número incorreto de parâmetros"  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] erro de sintaxe ou violação de acesso"  
  
 A chamada para a função Oracle OCI Odessp () falha nesse cenário, mas é necessária para implementar os parâmetros padrão. Depois que as permissões da tabela subjacente forem modificadas, o procedimento armazenado deverá ser recompilado antes de ser executado novamente.
