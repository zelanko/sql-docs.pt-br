---
title: Políticas de suporte do OLE DB Driver for SQL Server
description: Saiba mais sobre as políticas de suporte para o Driver do OLE DB para SQL Server e quais sistemas operacionais e versões do banco de dados SQL são compatíveis com cada versão de driver.
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aa01dec4758bb91a4b05d65af372ee66c1c53672
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506414"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Políticas de suporte do OLE DB Driver for SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Este artigo aborda como vários componentes de acesso a dados podem ser usados com o Driver do OLE DB para SQL Server.  

## <a name="sql-version-support"></a>Suporte para versão do SQL  

O Driver do OLE DB para SQL Server é compatível e testado com conexões com as versões do SQL Server a seguir.

| Versão do banco de dados&nbsp;&#8594;<br />&#8595; Versão do driver | Banco de Dados SQL do Azure | Azure Synapse Analytics | Instância Gerenciada do Azure SQL | SQL Server 2019 | Microsoft SQL Server 2017 | SQL Server 2016 | SQL Server 2014 | SQL Server 2012 |
|----|---|---|---|---|---|---|---|---|
|18.5|Sim|Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|18.4|Sim|Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|18.3|Sim|Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|18.2|Sim|Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|18.1|Sim|Sim|Sim|   |Sim|Sim|Sim|Sim|
|18.0|Sim|Sim|Sim|   |Sim|Sim|Sim|Sim|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="supported-operating-system-versions"></a>Versões de sistemas operacionais com suporte  

A tabela a seguir lista os sistemas operacionais compatíveis com o Driver do OLE DB para SQL Server.  

| Sistema operacional&nbsp;&#8594;<br />&#8595; Versão do driver | Windows Server 2019 | Windows Server 2016 | Windows Server 2012<sup>1</sup> | Windows Server 2012 R2<sup>2</sup> | Windows 10 | Windows 8.1<sup>3</sup> |
|----|---|---|---|---|---|---|
|18.5|Sim|Sim|Sim|Sim|Sim|Sim|
|18.4|Sim|Sim|Sim|Sim|Sim|Sim|
|18.3|Sim|Sim|Sim|Sim|Sim|Sim|
|18.2|Sim|Sim|Sim|Sim|Sim|Sim|
|18.1|   |Sim|Sim|Sim|Sim|Sim|
|18.0|   |Sim|Sim|Sim|Sim|Sim|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> Compatível o Windows Server 2012 com [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061).  
<sup>2</sup> Compatível com o Windows Server 2012 R2 com a [atualização de abril de 2014](https://go.microsoft.com/fwlink/?linkid=2073785) e [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061).  
<sup>3</sup> Compatível com o Windows 8.1 com a [atualização de abril de 2014](https://go.microsoft.com/fwlink/?linkid=2073785) e [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061).  

## <a name="ado-support-policies"></a>Políticas de suporte para ADO  

Os aplicativos ADO podem usar o provedor OLE DB SQLOLEDB incluído no Windows caso não precisem dos recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior.  

Os aplicativos ADO também podem usar o Driver do OLE DB para SQL Server, mas caso façam isso, eles devem especificar `DataTypeCompatibility=80` nas cadeias de conexão. Apenas os recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] estão disponíveis quando `DataTypeCompatibility=80` está presente nas cadeias de conexão.  

## <a name="ole-db-support-policies"></a>Políticas de suporte do OLE DB  

Os aplicativos podem usar o Provedor OLE DB (SQLOLEDB) incluído no sistema operacional Windows. No entanto, isso está no modo de manutenção e não é mais atualizado. Em vez disso, use o Driver do OLE DB para SQL Server (MSOLEDBSQL).

## <a name="see-also"></a>Confira também  

[Como criar aplicativos com o OLE DB Driver para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)
