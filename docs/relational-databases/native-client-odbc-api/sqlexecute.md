---
title: SQLExecute | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLExecute function
ms.assetid: 4d7db8b6-611f-4fe4-be85-2a407059de45
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 44987b3f6e2ceb1406101c88b8a962282468d7ed
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786934"
---
# <a name="sqlexecute"></a>SQLExecute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Se o atributo de instrução SQL_SOPT_SS_PARAM_FOCUS não estiver definido como 0, SQLExecute retornará SQL_ERROR e gerará um registro de diagnóstico com SQLSTATE = HY024 e a mensagem "valor de atributo inválido SQL_SOPT_SS_PARAM_FOCUS (deve ser zero em tempo de execução)". Para obter mais informações sobre SQL_SPOT_SS_PARAM_FOCUS, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros &#40;com valor&#41;de tabela ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
   [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=80708)  
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
