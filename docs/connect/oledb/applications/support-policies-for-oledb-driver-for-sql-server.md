---
title: Políticas de suporte do OLE DB Driver for SQL Server | Microsoft Docs
description: Políticas de suporte do OLE DB Driver for SQL Server
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b02789c787266a3370e3c5c9bfae50ea337d19db
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "72381857"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Políticas de suporte do OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artigo aborda como vários componentes de acesso a dados podem ser usados com o Driver do OLE DB para SQL Server.  

## <a name="server-support"></a>Suporte de servidor  
 O Driver do OLE DB para SQL Server dá suporte a conexões para [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] via [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Versões de sistemas operacionais com suporte  
 A tabela a seguir lista os sistemas operacionais dão suporte ao Driver do OLE DB para SQL Server.  

| Sistemas operacionais compatíveis |  |
|--------------------------------------|---------------------------------|   
| Microsoft Windows 8.1 + [Atualização de abril de 2014](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [Atualização de abril de 2014](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016<br /><br />Microsoft Windows Server 2019 |  |


## <a name="ado-support-policies"></a>Políticas de suporte para ADO  
 Os aplicativos ADO podem usar o provedor OLE DB SQLOLEDB incluído no Windows caso não precisem dos recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior.  

 Os aplicativos ADO também podem usar o Driver do OLE DB para SQL Server, mas caso façam isso, eles devem especificar `DataTypeCompatibility=80` nas cadeias de conexão. Apenas os recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] estão disponíveis quando `DataTypeCompatibility=80` está presente nas cadeias de conexão.  

## <a name="ole-db-support-policies"></a>Políticas de suporte do OLE DB  
Os aplicativos podem usar o Provedor OLE DB (SQLOLEDB) incluído no sistema operacional Windows. No entanto, isso está no modo de manutenção e não é mais atualizado. Em vez disso, use o Driver do OLE DB para SQL Server (MSOLEDBSQL).

## <a name="see-also"></a>Confira também  
 [Como criar aplicativos com o OLE DB Driver para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
