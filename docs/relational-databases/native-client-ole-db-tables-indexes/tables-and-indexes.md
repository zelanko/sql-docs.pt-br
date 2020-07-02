---
title: Tabelas e índices | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, indexes
- OLE DB, tables
- ITableDefinition interface
- tables [OLE DB]
- IIndexDefinition interface
- SQL Server Native Client OLE DB provider, tables
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: 4217c6d8-8cd2-43dc-b36f-3cfd8a58fabc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cc28a9df9b5f065314a8cd2f96a54457fa3c4b14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85658517"
---
# <a name="tables-and-indexes"></a>Tabelas e índices
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo expõe as interfaces **IIndexDefinition** e **ITableDefinition** , permitindo que os consumidores criem, alterem e removam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas e índices. As definições válidas de tabela e de índice dependem da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A capacidade de criar ou descartar tabelas e índices depende dos direitos de acesso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do usuário do aplicativo de consumidor. Descartar uma tabela pode ser uma operação ainda mais restrita pela presença de restrições de integridade referencial declarativas ou outros fatores.  
  
 A maioria dos aplicativos que visam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar o SQL-DMO em vez dessas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces do provedor de OLE DB do cliente nativo. SQL-DMO é uma coleção de objetos de automação OLE que dão suporte a todas as funções administrativas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os aplicativos destinados a vários provedores OLE DB usam essas interfaces OLE DB genéricas suportadas pelos vários provedores OLE DB.  
  
 No conjunto de propriedades específico de provedor DBPROPSET_SQLSERVERCOLUMN, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define a propriedade a seguir.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|Tipo: VT_BSTR<br /><br /> Leitura/gravação: gravação<br /><br /> Padrão: Null<br /><br /> Descrição: essa propriedade só é usada em **ITableDefinition**. A cadeia de caracteres especificada nesta propriedade é usada ao criar uma instrução [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)<br /><br /> .|  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criando tabelas do SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [Adicionando uma coluna a uma tabela do SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [Removendo uma coluna de uma tabela do SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [Descartando uma tabela do SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [Criando índices do SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [Descartando um índice do SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
