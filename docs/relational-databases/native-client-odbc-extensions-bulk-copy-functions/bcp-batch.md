---
title: bcp_batch | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_batch
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6d43e8ca308d09e10a2f41728650a2cc0a4991d7
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009122"
---
# <a name="bcp_batch"></a>bcp_batch
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Confirma todas as linhas copiadas em massa anteriormente de variáveis de programa e enviadas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DBINT bcp_batch (HDBC  
        hdbc);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
## <a name="returns"></a>Retornos  
 O número de linhas salvas depois da última chamada para **bcp_batch**, ou -1 em caso de erro.  
  
## <a name="remarks"></a>Comentários  
 Lotes de cópias em massa definem transações. Quando um aplicativo usar [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) e **bcp_sendrow** para copiar linhas em massa de variáveis de programa para tabelas do SQL Server, as linhas serão confirmadas apenas quando o programa chamar **bcp_batch** ou [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md).  
  
 Você poderá chamar **bcp_batch** uma vez a cada *n* linhas ou quando houver uma pausa nos dados de entrada (como em um aplicativo de telemetria). Se um aplicativo não chamar **bcp_batch** , as linhas copiadas em massa serão confirmadas apenas quando **bcp_done** for chamado.  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
