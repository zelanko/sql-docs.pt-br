---
title: Extensões específicas do SQL Server em processo para o ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data access [CLR integration]
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], in-process extensions
- in-process data access providers [CLR integration]
- extensions [CLR integration]
ms.assetid: 781b812e-eb14-472a-85fa-aa4cdb929bee
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 98781a7258a4fa70f9f8c70c37140445af5bcb76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874710"
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
  
  
