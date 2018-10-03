---
title: Conjuntos de linhas | Microsoft Docs
description: Conjuntos de linha no OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: d854a6e49428cdeef5b9c0b6899707522958d416
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736254"
---
# <a name="rowsets"></a>Conjuntos de linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Um conjunto de linhas contém colunas de dados. Os conjuntos de linhas são objetos centrais que permitem que todos os provedores de dados OLE DB exponham dados de conjuntos de resultados em formato tabular.  
  
 Depois que um consumidor cria uma sessão usando o método **IDBCreateSession::CreateSession**, ele pode usar a interface **IOpenRowset** ou **IDBCreateCommand** na sessão para criar um conjunto de linhas. O Driver do OLE DB para SQL Server dá suporte a essas duas interfaces. Esses dois métodos são descritos aqui.  
  
-   Criar um conjunto de linhas chamando o método **IOpenRowset::OpenRowset**.  
  
     Isto equivale a criar um conjunto de linhas sobre uma única tabela. Este método abre e retorna um conjunto de linhas que inclui todas as linhas de uma única tabela base. Um dos argumentos para **OpenRowset** é uma ID de tabela que identifica a tabela com base na qual criar o conjunto de linhas.  
  
-   Criar um objeto de comando chamando o método **IDBCreateCommand::CreateCommand**.  
  
     O objeto de comando executa comandos aos quais o provedor dá suporte. Com o OLE DB Driver for SQL Server, o consumidor pode especificar qualquer instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)], como a instrução SELECT, ou uma chamada a um procedimento armazenado. As etapas para a criação de um conjunto de linhas usando um objeto de comando são:  
  
    1.  O consumidor chama o método **IDBCreateCommand::CreateCommand** na sessão para obter um objeto de comando que solicita a interface **ICommandText** no objeto de comando. Essa interface **ICommandText** define e recupera o texto de comando real. O consumidor preenche o comando de texto chamando o método **ICommandText::SetCommandText**.  
  
    2.  O usuário chama o método **ICommand::Execute** no comando. O objeto do conjunto de linhas criado quando o comando é executado contém o conjunto de resultados do comando.  
  
 O consumidor pode usar a interface **ICommandProperties** para obter ou definir as propriedades do conjunto de linhas retornado pelo comando executado pelas interfaces **ICommand::Execute**. As propriedades solicitadas com mais frequência são as interfaces às quais o conjunto de linhas deve dar suporte. Além das interfaces, o consumidor pode solicitar propriedades que modificam o comportamento do conjunto de linhas ou da interface.  
  
 Os consumidores liberam conjuntos de linhas com o método **IRowset::Release**. A liberação de um conjunto de linhas libera todos os indicadores de linha mantidos pelo consumidor nesse conjunto de linhas. A liberação de um conjunto de linhas não libera os acessadores. Se você tiver uma interface **IAccessor**, ela ainda deverá ser liberada.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criando um conjunto de linhas com IOpenRowset](../../oledb/ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [Criando conjuntos de linhas com ICommand::Execute](../../oledb/ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [Propriedades e comportamentos do conjunto de linhas](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [Conjuntos de linha e cursores do SQL Server](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [Buscando linhas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
-   [Buscando uma única linha com IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [Indicadores](../../oledb/ole-db-rowsets/bookmarks.md)  
  
-   [Atualizando dados em conjuntos de linhas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
