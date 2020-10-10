---
title: Sobre o
description: Saiba mais sobre os recursos do SQL Server Native Client (SNAC). SQL Server Native Client refere-se aos drivers ODBC e OLE DB para SQL Server.
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f62b0fa0d27ed5db06f85b2c77e1ab381534d731
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891106"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SNAC, ou SQL Server Native Client, é um termo que foi usado de forma intercambiável para se referir aos drivers ODBC e OLE DB para SQL Server.

> [!IMPORTANT] 
> O SQL Server Native Client (SQLNCLI) permanece preterido e não é recomendável usá-lo para novos trabalhos de desenvolvimento. Em vez disso, use o novo [Driver do Microsoft OLE DB para SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL), que será atualizado com os recursos de servidor mais recentes.

> [!NOTE]
> Para obter mais informações e baixar os drivers SNAC ou ODBC, consulte a [postagem de blog do SNAC Lifecycle explicou](/archive/blogs/sqlreleaseservices/snac-lifecycle-explained).
> Para obter mais informações sobre o driver ODBC para SQL Server, consulte [Microsoft ODBC driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).  

 Informações sobre os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recursos de cliente nativo lançados com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o, a última versão disponível do SQL Server Native Client:

-   [Suporte do SQL Server Native Client para LocalDB](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [Descoberta de metadados](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [Suporte a UTF-16 no SQL Server Native Client 11.0](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [Acessar informações de diagnóstico nos logs de eventos estendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

O ODBC no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte a três recursos que foram adicionados ao ODBC padrão no SDK do Windows 7:  

-   Execução assíncrona em operações relacionadas à conexão. Para obter mais informações, consulte [Execução assíncrona](../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).  

-   Extensibilidade do tipo de dados C. Para obter mais informações, consulte [Tipos de dados C em ODBC](../../odbc/reference/develop-app/c-data-types-in-odbc.md).  

     Para dar suporte a esse recurso no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o SQLGetDescField pode retornar **SQL_C_SS_TIME2** (para tipos de **tempo** ) ou **SQL_C_SS_TIMESTAMPOFFSET** (para **DateTimeOffset**) em vez de **SQL_C_BINARY**, se seu aplicativo usar o ODBC 3,8. Para obter mais informações, consulte [suporte de tipo de dados para aprimoramentos de data e hora ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  

-   Chamando **SQLGetData** várias vezes com um buffer pequeno para recuperar um valor de parâmetro grande. Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  

 Os tópicos a seguir descrevem as alterações de comportamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  

-   Ao chamar **ICommandWithParameters::SetParameterInfo**, o valor transmitido ao parâmetro *pwszName* deve ser um identificador válido. Para obter mais informações, consulte [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md).  

-   **SQLDescribeParam** retornará consistentemente um valor de conformidade de especificação ODBC. Para obter mais informações, consulte [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md).  

-   [Alteração de comportamento do driver ODBC ao lidar com conversões de caracteres](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>Veja também  
[Instalar SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [Recursos do SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)