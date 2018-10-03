---
title: Alocando um identificador de ambiente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66afa14ccb1953265f526f8c8861237638f569fd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151266"
---
# <a name="allocating-an-environment-handle"></a>Alocando um identificador de ambiente
  Antes que um aplicativo possa chamar qualquer função ODBC, ele deve inicializar o ambiente de ODBC e alocar um identificador de ambiente. Trata-se do identificador de contexto global e do espaço reservado para os demais identificadores no ODBC. Você pode fazer isso chamando **SQLAllocHandle** com o *HandleType* parâmetro definido como SQL_HANDLE_ENV e *InputHandle* definido como SQL_NULL_HANDLE.  
  
 Depois de alocar o identificador de ambiente, o aplicativo deve definir atributos de ambiente para indicar qual versão das chamadas de função ODBC será usada. Para usar o ODBC 3. *x* funções, chame [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) com o *atributo* parâmetro definido como SQL_ATTR_ODBC_VERSION e *ValuePtr* definido como SQL_OV_ ODBC3.  
  
## <a name="see-also"></a>Consulte também  
 [Comunicando-se com o SQL Server &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
