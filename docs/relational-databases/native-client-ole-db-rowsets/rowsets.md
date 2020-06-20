---
title: Conjuntos de linhas | Microsoft Docs
description: Habilite todos os provedores de dados para expor dados de conjunto de resultados em formato de tabela. Em OLE DB, use o recurso conjunto de linhas, um conjunto de linhas que contém colunas de dados.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
ms.assetid: 5e7b3cbe-3670-4e18-8172-2226e0b6b142
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 18ebbe69102fae5042204c5e5d44024a4ff9f01d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84950036"
---
# <a name="rowsets"></a>Conjuntos de linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Um conjunto de linhas contém colunas de dados. Os conjuntos de linhas são objetos centrais que permitem que todos os provedores de dados OLE DB exponham dados de conjuntos de resultados em formato tabular.  
  
 Depois que um consumidor cria uma sessão usando o método **IDBCreateSession::CreateSession**, ele pode usar a interface **IOpenRowset** ou **IDBCreateCommand** na sessão para criar um conjunto de linhas. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte a essas duas interfaces. Esses dois métodos são descritos aqui.  
  
-   Criar um conjunto de linhas chamando o método **IOpenRowset::OpenRowset**.  
  
     Isto equivale a criar um conjunto de linhas sobre uma única tabela. Este método abre e retorna um conjunto de linhas que inclui todas as linhas de uma única tabela base. Um dos argumentos para **OpenRowset** é uma ID de tabela que identifica a tabela com base na qual criar o conjunto de linhas.  
  
-   Criar um objeto de comando chamando o método **IDBCreateCommand::CreateCommand**.  
  
     O objeto de comando executa comandos aos quais o provedor dá suporte. Com o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o consumidor pode especificar qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)], como a instrução SELECT, ou uma chamada para um procedimento armazenado. As etapas para a criação de um conjunto de linhas usando um objeto de comando são:  
  
    1.  O consumidor chama o método **IDBCreateCommand::CreateCommand** na sessão para obter um objeto de comando que solicita a interface **ICommandText** no objeto de comando. Essa interface **ICommandText** define e recupera o texto de comando real. O consumidor preenche o comando de texto chamando o método **ICommandText::SetCommandText**.  
  
    2.  O usuário chama o método **ICommand::Execute** no comando. O objeto do conjunto de linhas criado quando o comando é executado contém o conjunto de resultados do comando.  
  
 O consumidor pode usar a interface **ICommandProperties** para obter ou definir as propriedades do conjunto de linhas retornado pelo comando executado pelas interfaces **ICommand::Execute**. As propriedades solicitadas com mais frequência são as interfaces às quais o conjunto de linhas deve dar suporte. Além das interfaces, o consumidor pode solicitar propriedades que modificam o comportamento do conjunto de linhas ou da interface.  
  
 Os consumidores liberam conjuntos de linhas com o método **IRowset::Release**. A liberação de um conjunto de linhas libera todos os indicadores de linha mantidos pelo consumidor nesse conjunto de linhas. A liberação de um conjunto de linhas não libera os acessadores. Se você tiver uma interface **IAccessor**, ela ainda deverá ser liberada.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criando um conjunto de linhas com IOpenRowset](../../relational-databases/native-client-ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [Criando conjuntos de linhas com ICommand::Execute](../../relational-databases/native-client-ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [Propriedades e comportamentos do conjunto de linhas](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [Conjuntos de linha e cursores do SQL Server](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [Buscando linhas](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [Buscando uma única linha com IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [Indicadores](../../relational-databases/native-client-ole-db-rowsets/bookmarks.md)  
  
-   [Atualizando dados em conjuntos de linhas](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
