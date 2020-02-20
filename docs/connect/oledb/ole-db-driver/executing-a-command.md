---
title: Executar um comando | Microsoft Docs
description: Executando um comando
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- commands [OLE DB Driver for SQL Server]
- OLE DB, executing commands
- sessions [OLE DB Driver for SQL Server]
- OLE DB extensions for XML
- OLE DB Driver for SQL Server, command execution
author: pmasl
ms.author: pelopes
ms.openlocfilehash: f13c9177a74212b849572881f114e503a9530286
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994983"
---
# <a name="executing-a-command"></a>Executando um comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Depois de estabelecida a conexão com uma fonte de dados, o consumidor chama o método **IDBCreateSession::CreateSession** para criar uma sessão. A sessão atua como um comando, conjunto de linhas ou fábrica de transação.  
  
 Para trabalhar diretamente com tabelas ou índices individuais, o consumidor solicita a interface **IOpenRowset**. O método **IOpenRowset::OpenRowset** é aberto e retorna um conjunto de linhas que inclui todas as linhas de uma única tabela ou índice base.  
  
 Para executar um comando (como SELECT \* FROM Authors), o consumidor solicita a interface **IDBCreateCommand**. O consumidor pode executar o método **IDBCreateCommand::CreateCommand** para criar um objeto de comando e solicitar a interface **ICommandText**. O método **ICommandText::SetCommandText** é usado para especificar o comando que será executado.  
  
 O comando **Execute** é usado para executar o comando. O comando pode ser qualquer instrução SQL ou nome de procedimento. Nem todos os comandos geram um objeto de conjunto de resultados (conjunto de linhas). Comandos como SELECT * FROM Authors geram um conjunto de resultados.  
  
## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativo do Driver do OLE DB para SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
