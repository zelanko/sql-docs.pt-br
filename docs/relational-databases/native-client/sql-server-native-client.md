---
title: SQL Server Native Client | Microsoft Docs
ms.date: 04/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0d4694e013ce65fb1fb3c66b352b8e583a608899
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32952771"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

SNAC ou SQL Server Native Client, é um termo que tenha sido usado alternadamente para se referir a drivers ODBC e OLE DB para SQL Server.

**Observação:** não é recomendável usar esse driver para novo desenvolvimento. O novo provedor de OLE DB é chamado de [Microsoft OLE DB Driver para SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) que será atualizado com os recursos de servidor mais recentes no futuro.


**Para obter mais informações e baixar os Drivers de ODBC ou SNAC, visite [SNAC de ciclo de vida explicado](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).**

Para obter mais informações sobre o Driver ODBC para SQL Server, consulte [Microsoft ODBC Driver for SQL Server no Windows](https://msdn.microsoft.com/library/jj730314(v=sql.110).aspx).  Consulte também, [apresentando os novos Drivers de ODBC da Microsoft para SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/), e [ODBC Driver 13.1 para SQL Server lançadas](https://blogs.technet.microsoft.com/dataplatforminsider/2016/08/03/odbc-driver-13-1-for-sql-server-released/).  

 Obter informações sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recursos Native Client lançados com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], a última versão disponível do SQL Server native Client:

-   [Suporte do SQL Server Native Client para LocalDB](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [Descoberta de metadados](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [Suporte a UTF-16 no SQL Server Native Client 11.0](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [Suporte para alta disponibilidade, recuperação de desastres do SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [Acessar informações de diagnóstico nos logs de eventos estendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

ODBC em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte a três recursos que foram adicionados ao ODBC padrão no SDK do Windows 7:  

-   Execução assíncrona em operações relacionadas à conexão. Para obter mais informações, consulte [Execução assíncrona](http://go.microsoft.com/fwlink/?LinkID=191493).  

-   Extensibilidade do tipo de dados C. Para obter mais informações, consulte [Tipos de dados C em ODBC](http://go.microsoft.com/fwlink/?LinkID=191495).  

     Para dar suporte a esse recurso no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, SQLGetDescField pode retornar **SQL_C_SS_TIME2** (para **tempo** tipos) ou **SQL_C_SS_TIMESTAMPOFFSET** (para **datetimeoffset**) em vez de **SQL_C_BINARY**, se seu aplicativo usar o ODBC 3.8. Para obter mais informações, consulte [suporte de tipo de dados para aprimoramentos de hora e data de ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  

-   Chamando **SQLGetData** várias vezes com um buffer pequeno para recuperar um valor de parâmetro grande. Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](http://go.microsoft.com/fwlink/?LinkID=191494).  

 Os tópicos a seguir descrevem as alterações de comportamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  

-   Ao chamar **ICommandWithParameters::SetParameterInfo**, o valor transmitido ao parâmetro *pwszName* deve ser um identificador válido. Para obter mais informações, consulte [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md).  

-   **SQLDescribeParam** consistentemente retornará um valor de conformidade de especificação do ODBC. Para obter mais informações, consulte [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md).  

-   [Alteração de comportamento do driver ODBC ao lidar com conversões de caracteres](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>Consulte também  
[Instale o SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [Recursos do SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
