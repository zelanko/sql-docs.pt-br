---
title: MSSQLSERVER_1462 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 185a7d78f10656dc932259fb1098570190941afa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746684"
---
# <a name="mssqlserver1462"></a>MSSQLSERVER_1462
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte Também  
[Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
