---
title: Suporte a colunas esparsas no SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21b79a06acd838278073dee58026269f63b0da04
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75231706"
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>Suporte a colunas esparsas no SQL Server Native Client
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client suporta colunas esparsas. Para obter mais informações sobre colunas esparsas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], confira [Usar colunas esparsas](../../tables/use-sparse-columns.md) e [Usar conjuntos de colunas](../../tables/use-column-sets.md).  
  
 Para obter mais informações sobre o suporte a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] colunas esparsas no Native Client, consulte [suporte a colunas esparsas &#40;&#41;ODBC](../odbc/sparse-columns-support-odbc.md) e [colunas esparsas dão suporte a &#40;OLE DB&#41;](../ole-db/sparse-columns-support-ole-db.md).  
  
 Para obter informações sobre aplicativos de exemplo que demonstram esse recurso, confira [Amostras de programação do SQL Server Data](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>Cenários de usuário para colunas esparsas e o SQL Server Native Client  
 A tabela a seguir resume os cenários comuns para usuários do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client com colunas esparsas:  
  
|Cenário|Comportamento|  
|--------------|--------------|  
|**select \* from table** ou IOpenRowset::OpenRowset.|Retorna todas as colunas que não são membros do `column_set` esparso, além de uma coluna XML que contém os valores de todas as colunas não nulas membros do `column_set` esparso.|  
|Referenciar uma coluna por nome.|A coluna pode ser referenciada independentemente de seu status de coluna esparsa ou associação do `column_set`.|  
|Acessar colunas de membro do `column_set` através de uma coluna de XML computada.|As colunas que são membros do `column_set` esparso podem ser acessadas selecionando o `column_set` por nome e podem ter valores inseridos e atualizados atualizando o XML na coluna `column_set`.<br /><br /> O valor precisa estar de acordo com o esquema para colunas `column_set`.|  
|Recuperar metadados de todas as colunas em uma tabela por meio de SQLColumns com um padrão de pesquisa de coluna de nulo ou '% ' (ODBC); ou por meio do conjunto de linhas de esquema DBSCHEMA_COLUMNS sem restrição de coluna (OLE DB).|Retorna uma linha para todas as colunas que não são membros de um `column_set`. Se a tabela tiver um `column_set` esparso, uma linha será retornada para ela.<br /><br /> Observe que essa ação não retorna metadados para colunas que são membros de um `column_set`.|  
|Recuperar metadados para todas as colunas, independentemente de dispersão ou associação em um `column_set`. Essa ação pode retornar um número muito grande de linhas.|Defina o campo de descritor SQL_SOPT_SS_NAME_SCOPE como SQL_SS_NAME_SCOPE_EXTENDED e chamar [SQLColumns](../../native-client-odbc-api/sqlcolumns.md) (ODBC).<br /><br /> Chame IDBSchemaRowset:: GetRowset para o conjunto de linhas de esquema de DBSCHEMA_COLUMNS_EXTENDED (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema diretamente.|  
|Recuperar metadados somente para colunas que são membros de um `column_set`. Essa ação pode retornar um número muito grande de linhas.|Defina o campo de descritor SQL_SOPT_SS_NAME_SCOPE como SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET e chamar SQLColumns (ODBC).<br /><br /> Chame IDBSchemaRowset:: GetRowset para o conjunto de linhas de esquema de DBSCHEMA_SPARSE_COLUMN_SET (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema.|  
|Determinar se uma coluna está esparsa.|Consulte a coluna SS_IS_SPARSE do conjunto de resultados SQLColumns (ODBC).<br /><br /> Consulte a coluna SS_IS_SPARSE do conjunto de linhas de esquema de DBSCHEMA_COLUMNS (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema.|  
|Determinar se uma coluna é um `column_set`.|Consulte a coluna SS_IS_COLUMN_SET do conjunto de resultados SQLColumns. Ou então, consulte o atributo de coluna específico do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], SQL_CA_SS_IS_COLUMN_SET (ODBC).<br /><br /> Consulte a coluna SS_IS_COLUMN_SET do conjunto de linhas de esquema de DBSCHEMA_COLUMNS. Ou então, confira *dwFlags* retornado por IColumnsinfo::GetColumnInfo ou DBCOLUMNFLAGS no conjunto de linhas retornado por IColumnsRowset::GetColumnsRowset. Para colunas `column_set`, DBCOLUMNFLAGS_SS_ISCOLUMNSET será definido (OLE DB).<br /><br /> Esse cenário não é possível com um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client de uma versão anterior ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Entretanto, esse aplicativo poderia consultar exibições de sistema.|  
|Importar e exportar colunas esparsas por BCP para uma tabela sem `column_set`.|Nenhuma alteração em comportamento de versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|Importar e exportar colunas esparsas por BCP para uma tabela com `column_set`.|O `column_set` é importado e exportado da mesma maneira que o XML; ou seja, como `varbinary(max)` se fosse associado como um tipo binário, ou `nvarchar(max)` como se fosse associado `char` como um tipo ou **WCHAR** .<br /><br /> Colunas que são membros do `column_set` esparso não são exportadas como colunas distintas; elas só são exportadas no valor do `column_set`.|  
|Comportamento de `queryout` para BCP.|Nenhuma alteração na manipulação de colunas nomeadas explicitamente de versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.<br /><br /> Cenários que envolvem importação e exportação entre tabelas com esquemas diferentes podem exigir manipulação especial.<br /><br /> Para obter mais informações sobre BCP, consulte Suporte de BCP (cópia em massa) a colunas esparsas, mais adiante neste tópico.|  
  
## <a name="down-level-client-behavior"></a>Comportamento do cliente de versão anterior  
 Os clientes de nível inferior retornarão metadados somente para colunas que não sejam membros do esparso `column_set` para SQLColumns e DBSCHMA_COLUMNS. Os conjuntos de linhas de esquema OLE DB adicionais [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] introduzidos no Native Client não estarão disponíveis, nem as modificações em SQLColumns no ODBC via SQL_SOPT_SS_NAME_SCOPE.  
  
 Os clientes de nível inferior podem acessar as colunas que são membros do `column_set` esparso por nome, e a coluna `column_set` poderá ser acessada como uma coluna XML por clientes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Suporte de BCP (cópia em massa) a colunas esparsas  
 Não há nenhuma alteração à API de BCP em ODBC ou OLE DB para as colunas esparsas ou os recursos de `column_set`.  
  
 Se uma tabela tiver um `column_set`, as colunas esparsas não serão tratadas como colunas distintas. Os valores de todas as colunas esparsas são incluídos no valor de `column_set`, que é exportado da mesma maneira que uma coluna XML; ou seja, como `varbinary(max)` se fosse associado como um tipo binário, ou `nvarchar(max)` como se fosse associado `char` como um tipo ou **WCHAR** ). Na importação, o valor de `column_set` deve estar de acordo com o esquema do `column_set`.  
  
 Para operações de `queryout`, não há alterações na maneira como são tratadas as colunas referenciadas explicitamente. As colunas de `column_set` têm o mesmo comportamento das colunas XML e a dispersão não tem efeito sobre o tratamento de colunas esparsas nomeadas.  
  
 Entretanto, se `queryout` for usado para exportação e você referenciar colunas esparsas que são membros do conjunto de colunas esparsas por nome, não será possível executar uma importação direta para uma tabela de estrutura semelhante. Isso ocorre porque o bcp usa metadados consistentes com uma operação **Select \* ** para a importação e não pode `column_set` corresponder colunas de membros a esses metadados. Para importar as colunas de membro de `column_set` individualmente, você precisa definir uma exibição na tabela que referencia as colunas de `column_set` desejadas, além de executar a operação de importação usando a exibição.  
  
## <a name="see-also"></a>Consulte Também  
 [Programação do SQL Server Native Client](../sql-server-native-client-programming.md)  
  
