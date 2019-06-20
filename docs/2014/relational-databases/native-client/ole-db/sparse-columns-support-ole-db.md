---
title: Suporte a colunas esparsas (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b286ba7bde145a9a3676f38f329a8efbd932a4cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667634"
---
# <a name="sparse-columns-support-ole-db"></a>Suporte de colunas esparsas (OLE DB)
  Este tópico fornece informações o suporte OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para colunas esparsas. Para obter mais informações sobre colunas esparsas, consulte [Sparse Columns Support in SQL Server Native Client](../features/sparse-columns-support-in-sql-server-native-client.md). Para ver um exemplo, confira [Exibir metadados de colunas e de catálogos para colunas esparsas &#40;OLE DB&#41;](../../native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md).  
  
## <a name="ole-db-statement-metadata"></a>Metadados de instruções do OLE DB  
 Começando com o [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], um novo valor de sinalizador DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, está disponível. Esse valor deve ser definido para colunas que são valores `column_set`. O sinalizador DBCOLUMNFLAGS pode ser recuperado por meio de *dwFlags* parâmetro de icolumnsinfo:: Getcolumnsinfo e a coluna DBCOLUMN_FLAGS do conjunto de linhas retornado por IColumnsRowset:: Getcolumnsrowset.  
  
## <a name="ole-db-catalog-metadata"></a>Metadados de catálogo do OLE DB  
 Duas colunas específicas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adicionais foram acrescentadas a DBSCHEMA_COLUMNS.  
  
|Nome da coluna|Tipo de dados|Valor/comentários|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|Se a coluna for uma coluna esparsa, seu valor será VARIANT_TRUE; caso contrário, será VARIANT_FALSE.|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|Se a coluna for a coluna esparsa `column_set`, seu valor será VARIANT_TRUE; caso contrário, será VARIANT_FALSE.|  
  
 Também foram acrescentados dois conjuntos de linhas de esquema adicionais. Estes conjuntos de linhas têm a mesma estrutura que DBSCHEMA_COLUMNS, mas retornam conteúdo diferente. DBSCHEMA_COLUMNS_EXTENDED retorna todas as colunas, independentemente da associação `column_set`. DBSCHEMA_SPARSE_COLUMN_SET só retorna colunas que são os membros do `column_set` esparso.  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>Comportamento de DataTypeCompatibility do OLE DB  
 Comportamento com `DataTypeCompatibility=80` (na cadeia de caracteres de conexão) é consistente com um cliente [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], como a seguir:  
  
-   Os novos conjuntos de linhas de esquema não são visíveis e não há nenhuma linha para eles nos conjuntos de linhas do esquema.  
  
-   Colunas novas no conjunto de linhas COLUMNS não são visíveis.  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET não é definido para colunas `column_set`.  
  
-   DBCOMPUTEMODE_NOTCOMPUTED é definido para colunas `column_set`.  
  
## <a name="ole-db-support-for-sparse-columns"></a>Suporte do OLE DB para colunas esparsas  
 As seguintes interfaces do OLE DB foram modificadas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para dar suporte a colunas esparsas:  
  
|Tipo ou função de membro|Descrição|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|Sinalizador de DBCOLUMNFLAGS um novo valor DBCOLUMNFLAGS_SS_ISCOLUMNSET será definido para `column_set` colunas no *dwFlags*.<br /><br /> DBCOLUMNFLAGS_WRITE é definido para colunas `column_set`.|  
|IColumsRowset::GetColumnsRowset|Um novo valor de sinalizador DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, é definido para colunas `column_set` em DBCOLUMN_FLAGS.<br /><br /> DBCOLUMN_COMPUTEMODE é definido como DBCOMPUTEMODE_DYNAMIC para colunas `column_set`.|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS retorna duas colunas novas: SS_IS_COLUMN_SET e SS_IS_SPARSE.<br /><br /> DBSCHEMA_COLUMNS só retorna colunas que não são membros de um `column_set`.<br /><br /> Foram adicionados dois novos conjuntos de linhas de esquema: DBSCHEMA_COLUMNS_EXTENDED retornará todas as colunas, independentemente da dispersão de `column_set` associação. DBSCHEMA_SPARSE_COLUMN_SET só retorna colunas que são os membros de um `column_set`. Estes conjuntos de linhas novos têm as mesmas colunas e restrições que DBSCHEMA_COLUMNS.|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset::GetSchemas inclui os GUIDs para os novos conjuntos de linhas DBSCHEMA_COLUMNS_EXTENDED e DBSCHEMA_SPARSE_COLUMN_SET na lista de conjuntos de linhas de esquema disponíveis.|  
|ICommand::Execute|Se **selecionar \* partir** *tabela* é usada, ela retorna todas as colunas que não são membros de esparso `column_set`, além de uma coluna XML que contém os valores de todas as colunas não nulas que são membros de esparso `column_set`, se estiver presente.|  
|IOpenRowset::OpenRowset|IOpenRowset:: OPENROWSET retorna um conjunto de linhas com ICommand:: execute, as mesmas colunas com um **selecionar \***  consulta na mesma tabela.|  
|ITableDefinition|Não há nenhuma alteração nesta interface para colunas esparsas ou para colunas `column_set`. Aplicativos que precisam fazer modificações de esquema devem executar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] apropriado diretamente.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](sql-server-native-client-ole-db.md)  
  
  
