---
title: Executar um comando | Microsoft Docs
description: Executar um comando
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- commands [OLE DB Driver for SQL Server]
- OLE DB, executing commands
- sessions [OLE DB Driver for SQL Server]
- OLE DB extensions for XML
- OLE DB Driver for SQL Server, command execution
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 4183471cfb2cbf73cbbfe25b3fe561574de6b3ec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="executing-a-command"></a>Executando um comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Depois de estabelecida a conexão a uma fonte de dados, o consumidor chama o **idbcreatesession:: CreateSession** método para criar uma sessão. A sessão atua como um comando, conjunto de linhas ou fábrica de transação.  
  
 Para trabalhar diretamente com as tabelas individuais ou índices, o consumidor solicita a **IOpenRowset** interface. O **IOpenRowset:: OPENROWSET** método abre e retorna um conjunto de linhas que inclui todas as linhas de uma única tabela base ou índice.  
  
 Para executar um comando (como SELECT \* FROM Authors), o consumidor solicita a **IDBCreateCommand** interface. O consumidor pode executar o **idbcreatecommand:: CreateCommand** método para criar um objeto de comando e solicitar a **ICommandText** interface. O **ICommandText:: SetCommandText** método é usado para especificar o comando a ser executado.  
  
 O **Execute** comando é usado para executar o comando. O comando pode ser qualquer instrução SQL ou nome de procedimento. Nem todos os comandos geram um objeto de conjunto de resultados (conjunto de linhas). Comandos como SELECT * FROM Authors geram um conjunto de resultados.  
  
## <a name="see-also"></a>Consulte também  
 [Criação de aplicativo do Driver do OLE DB para SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
