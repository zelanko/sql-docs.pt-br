---
title: Revogando e conceder direitos ao usar procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f0572991348ba73f5c5775873d9fec8c16705484
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revogação e conceder direitos ao usar procedimentos armazenados
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Microsoft ODBC Driver for Oracle retorna a seguinte mensagem de erro quando os direitos de usuário são concedidos e revogados, em seguida, em uma tabela acessada por um procedimento armazenado:  
  
 1 = SQL_ERROR  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] número incorreto de parâmetros"  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] sintaxe ou violação de acesso"  
  
 A chamada para a função Oracle OCI Odessp() falha nesse cenário, mas é necessária para implementar os parâmetros padrão. Depois que as permissões de tabela subjacente são modificadas, o procedimento armazenado deve ser recompilado antes de executá-lo novamente.
