---
title: Políticas de suporte do Driver do OLE DB para SQL Server | Microsoft Docs
description: Políticas de suporte do Driver do OLE DB para SQL Server
ms.date: 03/26/2018
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 7660feb4b041804c33465b47d738085eecf4ca4c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Políticas de suporte do Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artigo aborda como vários componentes de acesso a dados podem ser usados com o Driver do OLE DB para SQL Server.  

## <a name="server-support"></a>Suporte de servidor  
 OLE DB Driver para SQL Server dá suporte a conexões com [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)],[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], e [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Versões de sistemas operacionais com suporte  
 A tabela a seguir lista que sistemas operacionais dão suporte a Driver OLE DB para SQL Server.  

|Sistemas operacionais com suporte|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2012 R2<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>Políticas de suporte para ADO  
 Os aplicativos ADO podem usar o provedor OLE DB SQLOLEDB incluído no Windows caso não precisem dos recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior.  

 Aplicativos ADO podem usar o Driver OLE DB para SQL Server, mas se eles fazem isso deve especificar `DataTypeCompatibility=80` nas cadeias de conexão. Apenas os recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] estão disponíveis quando `DataTypeCompatibility=80` está presente nas cadeias de conexão.  

## <a name="ole-db-support-policies"></a>Políticas de suporte do OLE DB  
Aplicativos podem usar o provedor de OLE DB (SQLOLEDB) incluído com o sistema operacional Windows. No entanto, que está no modo de manutenção e não mais atualizados. Você deve usar o Driver OLE DB para SQL Server (MSOLEDBSQL).

## <a name="see-also"></a>Consulte também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
