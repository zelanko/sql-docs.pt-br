---
title: Políticas de suporte do OLE DB Driver for SQL Server | Microsoft Docs
description: Políticas de suporte do OLE DB Driver for SQL Server
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 7aa291121c751b6634eed645fba52247849b6721
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778078"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Políticas de suporte do OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artigo aborda como vários componentes de acesso a dados podem ser usados com o Driver do OLE DB para SQL Server.  

## <a name="server-support"></a>Suporte de servidor  
 Driver do OLE DB para SQL Server dá suporte a conexões com [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], e [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Versões de sistemas operacionais com suporte  
 A tabela a seguir lista o suporte para quais sistemas operacionais Driver do OLE DB para SQL Server.  

|Sistemas operacionais compatíveis|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1 + [atualização de abril de 2014](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [atualização de abril de 2014](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>Políticas de suporte para ADO  
 Os aplicativos ADO podem usar o provedor OLE DB SQLOLEDB incluído no Windows caso não precisem dos recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior.  

 Aplicativos ADO podem usar o Driver do OLE DB para SQL Server, mas se eles fazem isso deve especificar `DataTypeCompatibility=80` nas cadeias de conexão. Apenas os recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] estão disponíveis quando `DataTypeCompatibility=80` está presente nas cadeias de conexão.  

## <a name="ole-db-support-policies"></a>Políticas de suporte do OLE DB  
Os aplicativos podem usar o Provedor OLE DB (SQLOLEDB) incluído no sistema operacional Windows. No entanto, que está no modo de manutenção e não mais atualizados. Use o Driver do OLE DB para SQL Server (MSOLEDBSQL).

## <a name="see-also"></a>Confira também  
 [Como criar aplicativos com o OLE DB Driver para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
