---
title: Suporte a colunas esparsas no Driver do OLE DB para SQL Server | Microsoft Docs
description: Suporte a colunas esparsas no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sparse columns, OLE DB Driver for SQL Server
- sparse columns, OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffb8b7f18cf9c1653e5c77217f1d1dd339333fcf
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="sparse-columns-support-in-ole-db-driver-for-sql-server"></a>Suporte a colunas esparsas no Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver para SQL Server dá suporte a colunas esparsas. Para obter mais informações sobre colunas esparsas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [usar colunas esparsas](../../../relational-databases/tables/use-sparse-columns.md) e [usar conjuntos de colunas](../../../relational-databases/tables/use-column-sets.md).  
  
 Para obter mais informações sobre suporte a colunas esparsas no Driver do OLE DB para SQL Server, [suporte a colunas esparsas &#40;OLE DB&#41;](../../oledb/ole-db/sparse-columns-support-ole-db.md).  
  
 Para obter informações sobre aplicativos de exemplo que demonstram esse recurso, consulte [exemplos de programação de dados do SQL Server](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-ole-db-driver-for-sql-server"></a>Cenários de usuário para as colunas esparsas e o Driver do OLE DB para SQL Server  
 A tabela a seguir resume os cenários comuns de usuário para o Driver do OLE DB para usuários do SQL Server com as colunas esparsas:  
  
|Cenário|Comportamento|  
|--------------|--------------|  
|**Selecione \* da tabela** ou IOpenRowset:: OPENROWSET.|Retorna todas as colunas que não são membros de esparso **column_set**, além de uma coluna XML que contém os valores de todas as colunas não nulas que são membros de esparso **column_set**.|  
|Referenciar uma coluna por nome.|A coluna pode ser referenciada independentemente de seu status de coluna esparsa ou **column_set** associação.|  
|Acesso **column_set** colunas de membro por meio de uma coluna XML computada.|Colunas que são membros de esparso **column_set** podem ser acessadas selecionando o **column_set** por nome e podem ter valores inseridos e atualizados atualizando o XML no **column_set** coluna.<br /><br /> O valor deve estar de acordo com o esquema para **column_set** colunas.|  
|Recupere metadados para todas as colunas em uma tabela no conjunto de linhas de esquema DBSCHEMA_COLUMNS sem restrição de coluna (OLE DB).|Retorna uma linha para todas as colunas que não são membros de um **column_set**. Se a tabela tiver um esparso **column_set**, uma linha será retornada para ela.<br /><br /> Observe que isso não retorna metadados para colunas que são membros de um **column_set**.|  
|Recuperar metadados para todas as colunas, independentemente de dispersão ou associação em um **column_set**. Essa ação pode retornar um número muito grande de linhas.|Chame IDBSchemaRowset:: Getrowset para o conjunto de linhas do esquema DBSCHEMA_COLUMNS_EXTENDED.|  
|Recuperar metadados somente para colunas que são membros de um **column_set**. Essa ação pode retornar um número muito grande de linhas.|Chame IDBSchemaRowset:: Getrowset para o conjunto de linhas do esquema DBSCHEMA_SPARSE_COLUMN_SET.|  
|Determinar se uma coluna está esparsa.|Consulte a coluna SS_IS_SPARSE do conjunto de linhas de esquema de DBSCHEMA_COLUMNS (OLE DB).|  
|Determinar se uma coluna é uma **column_set**.|Consulte a coluna SS_IS_COLUMN_SET do conjunto de linhas de esquema de DBSCHEMA_COLUMNS. Ou então, consulte *dwFlags* retornado por icolumnsinfo:: Getcolumninfo ou DBCOLUMNFLAGS no conjunto de linhas retornado por Getcolumnsrowset. Para **column_set** colunas, DBCOLUMNFLAGS_SS_ISCOLUMNSET será definido.|  
|Importar e exportar colunas esparsas por BCP para uma tabela sem nenhum **column_set**.|Nenhuma alteração no comportamento de versões anteriores do Driver do OLE DB para SQL Server.|  
|Importar e exportar colunas esparsas por BCP para uma tabela com um **column_set**.|O **column_set** é importado e exportado da mesma maneira como XML; ou seja, como **varbinary (max)** se associado como tipo binário ou como **nvarchar (max)** se associados como uma **char** ou **wchar** tipo.<br /><br /> Colunas que são membros de esparso **column_set** não são exportadas como colunas distintas; elas só são exportadas no valor da **column_set**.|  
|**QUERYOUT** comportamento para BCP.|Nenhuma alteração na manipulação de colunas nomeadas explicitamente de versões anteriores do Driver do OLE DB para SQL Server.<br /><br /> Cenários que envolvem importação e exportação entre tabelas com esquemas diferentes podem exigir manipulação especial.<br /><br /> Para obter mais informações sobre BCP, consulte Suporte de BCP (cópia em massa) a colunas esparsas, mais adiante neste tópico.|  
  
## <a name="down-level-client-behavior"></a>Comportamento do cliente de versão anterior  
 Clientes de nível inferior retornarão metadados somente para colunas que não são membros de esparso **column_set** para SQLColumns e DBSCHMA_COLUMNS.
  
 Clientes de nível inferior podem acessar as colunas que são membros de esparso **column_set** por nome e o **column_set** coluna poderá ser acessada como uma coluna XML para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] os clientes.  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Suporte de BCP (cópia em massa) a colunas esparsas  
 Não há nenhuma alteração à API do BCP no OLE DB para as colunas esparsas ou **column_set** recursos.  
  
 Se uma tabela tiver um **column_set**, as colunas esparsas não são tratadas como colunas distintas. Os valores de todas as colunas esparsas são incluídos no valor da **column_set**, que é exportado da mesma forma que uma coluna XML; ou seja, como **varbinary (max)** se associado como tipo binário ou como  **nvarchar (max)** se associados como uma **char** ou **wchar** tipo). Na importação, o **column_set** valor deve estar de acordo com o esquema do **column_set**.  
  
 Para **queryout** operações, não há nenhuma alteração na forma como são tratadas as colunas referenciadas explicitamente. **column_set** colunas têm o mesmo comportamento das colunas XML e dispersão não tem efeito sobre o tratamento de colunas esparsas nomeadas.  
  
 No entanto, se **queryout** é usado para exportar e fazer referência a colunas esparsas que são membros da coluna esparsa definido por nome, você não pode executar uma importação direta para uma tabela de estrutura semelhante. Isso ocorre porque o BCP usa metadados consistentes com um **selecione \***  operação para a importação e não pode corresponder **column_set** colunas de membro com esses metadados. Para importar **column_set** colunas de membro individualmente, você deve definir uma exibição em uma tabela que faz referência a desejado **column_set** colunas e você deve executar a operação de importação usando o modo de exibição.  
  
## <a name="see-also"></a>Consulte também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server-programming.md)  
  
  
