---
title: Suporte a colunas esparsas (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 25e45c61290a45240d5e4595a015b543ed89db29
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409095"
---
# <a name="sparse-columns-support-ole-db"></a>Suporte de colunas esparsas (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Este tópico fornece informações o suporte OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para colunas esparsas. Para obter mais informações sobre colunas esparsas, consulte [Sparse Columns Support in SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md). Para obter um exemplo, consulte [coluna de exibição e os metadados de catálogo para colunas esparsas &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md).  
  
## <a name="ole-db-statement-metadata"></a>Metadados de instruções do OLE DB  
 Começando com o [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], um novo valor de sinalizador DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, está disponível. Esse valor deve ser definido para colunas que são **column_set** valores. O sinalizador DBCOLUMNFLAGS pode ser recuperado por meio de *dwFlags* parâmetro de icolumnsinfo:: Getcolumnsinfo e a coluna DBCOLUMN_FLAGS do conjunto de linhas retornado por IColumnsRowset:: Getcolumnsrowset.  
  
## <a name="ole-db-catalog-metadata"></a>Metadados de catálogo do OLE DB  
 Duas colunas específicas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adicionais foram acrescentadas a DBSCHEMA_COLUMNS.  
  
|Nome da coluna|Tipo de dados|Valor/comentários|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|Se a coluna for uma coluna esparsa, seu valor será VARIANT_TRUE; caso contrário, será VARIANT_FALSE.|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|Se a coluna é esparso **column_set** coluna, isso tem o valor será VARIANT_TRUE; caso contrário, VARIANT_FALSE.|  
  
 Também foram acrescentados dois conjuntos de linhas de esquema adicionais. Estes conjuntos de linhas têm a mesma estrutura que DBSCHEMA_COLUMNS, mas retornam conteúdo diferente. DBSCHEMA_COLUMNS_EXTENDED retorna todas as colunas, independentemente de **column_set** associação. DBSCHEMA_SPARSE_COLUMN_SET só retorna colunas que são membros de esparso **column_set**.  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>Comportamento de DataTypeCompatibility do OLE DB  
 Comportamento com **DataTypeCompatibility = 80** (na cadeia de conexão) é consistente com um [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] cliente, da seguinte maneira:  
  
-   Os novos conjuntos de linhas de esquema não são visíveis e não há nenhuma linha para eles nos conjuntos de linhas do esquema.  
  
-   Colunas novas no conjunto de linhas COLUMNS não são visíveis.  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET não está definido para **column_set** colunas.  
  
-   DBCOMPUTEMODE_NOTCOMPUTED é definido para **column_set** colunas.  
  
## <a name="ole-db-support-for-sparse-columns"></a>Suporte do OLE DB para colunas esparsas  
 As seguintes interfaces do OLE DB foram modificadas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para dar suporte a colunas esparsas:  
  
|Tipo ou função de membro|Description|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|Sinalizador de DBCOLUMNFLAGS um novo valor DBCOLUMNFLAGS_SS_ISCOLUMNSET será definido para **column_set** colunas *dwFlags*.<br /><br /> DBCOLUMNFLAGS_WRITE é definido para **column_set** colunas.|  
|IColumsRowset::GetColumnsRowset|Um novo valor de sinalizador DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, é definido para **column_set** colunas em DBCOLUMN_FLAGS.<br /><br /> DBCOLUMN_COMPUTEMODE é definido como DBCOMPUTEMODE_DYNAMIC para **column_set** colunas.|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS retorna duas colunas novas: SS_IS_COLUMN_SET e SS_IS_SPARSE.<br /><br /> DBSCHEMA_COLUMNS só retorna colunas que não são membros de um **column_set**.<br /><br /> Foram adicionados dois novos conjuntos de linhas de esquema: DBSCHEMA_COLUMNS_EXTENDED retornará todas as colunas, independentemente da dispersão de **column_set** associação. DBSCHEMA_SPARSE_COLUMN_SET só retorna colunas que são membros de um **column_set**. Estes conjuntos de linhas novos têm as mesmas colunas e restrições que DBSCHEMA_COLUMNS.|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset::GetSchemas inclui as GUIDs para os novos conjuntos de linhas DBSCHEMA_COLUMNS_EXTENDED e DBSCHEMA_SPARSE_COLUMN_SET na lista de conjuntos de linhas de esquema disponíveis.|  
|ICommand::Execute|Se **selecionar \* partir** *tabela* é usada, ela retorna todas as colunas que não são membros de esparso **column_set**, além de uma coluna XML que contém os valores de todos os colunas não nulas que são membros de esparso **column_set**, se estiver presente.|  
|IOpenRowset::OpenRowset|IOpenRowset:: OPENROWSET retorna um conjunto de linhas com ICommand:: execute, as mesmas colunas com um **selecionar \***  consulta na mesma tabela.|  
|ITableDefinition|Não há nenhuma alteração nesta interface para colunas esparsas ou para **column_set** colunas. Aplicativos que precisam fazer modificações de esquema devem executar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] apropriado diretamente.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
