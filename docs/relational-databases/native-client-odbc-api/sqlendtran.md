---
title: SQLEndTran | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a7de8feba9c86292dc8149b6bfe9c8a14bc57911
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Por padrão, o driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client fecha o cursor associado de uma instrução quando **SQLEndTran** confirma ou reverte uma operação. Os cursores de servidor são fechados, a menos que eles sejam estáticos. Quando **SQLEndTran** confirma ou reverte uma operação, o comportamento do cursor associado da instrução é determinado pelo valor do atributo SQL_COPT_SS_PRESERVE_CURSORS da conexão ODBC específica do driver, definido por [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
## <a name="see-also"></a>Consulte também  
 [Detalhes de implementação de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [Função SQLEndTran](http://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
