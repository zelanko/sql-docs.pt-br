---
title: MSSQLSERVER_17067 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 17067 (Database Engine error)
ms.assetid: 32c1f0e8-db70-4836-95b2-8833be9e0ad1
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ff70b894892a49f9286bd041fabd5f8a49ad070
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425185"
---
# <a name="mssqlserver17067"></a>MSSQLSERVER_17067
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17067|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLASSERT_MESG|  
|Texto da mensagem|Declaração do SQL Server: arquivo: \<%s>, linha = %d %s. Talvez esse erro esteja relacionado à temporização. Se o erro persistir após a repetição da instrução, use DBCC CHECKDB para verificar a integridade estrutural do banco de dados ou reinicie o servidor para assegurar que as estruturas de dados na memória não estejam corrompidas.|  
  
## <a name="explanation"></a>Explicação  
 Talvez o erro seja causado por erros transitórios relacionados à temporização ou por dados corrompidos na memória ou no disco.  
  
## <a name="user-action"></a>Ação do usuário  
 Exiba novamente a instrução que causou o disparo da exceção. Se o erro foi causado por um evento relacionado à temporização, talvez ele não ocorra novamente. Se o problema persistir, execute DBCC CHECKDB para verificar se há dados corrompidos no disco. Reinicie o servidor para garantir que as estruturas de dados na memória não estão corrompidas.  
  
## <a name="see-also"></a>Consulte também  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
