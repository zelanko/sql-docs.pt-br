---
title: MSSQLSERVER_1793 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 808db1d0-acc1-41d0-9287-8a5455001a02
caps.latest.revision: 6
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d36a4c1235b8b6b9e25a5fd635a37fd6052ae524
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007506"
---
# <a name="mssqlserver1793"></a>MSSQLSERVER_1793
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1793|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|FILESTREAM_BASEDATA_NEED_SAME_PARTITION|  
|Texto da mensagem|Não é possível remover o índice '%.*ls', pois um esquema de partição não está especificado para os dados de FILESTREAM.|  
  
## <a name="explanation"></a>Explicação  
 Essa mensagem ocorre quando você tenta remover um índice clusterizado de uma tabela que contém dados FILESTREAM e especifica uma cláusula **MOVE TO** para os dados base, mas não especifica uma cláusula **FILESTREAM_ON** para os dados FILESTREAM.  
  
## <a name="user-action"></a>Ação do usuário  
 Ao remover um índice clusterizado em uma tabela que contém dados FILESTREAM, use um das seguintes opções:  
  
-   Especifique uma cláusula **MOVE TO** para os dados base e uma cláusula **FILESTREAM_ON** para os dados FILESTREAM.  
  
-   Não especifique uma cláusula **MOVE TO** para os dados base nem uma cláusula **FILESTREAM_ON** para os dados FILESTREAM.  
  
 O exemplo a seguir falha porque um esquema de partição foi especificado para os dados básicos, mas não foi especificado para os dados FILESTREAM.  
  
```tsql  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY] )  
GO  
```  
  
 O exemplo a seguir é bem-sucedido, porque uma cláusula **MOVE TO** para os dados base e uma cláusula **FILESTREAM_ON** para os dados FILESTREAM são especificadas.  
  
```tsql  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY], filestream_on 'default' )  
GO  
```  
  
 O exemplo a seguir também é bem-sucedido, porque uma cláusula **MOVE TO** para os dados base e uma cláusula **FILESTREAM_ON** para os dados FILESTREAM não são especificadas.  
  
```tsql  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF )  
GO  
```  
  
  