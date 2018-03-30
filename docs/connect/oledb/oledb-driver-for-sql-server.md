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
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: article
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 89e66fe2c61ae17a43e2a58071ba04374f33ea04
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-driver-for-sql-server"></a>Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL ou OLE DB Driver para SQL Server, é um termo que tenha sido usado alternadamente para se referir ao Driver do OLE DB para SQL Server.

## <a name="different-incarnations-of-ole-db-drivers"></a>Encarnação diferentes dos Drivers do OLE DB

Há três encarnação distintas do provedor Microsoft OLE DB para SQL Server.


### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Provedor Microsoft OLE DB para SQL Server (SQLOLEDB)

O [Microsoft OLE DB Provider para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) ainda é fornecido como parte do [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx). Não é recomendável usar esse driver para novo desenvolvimento.


### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)

A partir do SQL Server 2005, o [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) inclui uma interface de provedor do OLE DB (SQLNCLI) e é o provedor OLE DB que acompanha o SQL Server 2005 por meio de 2017 do SQL Server.

Foi [anunciados como substituídos no 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e não é recomendável usar esse driver para novo desenvolvimento.


### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Driver do Microsoft OLE DB para SQL Server (MSOLEDBSQL)

OLE DB foi [anunciado como undeprecated em 2017](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/). Uma nova versão planejada foi anunciada para 2018.

O novo provedor de OLE DB é chamado de Driver OLE DB da Microsoft para SQL Server (MSOLEDBSQL). O novo provedor será atualizado com os recursos de servidor mais recentes no futuro.

Informações sobre o Driver OLE DB para recursos do SQL Server:

-   [Driver do OLE DB para SQL Server Support for LocalDB](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [Descoberta de metadados](../oledb/features/metadata-discovery.md)  

-   [Suporte a UTF-16 no Driver do OLE DB para SQL Server](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [Driver do OLE DB para SQL Server Support for High Availability, Disaster Recovery](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [Acessar informações de diagnóstico nos logs de eventos estendidos](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>Consulte também  
[Instale o Driver do OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
 [Driver do OLE DB para recursos do SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )  
