---
title: Driver do OLE DB para SQL Server | Microsoft Docs
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
description: ''
ms.custom: ''
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5f009cf311c1eb395915e017bf202abea5ae5290
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="ole-db-driver-for-sql-server"></a>Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL ou OLE DB Driver para SQL Server, é um termo usado alternadamente para se referir ao Driver do OLE DB para SQL Server.

## <a name="different-generations-of-ole-db-drivers"></a>Diferentes gerações de Drivers do OLE DB

Há três gerações distintas do provedor Microsoft OLE DB para SQL Server.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Provedor Microsoft OLE DB para SQL Server (SQLOLEDB)
O [Microsoft OLE DB Provider para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) ainda é fornecido como parte do [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx). Não é mais mantido e não é recomendável usar esse driver para novo desenvolvimento. 


### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)
A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) inclui uma interface de provedor do OLE DB (SQLNCLI) e é o provedor OLE DB que acompanha [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] por meio de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

Foi [anunciados como substituídos no 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e não é recomendável usar esse driver para novo desenvolvimento. Para obter mais informações sobre o ciclo de vida SNAC e downloads disponíveis, consulte [SNAC de ciclo de vida explicado](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Driver do Microsoft OLE DB para SQL Server (MSOLEDBSQL)
OLE DB foi [undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) lançado em 2018 e pode ser baixado [aqui](https://go.microsoft.com/fwlink/?linkid=871294).

O novo provedor de OLE DB é chamado de Driver OLE DB da Microsoft para SQL Server (MSOLEDBSQL). O novo provedor será atualizado com os recursos de servidor mais recentes no futuro.

> [!NOTE]
> Para usar o novo Microsoft OLE DB Driver para SQL Server nos aplicativos existentes, você deve planejar converter cadeias de caracteres de conexão do SQLOLEDB ou SQLNCLI, para MSOLEDBSQL.   

Informações sobre o Driver OLE DB para recursos do SQL Server:

-   [Suporte ao Driver do OLE DB para SQL Server para LocalDB](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [Descoberta de metadados](../oledb/features/metadata-discovery.md)  

-   [Suporte ao UTF-16 no Driver do OLE DB para SQL Server](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [Suporte ao Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastre](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [Acessar informações de diagnóstico nos logs de eventos estendidos](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>Consulte também  
[Instale o Driver do OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)     
[Recursos do Driver do OLE DB para SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )     
