---
title: MSSQLSERVER_1462 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e1de41c30aae242bdb5fae3524b06e98bad21863
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013123"
---
# <a name="mssqlserver1462"></a>MSSQLSERVER_1462
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1462|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_DISABLED_DUE_TO_FAILED_REDO|  
|Texto da mensagem|O espelhamento de banco de dados foi desabilitado devido a uma falha na operação refazer. Não é possível retomar.|  
  
## <a name="explanation"></a>Explicação  
 Houve falha no espelhamento de banco de dados ao refazer um registro de log no espelho.  
  
### <a name="possible-causes"></a>Causas possíveis  
 A causa mais provável é que uma operação de adicionar arquivo tenha sido concluída no banco de dados principal, mas tenha apresentado falha no banco de dados espelho porque os nomes de arquivo ou as estruturas de diretório diferiam no servidor principal e no servidor espelho.  
  
## <a name="user-action"></a>Ação do usuário  
 Procure a causa desse erro no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tente resolver a causa e retomar o espelhamento no banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  