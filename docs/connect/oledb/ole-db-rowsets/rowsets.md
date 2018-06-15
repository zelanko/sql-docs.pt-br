---
title: Conjuntos de linhas | Microsoft Docs
description: Conjuntos de linhas no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 5e03aa5a887f25e9909ff2c755cfbfa598166475
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35306695"
---
# <a name="rowsets"></a>Conjuntos de linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Um conjunto de linhas contém colunas de dados. Os conjuntos de linhas são objetos centrais que permitem que todos os provedores de dados OLE DB exponham dados de conjuntos de resultados em formato tabular.  
  
 Depois que um consumidor cria uma sessão usando o **idbcreatesession:: CreateSession** método, o consumidor pode usar o **IOpenRowset** ou **IDBCreateCommand** interface na sessão para criar um conjunto de linhas. O Driver OLE DB para SQL Server dá suporte a duas interfaces. Esses dois métodos são descritos aqui.  
  
-   Criar um conjunto de linhas chamando o **IOpenRowset:: OPENROWSET** método.  
  
     Isto equivale a criar um conjunto de linhas sobre uma única tabela. Este método abre e retorna um conjunto de linhas que inclui todas as linhas de uma única tabela base. Um dos argumentos para **OpenRowset** é uma ID de tabela que identifica a tabela da qual criar o conjunto de linhas.  
  
-   Crie um objeto de comando chamando o **idbcreatecommand:: CreateCommand** método.  
  
     O objeto de comando executa comandos aos quais o provedor dá suporte. Com o OLE DB para SQL Server, o consumidor pode especificar qualquer [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução, como uma instrução SELECT ou uma chamada para um procedimento armazenado. As etapas para a criação de um conjunto de linhas usando um objeto de comando são:  
  
    1.  O consumidor chama o **idbcreatecommand:: CreateCommand** método na sessão para obter um objeto de comando solicitando o **ICommandText** interface no objeto de comando. Isso **ICommandText** interface define e recupera o texto do comando real. O consumidor preenche o comando de texto chamando o **ICommandText:: SetCommandText** método.  
  
    2.  O usuário chama o **ICommand:: execute** método no comando. O objeto do conjunto de linhas criado quando o comando é executado contém o conjunto de resultados do comando.  
  
 O consumidor pode usar o **ICommandProperties** interface para obter ou definir as propriedades do conjunto de linhas retornado pelo comando executado pelo **ICommand:: execute** interfaces. As propriedades solicitadas com mais frequência são as interfaces às quais o conjunto de linhas deve dar suporte. Além das interfaces, o consumidor pode solicitar propriedades que modificam o comportamento do conjunto de linhas ou da interface.  
  
 Os consumidores liberam conjuntos de linhas com o **IRowset:: Release** método. A liberação de um conjunto de linhas libera todos os indicadores de linha mantidos pelo consumidor nesse conjunto de linhas. A liberação de um conjunto de linhas não libera os acessadores. Se você tiver um **IAccessor** interface, ele ainda tem que ser liberado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criando um conjunto de linhas com IOpenRowset](../../oledb/ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [Criando conjuntos de linhas com ICommand::Execute](../../oledb/ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [Propriedades e comportamentos do conjunto de linhas](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [Conjuntos de linha e cursores do SQL Server](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [Buscando linhas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
-   [Buscando uma única linha com IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [Indicadores](../../oledb/ole-db-rowsets/bookmarks.md)  
  
-   [Atualizando dados em conjuntos de linhas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>Consulte também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
