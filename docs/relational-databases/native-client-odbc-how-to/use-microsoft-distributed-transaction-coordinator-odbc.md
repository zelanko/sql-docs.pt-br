---
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 603b9a84f49048b1e1867b56ecd8642704cdd052
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75244683"
---
# <a name="use-microsoft-distributed-transaction-coordinator-odbc"></a>Usar o Coordenador de Transações Distribuídas da Microsoft (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-update-two-or-more-sql-servers-by-using-ms-dtc"></a>Para atualizar dois ou mais SQL Servers usando MS DTC  
  
1.  Conecte-se a MS DTC usando a função DtcGetTransactionManager MS DTC OLE. Para obter informações sobre o MS DTC, consulte Coordenador de transações distribuídas da Microsoft.  
  
2.  Chame o SQL DriverConnect uma vez para cada conexão de SQL Server que você deseja estabelecer.  
  
3.  Chame a função ITransactionDispenser::BeginTransaction MS DTC OLE para começar uma transação MS DTC e obter um objeto de transação que a represente.  
  
4.  Chame [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) uma ou mais vezes para cada conexão ODBC que você deseja listar na transação MS DTC. O [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) segundo parâmetro deve ser SQL_ATTR_ENLIST_IN_DTC e o terceiro parâmetro deve ser o objeto Transaction (obtido na etapa 3).  
  
5.  Chame [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) uma vez para cada SQL Server que você deseja atualizar.  
  
6.  Chame a função ITransaction::Commit MS DTC OLE para confirmar a transação MS DTC. O objeto de transação não é mais válido.  

 Para executar uma série de MS DTC transações, repita as etapas de 3 a 6.  
  
 Para liberar a referência para o objeto de transação, chame a função ITransaction::Return MS DTC OLE.  
  
 Para usar uma conexão ODBC com uma transação MS DTC e usar a mesma conexão com uma transação do SQL Server local, chame [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) com SQL_DTC_DONE.  
  
> [!NOTE]  
>  Você também pode chamar [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) para cada SQL Server, em vez de chamá-lo conforme sugerido nas etapas 4 e 5.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando transações &#40;&#41;ODBC](https://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
