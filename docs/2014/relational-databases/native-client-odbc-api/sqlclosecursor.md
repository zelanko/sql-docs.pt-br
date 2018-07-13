---
title: SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ec1f623d2a770664897fce1247af1c94f506b04
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425295"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor** substitui [SQLFreeStmt](sqlfreestmt.md) com um *opção* valor SQL_CLOSE. Após o recebimento dos **SQLCloseCursor**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client descarta linhas de conjunto de resultados pendentes. Observe que as associações de parâmetro e coluna da instrução (se houver) são mantidas inalteradas por **SQLCloseCursor**.  
  
## <a name="see-also"></a>Consulte também  
 [SQLCloseCursor](http://go.microsoft.com/fwlink/?LinkId=59331)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
