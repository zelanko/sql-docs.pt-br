---
title: SQLExecDirect | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLExecDirect function
ms.assetid: e7c2a5b5-83f4-4c72-9aca-7b9fb4748b11
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e339bbb2b261301f72ce8e79034547b9430dae98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014498"
---
# <a name="sqlexecdirect"></a>SQLExecDirect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Se o atributo de instrução SQL_SOPT_SS_PARAM_FOCUS não 0, SQLExecDirect retornará SQL_ERROR e gerar um registro de diagnóstico com SQLSTATE = HY024 e a mensagem "valor de atributo inválido, SQL_SOPT_SS_PARAM_FOCUS (deve ser zero em tempo de execução)". Para obter mais informações sobre SQL_SPOT_SS_PARAM_FOCUS, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=80709)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
