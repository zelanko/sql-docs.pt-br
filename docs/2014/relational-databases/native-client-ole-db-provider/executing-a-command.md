---
title: Executar um comando | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2d9c0f935bf4d3cd903346281080a8b08384c1e4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116126"
---
# <a name="executing-a-command"></a>Executando um comando
  Depois de estabelecida a conexão a uma fonte de dados, o consumidor chama o **idbcreatesession:: CreateSession** método para criar uma sessão. A sessão atua como um comando, conjunto de linhas ou fábrica de transação.  
  
 Para trabalhar diretamente com tabelas ou índices individuais, o consumidor solicita a interface `IOpenRowset`. O método `IOpenRowset::OpenRowset` se abre e retorna um conjunto de linhas que inclui todas as linhas de uma única tabela ou índice base.  
  
 Para executar um comando (como SELECT \* FROM Authors), o consumidor solicita a `IDBCreateCommand` interface. O consumidor pode executar o método `IDBCreateCommand::CreateCommand` para criar um objeto de comando e solicitar a interface `ICommandText`. O método `ICommandText::SetCommandText` é usado para especificar o comando que será executado.  
  
 O comando `Execute` é usado para executar o comando. O comando pode ser qualquer instrução SQL ou nome de procedimento. Nem todos os comandos geram um objeto de conjunto de resultados (conjunto de linhas). Comandos como SELECT * FROM Authors geram um conjunto de resultados.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um aplicativo provedor OLE DB do SQL Server Native Client](creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  