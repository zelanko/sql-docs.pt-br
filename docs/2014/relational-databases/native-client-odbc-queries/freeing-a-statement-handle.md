---
title: Liberando um identificador de instrução | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b1a155f7d2ee6cc5f92d46c2bb744168dc5ebc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200050"
---
# <a name="freeing-a-statement-handle"></a>Liberando um identificador de instrução
  É mais eficiente reutilizar identificadores de instrução do que eliminá-los e alocar novos. Antes de executar uma nova instrução SQL em um identificador de instrução, os aplicativos deverão verificar se as configurações de instrução atuais são apropriadas. Essas configurações incluem atributos de instrução, associações de parâmetro e associações de conjunto de resultados. Geralmente, parâmetros e conjuntos de resultados para a instrução SQL antiga deve ser desassociada chamando [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) com o SQL_RESET_PARAMS e SQL_UNBIND opções e, em seguida, novamente associado para a nova instrução SQL.  
  
 Quando o aplicativo tiver terminado de usar a instrução, ele chama [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) para liberar a instrução. Observe que **SQLDisconnect** libera automaticamente todas as instruções em uma conexão.  
  
## <a name="see-also"></a>Consulte também  
 [Executando consultas &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
