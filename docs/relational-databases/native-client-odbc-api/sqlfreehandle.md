---
description: SQLFreeHandle
title: SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ee9fa4d5dabc24bfe761de638c3b5626c89fd6d3
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809772"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  No modo de confirmação manual, chamar **SQLFreeHandle** em um identificador de instrução com uma transação aberta causará uma reversão das alterações pendentes do banco de dados. Chamar **SQLFreeHandle** em um identificador de instrução sempre fechará quaisquer cursores abertos e descartará resultados pendentes, liberando todos os recursos associados ao identificador de instrução.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLFreeHandle](../../odbc/reference/syntax/sqlfreehandle-function.md)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
