---
description: MSSQLSERVER_1462
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
ms.openlocfilehash: 26254a4cac29b4295c3cf163c0f09b2ce6d818aa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88334072"
---
# <a name="mssqlserver_1462"></a>MSSQLSERVER_1462
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
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
[Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
