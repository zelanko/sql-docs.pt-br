---
title: Matriz de suporte de recursos de driver
description: Saiba quais recursos populares têm suporte nos drivers para SQL Server e onde encontrar informações sobre eles.
ms.custom: ''
ms.date: 12/03/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-daenge
ms.openlocfilehash: 4fff9c04098bd0796f714d160864e4edb93613ac
ms.sourcegitcommit: 28fecbf61ae7b53405ca378e2f5f90badb1a296a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2020
ms.locfileid: "96595227"
---
# <a name="driver-feature-support-matrix-for-microsoft-sql-server"></a>Matriz de suporte de recursos de driver para Microsoft SQL Server

Se você estiver planejando usar um recurso no Microsoft SQL Server, ele talvez não esteja disponível em todos os drivers. Alguns motivos pelos quais um recurso pode não estar em um determinado driver incluem:

- O recurso não se aplica à tecnologia de driver.
- O recurso é novo e ainda não foi implementado em todos os drivers.
- O recurso não está sob demanda em um driver específico.
- Outros recursos estão sendo implementados primeiro.

Queremos que todos os drivers deem suporte a todos os recursos e façam esforços para garantir a paridade de recursos entre os drivers. No entanto, isso nem sempre é possível. Para ajudar você a escolher o driver apropriado para suas necessidades, aqui está uma lista de recursos populares e os drivers que os implementam.

