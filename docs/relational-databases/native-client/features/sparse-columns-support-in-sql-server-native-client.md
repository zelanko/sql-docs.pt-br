---
title: Suporte a colunas esparsas no Cliente Nativo SQL
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 958424a4710b76e7e09ae15e10b612630f09eee3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303766"
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>Suporte a colunas esparsas no SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client suporta colunas esparsas. Para obter mais informações sobre colunas esparsas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], confira [Usar colunas esparsas](../../../relational-databases/tables/use-sparse-columns.md) e [Usar conjuntos de colunas](../../../relational-databases/tables/use-column-sets.md).  
  
 Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o suporte a colunas esparsas no Cliente Nativo, consulte [Colunas esparsas Suporte &#40;Suporte de&#41;](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md) e [Colunas Esparsas &#40;o LE DB&#41;](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md).  
  
 Para obter informações sobre aplicativos de exemplo que demonstram esse recurso, confira [Amostras de programação do SQL Server Data](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>Cenários de usuário para colunas esparsas e o SQL Server Native Client  
 A tabela a seguir resume os cenários comuns para usuários do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client com colunas esparsas:  
  
|Cenário|Comportamento|  
|--------------|--------------|  
|**select \* from table** ou IOpenRowset::OpenRowset.|Retorna todas as colunas que não são membros do **column_set** esparso, além de uma coluna XML que contém os valores de todas as colunas não nulas que são membros do **column_set** esparso.|  
|Referenciar uma coluna por nome.|A coluna pode ser referenciada, independentemente de seu status de coluna esparsa ou associação ao **column_set**.|  
|Acessar colunas de membro do **column_set** por meio de uma coluna XML computada.|As colunas que são membros do **column_set** esparso podem ser acessadas selecionando o **column_set** por nome e podem ter valores inseridos e atualizados atualizando o XML na coluna **column_set**.<br /><br /> O valor precisa estar em conformidade com o esquema para colunas **column_set**.|  
|Recuperar metadados para todas as colunas em uma tabela através de Colunas SQL com um padrão de pesquisa de coluna de NULL ou '%' (ODBC); ou através do esquema de DBSCHEMA_COLUMNS conjunto de linhas sem restrição de coluna (OLE DB).|Retorna uma linha para todas as colunas que não são membros de um **column_set**. Se a tabela tiver um **column_set** esparso, uma linha será retornada para ela.<br /><br /> Observe que isso não retorna os metadados para colunas que são membros de um **column_set**.|  
|Recuperar metadados para todas as colunas, independentemente da dispersão ou da associação em um **column_set**. Essa ação pode retornar um número muito grande de linhas.|Defina o campo descritor SQL_SOPT_SS_NAME_SCOPE para SQL_SS_NAME_SCOPE_EXTENDED e ligue para [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) (ODBC).<br /><br /> Ligue para o IDBSchemaRowset::GetRowset para o conjunto de linhas de esquema DBSCHEMA_COLUMNS_EXTENDED (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema diretamente.|  
|Recuperar metadados somente para colunas que são membros de um **column_set**. Essa ação pode retornar um número muito grande de linhas.|Defina o campo descritor SQL_SOPT_SS_NAME_SCOPE para SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET e ligue para SQLColumns (ODBC).<br /><br /> Ligue para o IDBSchemaRowset::GetRowset para o conjunto de linhas de esquema DBSCHEMA_SPARSE_COLUMN_SET (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema.|  
|Determinar se uma coluna está esparsa.|Consulte a coluna SS_IS_SPARSE do conjunto de resultados SQLColumns (ODBC).<br /><br /> Consulte a coluna SS_IS_SPARSE do conjunto de linhas de esquema de DBSCHEMA_COLUMNS (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema.|  
|Determinar se uma coluna é um **column_set**.|Consulte a coluna SS_IS_COLUMN_SET do conjunto de resultados SQLColumns. Ou então, consulte o atributo de coluna específico do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], SQL_CA_SS_IS_COLUMN_SET (ODBC).<br /><br /> Consulte a coluna SS_IS_COLUMN_SET do conjunto de linhas de esquema de DBSCHEMA_COLUMNS. Ou então, confira *dwFlags* retornado por IColumnsinfo::GetColumnInfo ou DBCOLUMNFLAGS no conjunto de linhas retornado por IColumnsRowset::GetColumnsRowset. Para **column_set** colunas, serão definidos DBCOLUMNFLAGS_SS_ISCOLUMNSET (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema.|  
|Importar e exportar colunas esparsas por BCP para uma tabela sem **column_set**.|Nenhuma alteração em comportamento de versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|Importar e exportar colunas esparsas por BCP para uma tabela com um **column_set**.|Se **column_set** estiver associado como um tipo binário, ele será importado e exportado da mesma maneira que o XML; ou seja, como **varbinary(max)**. Se estiver associado como um tipo **char** ou **wchar**, será importado como **nvarchar (max)**.<br /><br /> As colunas que são membros do **column_set** esparso não são exportadas como colunas distintas; elas só são exportadas no valor do **column_set**.|  
|Comportamento de **queryout** para BCP.|Nenhuma alteração na manipulação de colunas nomeadas explicitamente de versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.<br /><br /> Cenários que envolvem importação e exportação entre tabelas com esquemas diferentes podem exigir manipulação especial.<br /><br /> Para obter mais informações sobre BCP, consulte Suporte de BCP (cópia em massa) a colunas esparsas, mais adiante neste tópico.|  
  
## <a name="down-level-client-behavior"></a>Comportamento do cliente de versão anterior  
 Os clientes de nível inferior só retornarão metadados para colunas que não são membros do **column_set** esparso para SQLColumns e DBSCHMA_COLUMNS. Os conjuntos de linhas de esquema [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] OLE DB adicionais introduzidos no Cliente Nativo não estarão disponíveis, nem as modificações em Colunas SQL no ODBC via SQL_SOPT_SS_NAME_SCOPE.  
  
 Os clientes de nível inferior podem acessar as colunas que são membros do **column_set** esparso por nome, e a coluna **column_set** ficará acessível como uma coluna XML aos clientes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Suporte de BCP (cópia em massa) a colunas esparsas  
 Não há alterações na API BCP em ODBC ou OLE DB para as colunas esparsas ou **column_set** características.  
  
 Se uma tabela tiver um **column_set**, as colunas esparsas não serão tratadas como colunas distintas. Os valores de todas as colunas esparsas serão incluídos no valor do **column_set**, que é exportado da mesma maneira que uma coluna XML, ou seja, como **varbinary(max)**, se estiver associado como tipo binário ou como **nvarchar(max)** se estiver associado como tipo **char** or **wchar**). Na importação, o valor de **column_set** precisa estar em conformidade com o esquema do **column_set**.  
  
 Para operações **queryout**, não há alterações na maneira como são tratadas as colunas referenciadas explicitamente. As colunas de **column_set** têm o mesmo comportamento das colunas XML e a dispersão não tem nenhum efeito sobre o tratamento de colunas esparsas nomeadas.  
  
 Entretanto, se **queryout** for usado para exportação e você referenciar colunas esparsas que são membros do conjunto de colunas esparsas por nome, você não poderá executar uma importação direta para uma tabela de estrutura semelhante. Isso porque o BCP usa metadados consistentes com uma operação **&#42;selecionada** para a importação e não consegue corresponder **column_set** colunas de membros com esses metadados. Para importar as colunas de membro de **column_set** individualmente, você precisa definir uma exibição na tabela que referencia as colunas do **column_set** desejadas, além de executar a operação de importação usando a exibição.  
  
## <a name="see-also"></a>Consulte Também  
 [Programação do SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
