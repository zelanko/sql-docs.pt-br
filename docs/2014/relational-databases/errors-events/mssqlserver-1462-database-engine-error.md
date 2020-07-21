---
title: MSSQLSERVER_1462 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dbd397c80e2324d28a853ddf538cf592901a4a20
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553801"
---
# <a name="mssqlserver_1462"></a>MSSQLSERVER_1462
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|1462|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_DISABLED_DUE_TO_FAILED_REDO|  
|Texto da mensagem|O espelhamento de banco de dados foi desabilitado devido a uma falha na operação refazer. Não é possível retomar.|  
  
## <a name="explanation"></a>Explicação  
 Houve falha no espelhamento de banco de dados ao refazer um registro de log no espelho.  
  
### <a name="possible-causes"></a>Possíveis causas  
 A causa mais provável é que uma operação de adicionar arquivo tenha sido concluída no banco de dados principal, mas tenha apresentado falha no banco de dados espelho porque os nomes de arquivo ou as estruturas de diretório diferiam no servidor principal e no servidor espelho.  
  
## <a name="user-action"></a>Ação do usuário  
 Procure a causa desse erro no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tente resolver a causa e retomar o espelhamento no banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
