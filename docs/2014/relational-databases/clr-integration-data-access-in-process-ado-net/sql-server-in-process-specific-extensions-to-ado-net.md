---
title: Extensões específicas do SQL Server no processo para o ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [CLR integration]
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], in-process extensions
- in-process data access providers [CLR integration]
- extensions [CLR integration]
ms.assetid: 781b812e-eb14-472a-85fa-aa4cdb929bee
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b72ecf75f7c696e21fc14e73b42d1d192320679e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011410"
---
# <a name="sql-server-in-process-specific-extensions-to-adonet"></a>Extensões específicas em processo do SQL Server para o ADO.NET
  Há quatro extensões funcionais principais para o ADO.NET que se destinam especificamente ao uso em processo. Os tópicos a seguir abrangem essas extensões detalhadamente.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Objeto SqlContext](sqlcontext-object.md)  
 Esta classe fornece acesso às outras extensões abstraindo o contexto de um chamador de uma rotina do SQL Server que executa código gerenciado em processo.  
  
 [Objeto SqlPipe](sqlpipe-object.md)  
 Esta classe contém rotinas para enviar mensagens e resultados tabulares ao cliente.  
  
 [Objeto SqlTriggerContext](sqltriggercontext-object.md)  
 Esta classe fornece informações sobre o contexto no qual um gatilho é executado.  
  
 [Objeto SqlDataRecord](sqldatarecord-object.md)  
 A classe SqlDataRecord representa uma única linha de dados, juntamente com seus metadados relacionados, e permite que procedimentos armazenados retornem conjuntos de resultados personalizados ao cliente.  
  
  