---
title: Suporte a colunas esparsas (OLE DB) | Microsoft Docs
description: Suporte a colunas esparsas (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 1cfbd5bce17c658a7dff33bc7a590a22d525c193
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43018185"
---
# <a name="sparse-columns-support-ole-db"></a>Suporte de colunas esparsas (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este tópico fornece informações sobre o Driver do OLE DB para o suporte do SQL Server para colunas esparsas. Para obter mais informações sobre colunas esparsas, consulte [suporte a colunas esparsas no Driver do OLE DB para SQL Server](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md). [Exibir metadados de colunas e catálogos para colunas esparsas &#40;OLE DB&#41;](../../oledb/ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md)  
  
## <a name="ole-db-statement-metadata"></a>Metadados de instruções do OLE DB  
 Começando com o [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], um novo valor de sinalizador DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, está disponível. Esse valor deve ser definido para colunas que são valores **column_set**. O sinalizador DBCOLUMNFLAGS pode ser recuperado por meio de *dwFlags* parâmetro de icolumnsinfo:: Getcolumnsinfo e a coluna DBCOLUMN_FLAGS do conjunto de linhas retornado por IColumnsRowset:: Getcolumnsrowset.  
  
## <a name="ole-db-catalog-metadata"></a>Metadados de catálogo do OLE DB  
 Duas colunas específicas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adicionais foram acrescentadas a DBSCHEMA_COLUMNS.  
  
|Nome da coluna|Tipo de dados|Valor/comentários|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|Se a coluna for uma coluna esparsa, seu valor será VARIANT_TRUE; caso contrário, será VARIANT_FALSE.|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|Se a coluna for a coluna **column_set** esparsa, seu valor será VARIANT_TRUE; caso contrário, será VARIANT_FALSE.|  
  
 Também foram acrescentados dois conjuntos de linhas de esquema adicionais. Estes conjuntos de linhas têm a mesma estrutura que DBSCHEMA_COLUMNS, mas retornam conteúdo diferente. DBSCHEMA_COLUMNS_EXTENDED retorna todas as colunas, independentemente da associação a **column_set**. DBSCHEMA_SPARSE_COLUMN_SET só retorna colunas que são os membros do **column_set** esparso.  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>Comportamento de DataTypeCompatibility do OLE DB  
 Comportamento com **DataTypeCompatibility = 80** (na cadeia de conexão) é consistente com um [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] cliente, da seguinte maneira:  
  
-   Os novos conjuntos de linhas de esquema não são visíveis e não há nenhuma linha para eles nos conjuntos de linhas do esquema.  
  
-   Colunas novas no conjunto de linhas COLUMNS não são visíveis.  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET não é definido para colunas **column_set**.  
  
-   DBCOMPUTEMODE_NOTCOMPUTED é definido para colunas **column_set**.  
  
## <a name="ole-db-support-for-sparse-columns"></a>Suporte do OLE DB para colunas esparsas  
 As seguintes interfaces OLE DB foram modificadas no Driver do OLE DB para SQL Server dar suporte a colunas esparsas:  
  
|Tipo ou função de membro|Descrição|  
|-----------------------------|-----------------|  
|Icolumnsinfo:: Getcolumnsinfo|Um novo valor de sinalizador DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, é definido para colunas **column_set** em *dwFlags*.<br /><br /> DBCOLUMNFLAGS_WRITE é definido para colunas **column_set**.|  
|IColumsRowset::GetColumnsRowset|Um novo valor de sinalizador DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, é definido para colunas **column_set** em DBCOLUMN_FLAGS.<br /><br /> DBCOLUMN_COMPUTEMODE é definido como DBCOMPUTEMODE_DYNAMIC para colunas **column_set**.|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS retorna duas colunas novas: SS_IS_COLUMN_SET e SS_IS_SPARSE.<br /><br /> DBSCHEMA_COLUMNS só retorna colunas que não são membros de um **column_set**.<br /><br /> Foram adicionados dois novos conjuntos de linhas de esquema: DBSCHEMA_COLUMNS_EXTENDED retornará todas as colunas, independentemente da dispersão da associação a **column_set**. DBSCHEMA_SPARSE_COLUMN_SET só retorna colunas que são os membros de um **column_set**. Estes conjuntos de linhas novos têm as mesmas colunas e restrições que DBSCHEMA_COLUMNS.|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset::GetSchemas inclui os GUIDs para os novos conjuntos de linhas DBSCHEMA_COLUMNS_EXTENDED e DBSCHEMA_SPARSE_COLUMN_SET na lista de conjuntos de linhas de esquema disponíveis.|  
|ICommand::Execute|Se **select \* from** *table* for usado, ele retornará todas as colunas que não são membros do **column_set** esparso, além de uma coluna XML que contém os valores de todas as colunas não nulas que são membros do **column_set** esparso, se estiver presente.|  
|IOpenRowset::OpenRowset|IOpenRowset:: OPENROWSET retorna um conjunto de linhas com ICommand:: execute, as mesmas colunas com um **selecionar \***  consulta na mesma tabela.|  
|ITableDefinition|Não há nenhuma alteração nessa interface em colunas esparsas ou em colunas **column_set**. Aplicativos que precisam fazer modificações de esquema devem executar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] apropriado diretamente.|  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
