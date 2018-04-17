---
title: Suporte a colunas esparsas no SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7f4d77722108f82733978b5b2c778ddfbfb958c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>Suporte a colunas esparsas no SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client suporta colunas esparsas. Para obter mais informações sobre colunas esparsas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [usar colunas esparsas](../../../relational-databases/tables/use-sparse-columns.md) e [usar conjuntos de colunas](../../../relational-databases/tables/use-column-sets.md).  
  
 Para obter mais informações sobre colunas esparsas suporte no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, consulte [suporte a colunas esparsas &#40;ODBC&#41; ](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md) e [suporte a colunas esparsas &#40;OLE DB&#41; ](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md) .  
  
 Para obter informações sobre aplicativos de exemplo que demonstram esse recurso, consulte [exemplos de programação de dados do SQL Server](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>Cenários de usuário para colunas esparsas e o SQL Server Native Client  
 A tabela a seguir resume os cenários comuns para usuários do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client com colunas esparsas:  
  
|Cenário|Comportamento|  
|--------------|--------------|  
|**Selecione \* da tabela** ou IOpenRowset:: OPENROWSET.|Retorna todas as colunas que não são membros de esparso **column_set**, além de uma coluna XML que contém os valores de todas as colunas não nulas que são membros de esparso **column_set**.|  
|Referenciar uma coluna por nome.|A coluna pode ser referenciada independentemente de seu status de coluna esparsa ou **column_set** associação.|  
|Acesso **column_set** colunas de membro por meio de uma coluna XML computada.|Colunas que são membros de esparso **column_set** podem ser acessadas selecionando o **column_set** por nome e podem ter valores inseridos e atualizados atualizando o XML no **column_set** coluna.<br /><br /> O valor deve estar de acordo com o esquema para **column_set** colunas.|  
|Recuperar metadados para todas as colunas em uma tabela por meio de SQLColumns com um padrão de pesquisa de coluna de NULL ou '%' (ODBC); ou por meio do conjunto de linhas de esquema DBSCHEMA_COLUMNS sem restrição de coluna (OLE DB).|Retorna uma linha para todas as colunas que não são membros de um **column_set**. Se a tabela tiver um esparso **column_set**, uma linha será retornada para ela.<br /><br /> Observe que isso não retorna metadados para colunas que são membros de um **column_set**.|  
|Recuperar metadados para todas as colunas, independentemente de dispersão ou associação em um **column_set**. Essa ação pode retornar um número muito grande de linhas.|Defina o campo do descritor SQL_SOPT_SS_NAME_SCOPE como SQL_SS_NAME_SCOPE_EXTENDED e chame [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) (ODBC).<br /><br /> Chame IDBSchemaRowset:: Getrowset para o conjunto de linhas de esquema DBSCHEMA_COLUMNS_EXTENDED (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. No entanto, esse aplicativo poderia consultar exibições de sistema diretamente.|  
|Recuperar metadados somente para colunas que são membros de um **column_set**. Essa ação pode retornar um número muito grande de linhas.|Defina o campo do descritor SQL_SOPT_SS_NAME_SCOPE como SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET e chame SQLColumns (ODBC).<br /><br /> Chame IDBSchemaRowset:: Getrowset para o conjunto de linhas de esquema DBSCHEMA_SPARSE_COLUMN_SET (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema.|  
|Determinar se uma coluna está esparsa.|Consulte a coluna SS_IS_SPARSE do conjunto de resultados SQLColumns (ODBC).<br /><br /> Consulte a coluna SS_IS_SPARSE do conjunto de linhas de esquema de DBSCHEMA_COLUMNS (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema.|  
|Determinar se uma coluna é uma **column_set**.|Consulte a coluna SS_IS_COLUMN_SET do conjunto de resultados SQLColumns. Ou então, consulte o atributo de coluna específico do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], SQL_CA_SS_IS_COLUMN_SET (ODBC).<br /><br /> Consulte a coluna SS_IS_COLUMN_SET do conjunto de linhas de esquema de DBSCHEMA_COLUMNS. Ou então, consulte *dwFlags* retornado por icolumnsinfo:: Getcolumninfo ou DBCOLUMNFLAGS no conjunto de linhas retornado por Getcolumnsrowset. Para **column_set** colunas, DBCOLUMNFLAGS_SS_ISCOLUMNSET será definido (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema.|  
|Importar e exportar colunas esparsas por BCP para uma tabela sem nenhum **column_set**.|Nenhuma alteração em comportamento de versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|Importar e exportar colunas esparsas por BCP para uma tabela com um **column_set**.|O **column_set** é importado e exportado da mesma maneira como XML; ou seja, como **varbinary (max)** se associado como tipo binário ou como **nvarchar (max)** se associados como uma **char** ou **wchar** tipo.<br /><br /> Colunas que são membros de esparso **column_set** não são exportadas como colunas distintas; elas só são exportadas no valor da **column_set**.|  
|**QUERYOUT** comportamento para BCP.|Nenhuma alteração na manipulação de colunas nomeadas explicitamente de versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.<br /><br /> Cenários que envolvem importação e exportação entre tabelas com esquemas diferentes podem exigir manipulação especial.<br /><br /> Para obter mais informações sobre BCP, consulte Suporte de BCP (cópia em massa) a colunas esparsas, mais adiante neste tópico.|  
  
## <a name="down-level-client-behavior"></a>Comportamento do cliente de versão anterior  
 Clientes de nível inferior retornarão metadados somente para colunas que não são membros de esparso **column_set** para SQLColumns e DBSCHMA_COLUMNS. As linhas do esquema OLE DB adicionais introduzidas no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client não estarão disponível, nem as modificações no SQLColumns em ODBC via SQL_SOPT_SS_NAME_SCOPE.  
  
 Clientes de nível inferior podem acessar as colunas que são membros de esparso **column_set** por nome e o **column_set** coluna poderá ser acessada como uma coluna XML para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] os clientes.  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Suporte de BCP (cópia em massa) a colunas esparsas  
 Não há nenhuma alteração para a API BCP em ODBC ou OLE DB para as colunas esparsas ou **column_set** recursos.  
  
 Se uma tabela tiver um **column_set**, as colunas esparsas não são tratadas como colunas distintas. Os valores de todas as colunas esparsas são incluídos no valor da **column_set**, que é exportado da mesma forma que uma coluna XML; ou seja, como **varbinary (max)** se associado como tipo binário ou como  **nvarchar (max)** se associados como uma **char** ou **wchar** tipo). Na importação, o **column_set** valor deve estar de acordo com o esquema do **column_set**.  
  
 Para **queryout** operações, não há nenhuma alteração na forma como são tratadas as colunas referenciadas explicitamente. **column_set** colunas têm o mesmo comportamento das colunas XML e dispersão não tem efeito sobre o tratamento de colunas esparsas nomeadas.  
  
 No entanto, se **queryout** é usado para exportar e fazer referência a colunas esparsas que são membros da coluna esparsa definido por nome, você não pode executar uma importação direta para uma tabela de estrutura semelhante. Isso ocorre porque o BCP usa metadados consistentes com um **selecione \***  operação para a importação e não pode corresponder **column_set** colunas de membro com esses metadados. Para importar **column_set** colunas de membro individualmente, você deve definir uma exibição em uma tabela que faz referência a desejado **column_set** colunas e você deve executar a operação de importação usando o modo de exibição.  
  
## <a name="see-also"></a>Consulte também  
 [Programação do SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
