---
title: Suporte a colunas esparsas no OLE DB Driver for SQL Server | Microsoft Docs
description: Suporte a colunas esparsas no OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sparse columns, OLE DB Driver for SQL Server
- sparse columns, OLE DB
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7b617ecdbf2977372dbb006baaec4c791b988ef8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988909"
---
# <a name="sparse-columns-support-in-ole-db-driver-for-sql-server"></a>Suporte a colunas esparsas no OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O driver de OLE DB para SQL Server dá suporte a colunas esparsas. Para obter mais informações sobre colunas esparsas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [usar colunas esparsas](../../../relational-databases/tables/use-sparse-columns.md) e [usar conjuntos](../../../relational-databases/tables/use-column-sets.md)de colunas.  
  
 Para obter mais informações sobre o suporte a colunas esparsas no driver OLE DB para SQL Server, as [colunas esparsas dão suporte &#40;a OLE DB&#41;](../../oledb/ole-db/sparse-columns-support-ole-db.md).  
  
 Para obter informações sobre aplicativos de exemplo que demonstram esse recurso, confira [Amostras de programação do SQL Server Data](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-ole-db-driver-for-sql-server"></a>Cenários de usuário para colunas esparsas e OLE DB driver para SQL Server  
 A tabela a seguir resume os cenários comuns de usuário para OLE DB driver para SQL Server usuários com colunas esparsas:  
  
|Cenário|Comportamento|  
|--------------|--------------|  
|**selecione\* da tabela** ou IOpenRowset:: OPENROWSET.|Retorna todas as colunas que não são membros do **column_set** esparso, além de uma coluna XML que contém os valores de todas as colunas não nulas que são membros do **column_set** esparso.|  
|Referenciar uma coluna por nome.|A coluna pode ser referenciada, independentemente de seu status de coluna esparsa ou associação ao **column_set**.|  
|Acessar colunas de membro do **column_set** por meio de uma coluna XML computada.|As colunas que são membros do **column_set** esparso podem ser acessadas selecionando o **column_set** por nome e podem ter valores inseridos e atualizados atualizando o XML na coluna **column_set**.<br /><br /> O valor precisa estar em conformidade com o esquema para colunas **column_set**.|  
|Recupere metadados para todas as colunas em uma tabela por meio do conjunto de linhas de esquema DBSCHEMA_COLUMNS sem restrição de coluna (OLE DB).|Retorna uma linha para todas as colunas que não são membros de um **column_set**. Se a tabela tiver um **column_set** esparso, uma linha será retornada para ela.<br /><br /> Observe que isso não retorna os metadados para colunas que são membros de um **column_set**.|  
|Recuperar metadados para todas as colunas, independentemente da dispersão ou da associação em um **column_set**. Essa ação pode retornar um número muito grande de linhas.|Chame IDBSchemaRowset:: GetRowset para o conjunto de linhas de esquema DBSCHEMA_COLUMNS_EXTENDED.|  
|Recuperar metadados somente para colunas que são membros de um **column_set**. Essa ação pode retornar um número muito grande de linhas.|Chame IDBSchemaRowset:: GetRowset para o conjunto de linhas de esquema DBSCHEMA_SPARSE_COLUMN_SET.|  
|Determinar se uma coluna está esparsa.|Consulte a coluna SS_IS_SPARSE do conjunto de linhas de esquema de DBSCHEMA_COLUMNS (OLE DB).|  
|Determine se uma coluna é **column_set**.|Consulte a coluna SS_IS_COLUMN_SET do conjunto de linhas de esquema de DBSCHEMA_COLUMNS. Ou, consulte *dwFlags* retornado por IColumnsInfo:: GETCOLUMNINFO ou DBCOLUMNFLAGS no conjunto de linhas retornado por IColumnsRowset:: GetColumnsRowset. Para colunas **column_set**, DBCOLUMNFLAGS_SS_ISCOLUMNSET será definido.|  
|Importar e exportar colunas esparsas por BCP para uma tabela sem **column_set**.|Nenhuma alteração no comportamento de versões anteriores do OLE DB driver para SQL Server.|  
|Importar e exportar colunas esparsas por BCP para uma tabela com um **column_set**.|O **column_set** é importado e exportado da mesma forma que o XML; ou seja, como **varbinary (max)** se estiver associado como um tipo binário, ou como **nvarchar (max)** , se associado como um tipo **Char** ou **WCHAR** .<br /><br /> As colunas que são membros do **column_set** esparso não são exportadas como colunas distintas; elas só são exportadas no valor do **column_set**.|  
|comportamento de **consulta** do bcp.|Nenhuma alteração na manipulação de colunas nomeadas explicitamente de versões anteriores do OLE DB driver para SQL Server.<br /><br /> Cenários que envolvem importação e exportação entre tabelas com esquemas diferentes podem exigir manipulação especial.<br /><br /> Para obter mais informações sobre BCP, consulte Suporte de BCP (cópia em massa) a colunas esparsas, mais adiante neste tópico.|  
  
## <a name="down-level-client-behavior"></a>Comportamento do cliente de versão anterior  
 Os clientes de nível inferior só retornarão metadados para colunas que não são membros do **column_set** esparso para SQLColumns e DBSCHMA_COLUMNS.
  
 Os clientes de nível inferior podem acessar as colunas que são membros do **column_set** esparso por nome, e a coluna **column_set** ficará acessível como uma coluna XML aos clientes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Suporte de BCP (cópia em massa) a colunas esparsas  
 Não há nenhuma alteração na API de BCP no OLE DB para as colunas esparsas ou os recursos de **column_set**.  
  
 Se uma tabela tiver um **column_set**, as colunas esparsas não serão tratadas como colunas distintas. Os valores de todas as colunas esparsas são incluídos no valor de **column_set**, que é exportado da mesma maneira que uma coluna XML; ou seja, como **varbinary (max)** se associado como um tipo binário, ou como **nvarchar (max)** , se associado como um tipo **Char** ou **WCHAR** ). Na importação, o valor **column_set** deve estar de acordo com o esquema do **column_set**.  
  
 Para operações **queryout**, não há alterações na maneira como são tratadas as colunas referenciadas explicitamente. As colunas de **column_set** têm o mesmo comportamento das colunas XML e a dispersão não tem nenhum efeito sobre o tratamento de colunas esparsas nomeadas.  
  
 Entretanto, se **queryout** for usado para exportação e você referenciar colunas esparsas que são membros do conjunto de colunas esparsas por nome, você não poderá executar uma importação direta para uma tabela de estrutura semelhante. Isso acontece porque o BCP usa metadados de maneira consistente com uma operação **select \*** para a importação e não consegue corresponder às colunas de membro de **column_set** com esses metadados. Para importar as colunas de membro de **column_set** individualmente, você precisa definir uma exibição na tabela que referencia as colunas do **column_set** desejadas, além de executar a operação de importação usando a exibição.  
  
## <a name="see-also"></a>Consulte Também  
 [Driver do OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server.md)  
  
  
