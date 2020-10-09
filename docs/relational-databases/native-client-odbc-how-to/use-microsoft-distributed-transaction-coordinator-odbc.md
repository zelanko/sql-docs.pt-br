---
description: Usar o Coordenador de Transações Distribuídas da Microsoft (ODBC)
title: Coordenador de Transações Distribuídas (ODBC)
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, using
ms.assetid: 12a275e1-8c7e-436d-8a4e-b7bee853b35c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d8be0e1e3ffc0692eae8b2d1dfa6464ad2e7edae
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868829"
---
# <a name="use-microsoft-distributed-transaction-coordinator-odbc"></a>Usar o Coordenador de Transações Distribuídas da Microsoft (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-update-two-or-more-sql-servers-by-using-ms-dtc"></a>Para atualizar dois ou mais SQL Servers usando MS DTC  
  
1.  Conecte-se a MS DTC usando a função DtcGetTransactionManager MS DTC OLE. Para obter informações sobre o MS DTC, consulte Coordenador de transações distribuídas da Microsoft.  
  
2.  Chame o SQL DriverConnect uma vez para cada conexão de SQL Server que você deseja estabelecer.  
  
3.  Chame a função ITransactionDispenser::BeginTransaction MS DTC OLE para começar uma transação MS DTC e obter um objeto de transação que a represente.  
  
4.  Chame [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) uma ou mais vezes para cada conexão ODBC que você deseja listar na transação MS DTC. O segundo parâmetro [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) deve ser SQL_ATTR_ENLIST_IN_DTC e o terceiro, o objeto de transação (obtido na Etapa 3).  
  
5.  Chame [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) uma vez para cada SQL Server que você deseja atualizar.  
  
6.  Chame a função ITransaction::Commit MS DTC OLE para confirmar a transação MS DTC. O objeto de transação não é mais válido.  

 Para executar uma série de MS DTC transações, repita as etapas de 3 a 6.  
  
 Para liberar a referência para o objeto de transação, chame a função ITransaction::Return MS DTC OLE.  
  
 Para usar uma conexão ODBC com uma transação MS DTC e usar a mesma conexão com uma transação do SQL Server local, chame [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) com SQL_DTC_DONE.  
  
> [!NOTE]  
>  Você também pode chamar [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) para cada SQL Server, em vez de chamá-lo conforme sugerido nas etapas 4 e 5.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando transações &#40;&#41;ODBC ](../native-client/odbc/performing-transactions-in-odbc.md)  
  
