---
title: MSSQLSERVER_17067 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17067 (Database Engine error)
ms.assetid: 32c1f0e8-db70-4836-95b2-8833be9e0ad1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2bd9a9d7e2c8b9d03c3fdaefd1364102cbd7ba56
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553691"
---
# <a name="mssqlserver_17067"></a>MSSQLSERVER_17067
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|17067|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLASSERT_MESG|  
|Texto da mensagem|Asserção do SQL Server: Arquivo: \<%s>, linha = %d %s. Talvez esse erro esteja relacionado à temporização. Se o erro persistir após a repetição da instrução, use DBCC CHECKDB para verificar a integridade estrutural do banco de dados ou reinicie o servidor para assegurar que as estruturas de dados na memória não estejam corrompidas.|  
  
## <a name="explanation"></a>Explicação  
 Talvez o erro seja causado por erros transitórios relacionados à temporização ou por dados corrompidos na memória ou no disco.  
  
## <a name="user-action"></a>Ação do usuário  
 Exiba novamente a instrução que causou o disparo da exceção. Se o erro foi causado por um evento relacionado à temporização, talvez ele não ocorra novamente. Se o problema persistir, execute DBCC CHECKDB para verificar se há dados corrompidos no disco. Reinicie o servidor para garantir que as estruturas de dados na memória não estão corrompidas.  
  
## <a name="see-also"></a>Consulte Também  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
