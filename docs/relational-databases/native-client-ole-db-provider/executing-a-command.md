---
title: Executar um comando | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-provider
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3c815f3ef1ac305fdf7ec7f6aa2a29e1770b491b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="executing-a-command"></a>Executando um comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Depois de estabelecida a conexão a uma fonte de dados, o consumidor chama o **idbcreatesession:: CreateSession** método para criar uma sessão. A sessão atua como um comando, conjunto de linhas ou fábrica de transação.  
  
 Para trabalhar diretamente com as tabelas individuais ou índices, o consumidor solicita a **IOpenRowset** interface. O **IOpenRowset:: OPENROWSET** método abre e retorna um conjunto de linhas que inclui todas as linhas de uma única tabela base ou índice.  
  
 Para executar um comando (como SELECT \* FROM Authors), o consumidor solicita a **IDBCreateCommand** interface. O consumidor pode executar o **idbcreatecommand:: CreateCommand** método para criar um objeto de comando e solicitar a **ICommandText** interface. O **ICommandText:: SetCommandText** método é usado para especificar o comando a ser executado.  
  
 O **Execute** comando é usado para executar o comando. O comando pode ser qualquer instrução SQL ou nome de procedimento. Nem todos os comandos geram um objeto de conjunto de resultados (conjunto de linhas). Comandos como SELECT * FROM Authors geram um conjunto de resultados.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um aplicativo de provedor do SQL Server Native Client OLE DB](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
