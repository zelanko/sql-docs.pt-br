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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3e076c7e81a1ccf61813bf5dc629fb3ce59f5070
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706354"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor** substitui [SQLFreeStmt](sqlfreestmt.md) por um valor de *opção* de SQL_CLOSE. Após a recepção de **SQLCloseCursor**, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client descarta linhas de conjunto de resultados pendentes. Observe que as associações de parâmetro e coluna da instrução (se houver) são mantidas inalteradas por **SQLCloseCursor**.  
  
## <a name="see-also"></a>Consulte Também  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
