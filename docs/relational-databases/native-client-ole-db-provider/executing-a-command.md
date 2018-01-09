---
title: Executar um comando | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-provider
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cc96e519125e676212e1b7e4eb8773f2b0a59513
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="executing-a-command"></a>Executando um comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Depois de estabelecida a conexão a uma fonte de dados, o consumidor chama o **idbcreatesession:: CreateSession** método para criar uma sessão. A sessão atua como um comando, conjunto de linhas ou fábrica de transação.  
  
 Para trabalhar diretamente com as tabelas individuais ou índices, o consumidor solicita a **IOpenRowset** interface. O **IOpenRowset:: OPENROWSET** método abre e retorna um conjunto de linhas que inclui todas as linhas de uma única tabela base ou índice.  
  
 Para executar um comando (como SELECT \* FROM Authors), o consumidor solicita a **IDBCreateCommand** interface. O consumidor pode executar o **idbcreatecommand:: CreateCommand** método para criar um objeto de comando e solicitar a **ICommandText** interface. O **ICommandText:: SetCommandText** método é usado para especificar o comando a ser executado.  
  
 O **Execute** comando é usado para executar o comando. O comando pode ser qualquer instrução SQL ou nome de procedimento. Nem todos os comandos geram um objeto de conjunto de resultados (conjunto de linhas). Comandos como SELECT * FROM Authors geram um conjunto de resultados.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um aplicativo provedor OLE DB do SQL Server Native Client](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
