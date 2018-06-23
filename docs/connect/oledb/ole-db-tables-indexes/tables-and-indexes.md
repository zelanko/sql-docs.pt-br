---
title: Tabelas e índices | Microsoft Docs
description: Criando, alterando e droping tabelas e índices usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, indexes
- OLE DB, tables
- ITableDefinition interface
- tables [OLE DB]
- IIndexDefinition interface
- OLE DB Driver for SQL Server, tables
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 962efa70c583bdb9aa9537826800c1c166350dc4
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689339"
---
# <a name="tables-and-indexes"></a>Tabelas e índices
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver OLE DB para SQL Server expõe o **IIndexDefinition** e **ITableDefinition** interfaces, permitindo que os consumidores criar, alterar e descartar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabelas e índices. As definições válidas de tabela e de índice dependem da versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 A capacidade de criar ou descartar tabelas e índices depende dos direitos de acesso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do usuário do aplicativo de consumidor. Descartar uma tabela pode ser uma operação ainda mais restrita pela presença de restrições de integridade referencial declarativas ou outros fatores.  
  
 A maioria dos aplicativos voltados para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usar SQL-DMO em vez desses Driver OLE DB para SQL Server interfaces. SQL-DMO é uma coleção de objetos de automação OLE que dão suporte a todas as funções administrativas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os aplicativos destinados a vários provedores OLE DB usam essas interfaces OLE DB genéricas suportadas pelos vários provedores OLE DB.  
  
 No conjunto de propriedades específico de provedor DBPROPSET_SQLSERVERCOLUMN, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] define a propriedade a seguir.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|Tipo: VT_BSTR<br /><br /> Leitura/gravação: gravação<br /><br /> Padrão: Null<br /><br /> Descrição: Esta propriedade é usada somente em **ITableDefinition**. A cadeia de caracteres especificada por esta propriedade é usada ao criar um [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md)<br /><br /> .|  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criando tabelas do SQL Server](../../oledb/ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [Adicionando uma coluna a uma tabela do SQL Server](../../oledb/ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [Removendo uma coluna de uma tabela do SQL Server](../../oledb/ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [Descartando uma tabela do SQL Server](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [Criando índices do SQL Server](../../oledb/ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [Descartando um índice do SQL Server](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>Consulte também  
 [Driver do OLE DB para programação do SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
