---
title: Solucionar problemas de trabalhos com multisservidor que usam proxies | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 765198145f6278635ffdf299a3aef1540aa0bdc3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224706"
---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>Solucionar problemas de trabalhos multisservidor que usam proxies
  Trabalhos distribuídos cujas etapas estejam associadas a um proxy são executados no contexto da conta proxy no servidor de destino. Se as etapas de trabalho que usam contas proxy falharem ao serem baixadas do servidor mestre, verifique a coluna **error_message** da tabela **sysdownloadlist** no banco de dados **msdb** quanto às seguintes mensagens de erro:  
  
-   "A etapa do trabalho requer uma conta proxy. Entretanto, a verificação de proxy está desabilitada no servidor de destino."  
  
     Para resolver este erro, defina a subchave do Registro **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.***\<n*>** \SQLServerAgent\AllowDownloadedJobsToMatchProxyName** como **1 (verdadeiro)**. Por padrão, essa subchave é definida como **0** (`false`). O valor de **MSSQL.**\<*n*> é o nome de instância; por exemplo, **MSSQL.1** ou **MSSQL.3**.  
  
-   "Proxy não localizado."  
  
     Para resolver este erro, verifique se existe uma conta proxy no servidor de destino com o mesmo nome da conta proxy do servidor mestre sob a qual a etapa de trabalho é executada.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Criar um ambiente multisservidor](create-a-multiserver-environment.md)  
  
  
