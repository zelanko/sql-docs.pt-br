---
title: Liberando um identificador de instrução | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7da2fec15303e9c2d50fb7aa2e6dc40266a380d9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116358"
---
# <a name="freeing-a-statement-handle"></a>Liberando um identificador de instrução
  É mais eficiente reutilizar identificadores de instrução do que eliminá-los e alocar novos. Antes de executar uma nova instrução SQL em um identificador de instrução, os aplicativos deverão verificar se as configurações de instrução atuais são apropriadas. Essas configurações incluem atributos de instrução, associações de parâmetro e associações de conjunto de resultados. Geralmente, parâmetros e conjuntos de resultados para a instrução SQL antiga deve ser desassociada chamando [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) com o SQL_RESET_PARAMS e SQL_UNBIND opções e associado novamente para a nova instrução SQL.  
  
 Quando o aplicativo terminar de usar a instrução, ele chama [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) para liberar a instrução. Observe que **SQLDisconnect** libera automaticamente todas as instruções em uma conexão.  
  
## <a name="see-also"></a>Consulte também  
 [Executando consultas &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  