---
title: Rowsets | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
ms.assetid: 5e7b3cbe-3670-4e18-8172-2226e0b6b142
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe964e8e0cadaee2118540714f6e8a9c43763748
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="rowsets"></a>Conjuntos de linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Um conjunto de linhas contém colunas de dados. Os conjuntos de linhas são objetos centrais que permitem que todos os provedores de dados OLE DB exponham dados de conjuntos de resultados em formato tabular.  
  
 Depois que um consumidor cria uma sessão usando o **idbcreatesession:: CreateSession** método, o consumidor pode usar o **IOpenRowset** ou **IDBCreateCommand** interface na sessão para criar um conjunto de linhas. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client oferece suporte a duas interfaces. Esses dois métodos são descritos aqui.  
  
-   Criar um conjunto de linhas chamando o **IOpenRowset:: OPENROWSET** método.  
  
     Isto equivale a criar um conjunto de linhas sobre uma única tabela. Este método abre e retorna um conjunto de linhas que inclui todas as linhas de uma única tabela base. Um dos argumentos para **OpenRowset** é uma ID de tabela que identifica a tabela da qual criar o conjunto de linhas.  
  
-   Crie um objeto de comando chamando o **idbcreatecommand:: CreateCommand** método.  
  
     O objeto de comando executa comandos aos quais o provedor dá suporte. Com o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o consumidor pode especificar qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)], como a instrução SELECT, ou uma chamada para um procedimento armazenado. As etapas para a criação de um conjunto de linhas usando um objeto de comando são:  
  
    1.  O consumidor chama o **idbcreatecommand:: CreateCommand** método na sessão para obter um objeto de comando solicitando o **ICommandText** interface no objeto de comando. Isso **ICommandText** interface define e recupera o texto do comando real. O consumidor preenche o comando de texto chamando o **ICommandText:: SetCommandText** método.  
  
    2.  O usuário chama o **ICommand:: execute** método no comando. O objeto do conjunto de linhas criado quando o comando é executado contém o conjunto de resultados do comando.  
  
 O consumidor pode usar o **ICommandProperties** interface para obter ou definir as propriedades do conjunto de linhas retornado pelo comando executado pelo **ICommand:: execute** interfaces. As propriedades solicitadas com mais frequência são as interfaces às quais o conjunto de linhas deve dar suporte. Além das interfaces, o consumidor pode solicitar propriedades que modificam o comportamento do conjunto de linhas ou da interface.  
  
 Os consumidores liberam conjuntos de linhas com o **IRowset:: Release** método. A liberação de um conjunto de linhas libera todos os indicadores de linha mantidos pelo consumidor nesse conjunto de linhas. A liberação de um conjunto de linhas não libera os acessadores. Se você tiver um **IAccessor** interface, ele ainda tem que ser liberado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criando um conjunto de linhas com IOpenRowset](../../relational-databases/native-client-ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [Criando conjuntos de linhas com ICommand:: execute](../../relational-databases/native-client-ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [Comportamentos e propriedades de conjunto de linhas](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [Conjuntos de linhas e cursores do SQL Server](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [Buscando linhas](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [Buscando uma única linha com IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [Indicadores](../../relational-databases/native-client-ole-db-rowsets/bookmarks.md)  
  
-   [Atualizando dados em conjuntos de linhas](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
