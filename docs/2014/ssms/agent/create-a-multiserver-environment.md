---
title: Criar um ambiente multisservidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, multiserver environments
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- multiserver environments [SQL Server]
ms.assetid: edc2b60d-15da-40a1-8ba3-f1d473366ee6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bacf87c25d7949580eb3d366467e1dae9381e8a4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48115586"
---
# <a name="create-a-multiserver-environment"></a>Criar um ambiente multisservidor
  A administração multisservidor requer a configuração de um servidor mestre (MSX) e de um ou mais servidores de destino (TSX). Os trabalhos a serem processados em todos os servidores de destino são definidos primeiramente no servidor mestre e depois são baixados nos servidores de destino.  
  
 Por padrão, a criptografia SSL completa e a validação de certificado são habilitadas para conexões entre servidores mestres e servidores de destino. Para obter mais informações, veja [Definir opções de criptografia em servidores de destino](set-encryption-options-on-target-servers.md).  
  
 Se você tiver um número grande de servidores de destino, evite definir seu servidor mestre em um servidor de produção que tenha requisitos de desempenho significantes de outra funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , porque o tráfego do servidor de destino pode reduzir o desempenho em seu servidor de produção. Se também encaminhar eventos a um servidor mestre dedicado, você poderá centralizar a administração em um servidor. Para obter mais informações, consulte [Gerenciar eventos](manage-events.md).  
  
> [!NOTE]  
>  Para usar processamento de trabalhos multisservidor, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser membro da função **TargetServersRole** do banco de dados **msdb** no servidor mestre. O Assistente de Servidor Mestre adiciona automaticamente a conta de serviço a essa função como parte do processo de inscrição  
  
## <a name="considerations-for-multiserver-environments"></a>Considerações para ambientes multisservidor  
 Consulte a tabela abaixo para verificar as configurações de MSX/TSX suportadas.  
  
||**TSX = 7.0**|**TSX = 8.0 &LT; SP3**|**TSX = 8.0 SP3 ou superior**|**TSX = 9.0**|**TSX = 10.0**|**TSX = 10,5**|**TSX = 11.0**|  
|-|--------------------|---------------------------|----------------------------------|--------------------|--------------------|---------------------|---------------------|  
|**MSX = 7.0**|Sim|Sim|não|não|não|não|não|  
|**MSX = 8.0 &LT; SP3**|Sim|Sim|não|não|não|não|não|  
|**MSX = 8.0 SP3 ou superior**|não|não|Sim|Sim|Sim|Sim|Sim|  
|**MSX = 9.0**|não|não|não|Sim|Sim|Sim|Sim|  
|**MSX = 10.0**|não|não|não|não|Sim|Sim|Sim|  
|**MSX = 10,5**|não|não|não|não|não|Sim|Sim|  
|**MSX = 11.0**|não|não|não|não|não|não|Sim|  
  
 Considere as seguintes questões ao criar um ambiente multisservidor:  
  
-   Cada servidor de destino se reporta a apenas um servidor mestre. Você deve remover um servidor de destino de um servidor mestre para poder inscrevê-lo em outro.  
  
-   Para alterar o nome de um servidor de destino, primeiro você deve removê-lo antes de alterar o nome e reinscrevê-lo após a alteração.  
  
-   Se desejar desmontar uma configuração multisservidor, você deve remover todos os servidores de destino do servidor mestre.  
  
-   O SQL Server Integration Services oferece suporte apenas aos servidores de destino que têm a mesma versão ou maior que a versão do servidor mestre.  
  
## <a name="related-tasks"></a>Related Tasks  
 Os tópicos a seguir documentam tarefas comuns de criação de um ambiente multisservidor.  
  
|Description|Tópico|  
|-----------------|-----------|  
|Descreve como criar um servidor mestre.|[Criar um servidor mestre](make-a-master-server.md)|  
|Descreve como criar um servidor de destino.|[Criar um servidor de destino](make-a-target-server.md)|  
|Descreve como inscrever um servidor de destino em um servidor mestre.|[Inscrever um servidor de destino em um servidor mestre](enlist-a-target-server-to-a-master-server.md)|  
|Descreve como cancelar a inscrição de um servidor de destino de um servidor mestre.|[Remover um servidor de destino de um servidor mestre](defect-a-target-server-from-a-master-server.md)|  
|Descreve como cancelar a inscrição de vários servidores de destino de um servidor mestre.|[Remover vários servidores de destino de um servidor mestre](defect-multiple-target-servers-from-a-master-server.md)|  
|Descreve como verificar o status de um servidor de destino.|[sp_help_targetserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql)<br /><br /> [sp_help_targetservergroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql)|  
  
## <a name="see-also"></a>Consulte também  
 [Solucionar problemas de trabalhos com multisservidor que usam proxies](troubleshoot-multiserver-jobs-that-use-proxies.md)  
  
  
