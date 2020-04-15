---
title: Revogação e concessão de direitos ao usar procedimentos armazenados | Microsoft Docs
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
ms.openlocfilehash: 469e6f0fdc6794e3bd163844e43821798aa4a617
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303982"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revogar e conceder direitos ao usar procedimentos armazenados
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Driver ODBC do Microsoft para Oracle retorna a seguinte mensagem de erro quando os direitos do usuário são concedidos e, em seguida, revogados em uma tabela acessada por um procedimento armazenado:  
  
 SQL_ERROR=-1  
  
 szErrorMsg="[Microsoft][Driver ODBC para Oracle]Número errado de parâmetros"  
  
 szErrorMsg="[Microsoft][Driver ODBC para Oracle]Erro de sintaxe ou violação de acesso"  
  
 A chamada para a função OCI Oracle Odessp() falha neste cenário, mas é necessária para implementar parâmetros padrão. Depois que as permissões da tabela subjacente forem modificadas, o procedimento armazenado deve ser recompilado antes de executá-lo novamente.
