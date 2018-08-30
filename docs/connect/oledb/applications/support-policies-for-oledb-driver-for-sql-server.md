---
title: Políticas de suporte do OLE DB Driver for SQL Server | Microsoft Docs
description: Políticas de suporte do OLE DB Driver for SQL Server
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 6d71a4944aaf4fe15ba76c4d831f4809f5278f83
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021739"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Políticas de suporte do OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artigo aborda como vários componentes de acesso a dados podem ser usados com o Driver do OLE DB para SQL Server.  

## <a name="server-support"></a>Suporte de servidor  
 Driver do OLE DB para SQL Server dá suporte a conexões com [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)],[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], e [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Versões de sistemas operacionais com suporte  
 A tabela a seguir lista o suporte para quais sistemas operacionais Driver do OLE DB para SQL Server.  

|Sistemas operacionais compatíveis|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>Políticas de suporte para ADO  
 Os aplicativos ADO podem usar o provedor OLE DB SQLOLEDB incluído no Windows caso não precisem dos recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior.  

 Aplicativos ADO podem usar o Driver do OLE DB para SQL Server, mas se eles fazem isso deve especificar `DataTypeCompatibility=80` nas cadeias de conexão. Apenas os recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] estão disponíveis quando `DataTypeCompatibility=80` está presente nas cadeias de conexão.  

## <a name="ole-db-support-policies"></a>Políticas de suporte do OLE DB  
Os aplicativos podem usar o Provedor OLE DB (SQLOLEDB) incluído no sistema operacional Windows. No entanto, que está no modo de manutenção e não mais atualizados. Você deve usar o Driver do OLE DB para SQL Server (MSOLEDBSQL) em vez disso.

## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
