---
title: Criar um ambiente multisservidor | Microsoft Docs
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, multiserver environments
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- multiserver environments [SQL Server]
ms.assetid: edc2b60d-15da-40a1-8ba3-f1d473366ee6
caps.latest.revision: "6"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 502763ce7527a31ade9e35cffeaad67e6fae9590
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-multiserver-environment"></a>Criar um ambiente multisservidor
A administração multisservidor requer a configuração de um servidor mestre (MSX) e de um ou mais servidores de destino (TSX). Os trabalhos a serem processados em todos os servidores de destino são definidos primeiramente no servidor mestre e depois são baixados nos servidores de destino.  
  
Por padrão, a criptografia SSL completa e a validação de certificado são habilitadas para conexões entre servidores mestres e servidores de destino. Para obter mais informações, veja [Definir opções de criptografia em servidores de destino](../../ssms/agent/set-encryption-options-on-target-servers.md).  
  
Se você tiver um número grande de servidores de destino, evite definir seu servidor mestre em um servidor de produção que tenha requisitos de desempenho significantes de outra funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , porque o tráfego do servidor de destino pode reduzir o desempenho em seu servidor de produção. Se também encaminhar eventos a um servidor mestre dedicado, você poderá centralizar a administração em um servidor. Para obter mais informações, consulte [Gerenciar eventos](../../ssms/agent/manage-events.md).  
  
> [!NOTE]  
> Para usar processamento de trabalhos multisservidor, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve ser membro da função **TargetServersRole** do banco de dados **msdb** no servidor mestre. O Assistente de Servidor Mestre adiciona automaticamente a conta de serviço a essa função como parte do processo de inscrição  
  
## <a name="considerations-for-multiserver-environments"></a>Considerações para ambientes multisservidor  
  
Considere as seguintes questões ao criar um ambiente multisservidor:  
  
-   Use a versão mais recente do servidor mestre. A versão atual e as duas versões anteriores tem suporte.

-   Cada servidor de destino se reporta a apenas um servidor mestre. Você deve remover um servidor de destino de um servidor mestre para poder inscrevê-lo em outro.  
  
-   Para alterar o nome de um servidor de destino, primeiro você deve removê-lo antes de alterar o nome e reinscrevê-lo após a alteração.  
  
-   Se desejar desmontar uma configuração multisservidor, você deve remover todos os servidores de destino do servidor mestre.  
  
-   O SQL Server Integration Services oferece suporte apenas aos servidores de destino que têm a mesma versão ou maior que a versão do servidor mestre.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
Os tópicos a seguir documentam tarefas comuns de criação de um ambiente multisservidor.  
  
|Description|Tópico|  
|---------------|---------|  
|Descreve como criar um servidor mestre.|[Criar um servidor mestre](../../ssms/agent/make-a-master-server.md)|  
|Descreve como criar um servidor de destino.|[Criar um servidor de destino](../../ssms/agent/make-a-target-server.md)|  
|Descreve como inscrever um servidor de destino em um servidor mestre.|[Inscrever um servidor de destino em um servidor mestre](../../ssms/agent/enlist-a-target-server-to-a-master-server.md)|  
|Descreve como cancelar a inscrição de um servidor de destino de um servidor mestre.|[Remover um servidor de destino de um servidor mestre](../../ssms/agent/defect-a-target-server-from-a-master-server.md)|  
|Descreve como cancelar a inscrição de vários servidores de destino de um servidor mestre.|[Remover vários servidores de destino de um servidor mestre](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)|  
|Descreve como verificar o status de um servidor de destino.|[sp_help_targetserver (Transact-SQL)](http://msdn.microsoft.com/en-us/f841d3bd-901a-4980-ad0b-1c6eeba3f717)<br /><br />[sp_help_targetservergroup (Transact-SQL)](http://msdn.microsoft.com/en-us/ec3a4a68-b591-431c-9518-053ede522d0c)|  
  
## <a name="see-also"></a>Consulte também  
[Solucionar problemas de trabalhos com multisservidor que usam proxies](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
  
