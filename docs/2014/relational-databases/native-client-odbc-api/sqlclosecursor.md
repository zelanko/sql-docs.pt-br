---
title: SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da7d6541f7bf31920519cc7462bdfd24a5f6dc0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067682"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor** substitui [SQLFreeStmt](sqlfreestmt.md) com um *opção* valor SQL_CLOSE. Após a recepção de **SQLCloseCursor**, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client descarta linhas de conjunto de resultados pendentes. Observe que as associações de parâmetro e coluna da instrução (se houver) são mantidas inalteradas por **SQLCloseCursor**.  
  
## <a name="see-also"></a>Consulte também  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
