---
title: Tabelas e índices | Microsoft Docs
description: Criando, alterando e removendo tabelas e índices usando OLE DB driver para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
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
ms.author: pelopes
ms.openlocfilehash: 0fc8aeed348f64c17894fa3432a7a81274ffbea4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015241"
---
# <a name="tables-and-indexes"></a>Tabelas e índices
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O OLE DB Driver for SQL Server expõe as interfaces **IIndexDefinition** e **ITableDefinition**, permitindo que os consumidores criem, alterem e descartem tabelas e índices do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. As definições válidas de tabela e de índice dependem da versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 A capacidade de criar ou descartar tabelas e índices depende dos direitos de acesso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do usuário do aplicativo de consumidor. Descartar uma tabela pode ser uma operação ainda mais restrita pela presença de restrições de integridade referencial declarativas ou outros fatores.  
  
 A maioria dos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplicativos que visam usar o SQL-DMO em vez desses OLE DB driver para interfaces SQL Server. SQL-DMO é uma coleção de objetos de automação OLE que dão suporte a todas as funções administrativas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os aplicativos destinados a vários provedores OLE DB usam essas interfaces OLE DB genéricas suportadas pelos vários provedores OLE DB.  
  
 No conjunto de propriedades específico de provedor DBPROPSET_SQLSERVERCOLUMN, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] define a propriedade a seguir.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|Tipo: VT_BSTR<br /><br /> Leitura/gravação: gravação<br /><br /> Padrão: Null<br /><br /> Descrição: essa propriedade só é usada em **ITableDefinition**. A cadeia de caracteres especificada nesta propriedade é usada ao criar uma instrução [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md)<br /><br /> .|  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criando tabelas do SQL Server](../../oledb/ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [Adicionando uma coluna a uma tabela do SQL Server](../../oledb/ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [Removendo uma coluna de uma tabela do SQL Server](../../oledb/ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [Descartando uma tabela do SQL Server](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [Criando índices do SQL Server](../../oledb/ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [Descartando um índice do SQL Server](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no OLE DB Driver for SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
