---
title: SQLExecute | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQLExecute function
ms.assetid: 4d7db8b6-611f-4fe4-be85-2a407059de45
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6f63bb60af1be4e81cfb17bf14344872a3a75932
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sqlexecute"></a>SQLExecute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Se o atributo de instrução que sql_sopt_ss_param_focus não for definido como 0, SQLExecute retornará SQL_ERROR e gerar um registro de diagnóstico com SQLSTATE = HY024 e a mensagem "valor de atributo inválido, SQL_SOPT_SS_PARAM_FOCUS (deve ser zero em tempo de execução)". Para obter mais informações sobre SQL_SOPT_SS_PARAM_FOCUS, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=80708)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