- [.NET](#table1)
- [ODBC](#table2)
- [OLE DB](#table2)
- [JDBC](#table2)
- [PHP](#table3)
- [Node.js/JavaScript](#table3)
- [Python](#table3)

| <a id="table1"></a>Recurso | [Microsoft.<wbr>Data.<wbr>SqlClient (.NET Core)](ado-net/microsoft-ado-net-sql-server.md) | [Microsoft.<wbr>Data.<wbr>SqlClient (.NET Framework)](ado-net/microsoft-ado-net-sql-server.md) | System.<wbr>Data.<wbr>SqlClient (.NET Core) | [System.<wbr>Data.<wbr>SqlClient (.NET Framework)](/dotnet/framework/data/adonet/sql/) |
| :-- | :-- | :-- | :-- | :-- |
| [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [Sim](ado-net/sql/sqlclient-support-always-encrypted.md) | [Sim](ado-net/sql/sqlclient-support-always-encrypted.md) | | [Sim](ado-net/sql/sqlclient-support-always-encrypted.md) |
| [Always Encrypted com enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [Sim](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) | [Sim](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) | | [Sim](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) |
| [Autenticação do Token de Acesso do Azure Active Directory](/azure/active-directory/develop/access-tokens) | [Sim](/dotnet/api/system.data.sqlclient.sqlconnection.accesstoken) | [Sim](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) | [Sim](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) | [Sim](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) |
| [Autenticação de Senha do Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | [Sim](ado-net/sql/azure-active-directory-authentication.md) | [Sim](ado-net/sql/azure-active-directory-authentication.md) | | Sim |
| [Autenticação integrada do Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | [Sim](ado-net/sql/azure-active-directory-authentication.md) | [Sim](ado-net/sql/azure-active-directory-authentication.md) | | Sim |
| [Autenticação Interativa (MFA) do Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | [Sim](ado-net/sql/azure-active-directory-authentication.md) | [Sim](ado-net/sql/azure-active-directory-authentication.md) | | Sim |
| [Autenticação de Identidade Gerenciada do Azure Active Directory](/azure/active-directory/managed-identities-azure-resources/overview) | [Sim](ado-net/sql/azure-active-directory-authentication.md) | [Sim](ado-net/sql/azure-active-directory-authentication.md) | | |
| [Autenticação da Entidade de Serviço do Azure Active Directory](/azure/active-directory/develop/app-objects-and-service-principals) | [Sim](ado-net/sql/azure-active-directory-authentication.md) | [Sim](ado-net/sql/azure-active-directory-authentication.md) | | |
| [Autenticação Integrada do Windows](/windows-server/security/windows-authentication/windows-authentication-overview) | [Sim](ado-net/sql/authentication-sql-server.md) | [Sim](ado-net/sql/authentication-sql-server.md) | [Sim](/dotnet/framework/data/adonet/sql/authentication-in-sql-server) | [Sim](/dotnet/framework/data/adonet/sql/authentication-in-sql-server) |
| [Cópia em Massa](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | [Sim](ado-net/sql/bulk-copy-operations-sql-server.md) | [Sim](ado-net/sql/bulk-copy-operations-sql-server.md) | [Sim](/dotnet/framework/data/adonet/sql/bulk-copy-operations-in-sql-server) | [Sim](/dotnet/framework/data/adonet/sql/bulk-copy-operations-in-sql-server) |
| [Confidencialidade de dados e metadados de classificação](../relational-databases/security/sql-data-discovery-and-classification.md) | [Sim](ado-net/sql/data-classification.md) | [Sim](ado-net/sql/data-classification.md) | Sim | Sim |
| [MARS (conjunto de resultados ativos múltiplos)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [Sim](ado-net/sql/multiple-active-result-sets-mars.md) | [Sim](ado-net/sql/multiple-active-result-sets-mars.md) | [Sim](/dotnet/framework/data/adonet/sql/multiple-active-result-sets-mars) | [Sim](/dotnet/framework/data/adonet/sql/multiple-active-result-sets-mars) |
| [Tipos de dados espaciais](../relational-databases/spatial/spatial-data-sql-server.md) | | Sim | | Sim |
| [TVP (Parâmetros com Valor de Tabela)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | [Sim](ado-net/sql/table-valued-parameters.md) | [Sim](ado-net/sql/table-valued-parameters.md) | [Sim](/dotnet/framework/data/adonet/sql/table-valued-parameters) | [Sim](/dotnet/framework/data/adonet/sql/table-valued-parameters) |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sim](ado-net/sql/sqlclient-support-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sim](ado-net/sql/sqlclient-support-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sim](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.multisubnetfailover?view=netcore-1.0&preserve-view=true) | [Sim](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.multisubnetfailover?view=netframework-4.8&preserve-view=true) |
| [Resolução IP de Rede Transparente](odbc/using-transparent-network-ip-resolution.md) | | [Sim](/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-1.1&preserve-view=true) | | [Sim](/dotnet/api/system.data.sqlclient.sqlconnection.connectionstring?view=netframework-4.8&preserve-view=true) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

| <a id="table2"></a>Recurso | [ODBC Driver for SQL Server no Windows](odbc/microsoft-odbc-driver-for-sql-server.md) | [ODBC Driver for SQL Server em Linux e macOS](odbc/microsoft-odbc-driver-for-sql-server.md) | [JDBC Driver for SQL Server](jdbc/microsoft-jdbc-driver-for-sql-server.md) | [Driver do OLE DB para SQL Server](oledb/oledb-driver-for-sql-server.md) |
| :-- | :-- | :-- | :-- | :-- |
| [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [Sim](odbc/using-always-encrypted-with-the-odbc-driver.md) | [Sim](odbc/using-always-encrypted-with-the-odbc-driver.md) | [Sim](jdbc/using-always-encrypted-with-the-jdbc-driver.md) |
| [Always Encrypted com enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [Sim](odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) | [Sim](odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) | [Sim](jdbc/using-always-encrypted-with-the-jdbc-driver.md) | |
| [Autenticação do Token de Acesso do Azure Active Directory](/azure/active-directory/develop/access-tokens) | [Sim](odbc/using-azure-active-directory.md#authenticating-with-an-access-token) | [Sim](odbc/using-azure-active-directory.md#authenticating-with-an-access-token) | [Sim](jdbc/connecting-using-azure-active-directory-authentication.md#connecting-using-access-token) | [Sim](oledb/features/using-azure-active-directory.md) |
| [Autenticação de Senha do Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) |  [Sim](odbc/using-azure-active-directory.md) | [Sim](odbc/using-azure-active-directory.md) | [Sim](jdbc/connecting-using-azure-active-directory-authentication.md) | [Sim](oledb/features/using-azure-active-directory.md) |
| [Autenticação integrada do Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | [Sim](odbc/using-azure-active-directory.md) | [Sim](odbc/using-azure-active-directory.md) | [Sim](jdbc/connecting-using-azure-active-directory-authentication.md) | [Sim](oledb/features/using-azure-active-directory.md) |
| [Autenticação Interativa (MFA) do Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | [Sim](odbc/using-azure-active-directory.md) | | | [Sim](oledb/features/using-azure-active-directory.md) |
| [Autenticação de Identidade Gerenciada do Azure Active Directory](/azure/active-directory/managed-identities-azure-resources/overview) | [Sim](odbc/using-azure-active-directory.md) | [Sim](odbc/using-azure-active-directory.md) | [Sim](jdbc/connecting-using-azure-active-directory-authentication.md) | [Sim](oledb/features/using-azure-active-directory.md) |
| [Autenticação da Entidade de Serviço do Azure Active Directory](/azure/active-directory/develop/app-objects-and-service-principals) | | | | [Sim](oledb/features/using-azure-active-directory.md) |
| [Autenticação Integrada do Windows](/windows-server/security/windows-authentication/windows-authentication-overview) | Sim | [Sim](odbc/linux-mac/using-integrated-authentication.md) | [Sim](jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) | Sim |
| [Cópia em Massa](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | [Sim](../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) | [Sim](../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) | [Sim](jdbc/using-bulk-copy-with-the-jdbc-driver.md) | [Sim](oledb/features/performing-bulk-copy-operations.md) |
| [Descoberta de dados e metadados de classificação](../relational-databases/security/sql-data-discovery-and-classification.md) | [Sim](odbc/data-classification.md) | [Sim](odbc/data-classification.md) | [Sim](jdbc/data-discovery-classification-sample.md) | |
| [MARS (conjunto de resultados ativos múltiplos)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [Sim](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [Sim](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | | [Sim](oledb/features/using-multiple-active-result-sets-mars.md) |
| [Tipos de dados espaciais](../relational-databases/spatial/spatial-data-sql-server.md) | | | [Sim](jdbc/use-spatial-datatypes.md) | |
| [TVP (Parâmetros com Valor de Tabela)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | [Sim](../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md) | [Sim](../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md) | [Sim](jdbc/using-table-valued-parameters.md) | [Sim](oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md) |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sim](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sim](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sim](jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) | [Sim](oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) |
| [Resolução IP de Rede Transparente](odbc/using-transparent-network-ip-resolution.md) | [Sim](odbc/using-transparent-network-ip-resolution.md) | [Sim](odbc/using-transparent-network-ip-resolution.md) | [Sim](jdbc/setting-the-connection-properties.md) | [Sim](oledb/features/using-transparent-network-ip-resolution.md) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

| <a id="table3"></a>Recurso | [Drivers para PHP para SQL Server no Windows](php/microsoft-php-driver-for-sql-server.md)<sup>[1](#note1)</sup> | [Drivers para PHP para SQL Server no Linux e macOS](php/microsoft-php-driver-for-sql-server.md)<sup>[1](#note1)</sup> | [Tedious (Node.js)](node-js/node-js-driver-for-sql-server.md) | [pyODBC (Python)](python/pyodbc/python-sql-driver-pyodbc.md)<sup>[1](#note1)</sup> |
| :-- | :-- | :-- | :-- | :-- |
| [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [Sim](php/using-always-encrypted-php-drivers.md) | [Sim](php/using-always-encrypted-php-drivers.md) | | Sim |
| [Always Encrypted com enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [Sim](php/always-encrypted-secure-enclaves.md) | [Sim](php/always-encrypted-secure-enclaves.md) | | Sim |
| [Autenticação do Token de Acesso do Azure Active Directory](/azure/active-directory/develop/access-tokens) | [Sim](php/azure-active-directory.md) | [Sim](php/azure-active-directory.md) | [Sim](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | Sim |
| [Autenticação de Senha do Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | [Sim](php/azure-active-directory.md) | [Sim](php/azure-active-directory.md) | [Sim](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | Sim |
| [Autenticação integrada do Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | [Sim](php/azure-active-directory.md) | [Sim](php/azure-active-directory.md) | | Sim |
| [Autenticação Interativa (MFA) do Azure Active Directory](/azure/sql-database/sql-database-aad-authentication) | | | | Sim<sup>[2](#note2)</sup> |
| [Autenticação de Identidade Gerenciada do Azure Active Directory](/azure/active-directory/managed-identities-azure-resources/overview) | [Sim](php/azure-active-directory.md) | [Sim](php/azure-active-directory.md) | [Sim](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | Sim |
| [Autenticação da Entidade de Serviço do Azure Active Directory](/azure/active-directory/develop/app-objects-and-service-principals) | | | | |
| [Autenticação Integrada do Windows](/windows-server/security/windows-authentication/windows-authentication-overview) | [Sim](php/how-to-connect-using-windows-authentication.md) | [Sim](odbc/linux-mac/using-integrated-authentication.md) | | Sim |
| [Cópia em Massa](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | | | [Sim](https://tediousjs.github.io/tedious/bulk-load.html) | |
| [Descoberta de dados e metadados de classificação](../relational-databases/security/sql-data-discovery-and-classification.md) | Sim | Sim | | |
| [MARS (conjunto de resultados ativos múltiplos)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [Sim](php/how-to-disable-multiple-active-resultsets-mars.md) | [Sim](php/how-to-disable-multiple-active-resultsets-mars.md) | | Sim |
| [Tipos de dados espaciais](../relational-databases/spatial/spatial-data-sql-server.md) | | | | |
| [TVP (Parâmetros com Valor de Tabela)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | | | [Sim](https://tediousjs.github.io/tedious/parameters.html) | Sim |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [Sim](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | [Sim](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | | [Sim](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) |
| [Resolução IP de Rede Transparente](odbc/using-transparent-network-ip-resolution.md) | [Sim](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | [Sim](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | | [Sim](odbc/using-transparent-network-ip-resolution.md) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<a id="note1"></a><sup>1</sup> Como esses drivers dependem do Microsoft ODBC Driver for SQL Server, também deve ser usada uma versão desse driver que dê suporte ao recurso.

<a id="note2"></a><sup>2</sup> Somente no Windows.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
