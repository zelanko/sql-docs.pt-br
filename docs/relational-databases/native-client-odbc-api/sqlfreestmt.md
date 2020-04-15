---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3eb86f9b7b1076fa3a01135b5780637ee9857f90
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298442"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Geralmente   
      **SQLFreeStmt** não é recomendado no ODBC 3.0 e posterior. No entanto, se o aplicativo precisar reutilizar a declaração, você ainda deve usar **o SQLFreeStmt** com as opções **SQL_RESET_PARAMS** e **SQL_UNBIND).** Você também pode usar [SQLCloseCursor,](../../relational-databases/native-client-odbc-api/sqlclosecursor.md) [SQLBindParameter,](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) [SQLBindCol,](../../relational-databases/native-client-odbc-api/sqlbindcol.md) [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)e [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para substituir ou duplicar a função do **SQLFreeStmt** e usá-los em seu lugar.  
  
 Em geral, é mais eficiente reutilizar declarações do que solhá-las e alocar novas. No entanto, em algumas situações, como a reutilização de declarações, sqlFreestmt ainda deve ser usado.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLFreeStmt](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
