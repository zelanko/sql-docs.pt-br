---
title: Propriedades do navegador do SQL Server (guia fazer logon) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c77871ec-c2f4-4e4a-9a10-5aeb4ae70507
caps.latest.revision: "20"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 688b87426feba4128e1c2d8708d0de94a102d94f
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="sql-server-browser-properties-log-on-tab"></a>Propriedades do Navegador do SQL Server (guia Fazer Logon)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programa navegador é executado como um serviço no servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Escuta as solicitações de entrada de recursos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornece informações sobre as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no computador.  
  
 O Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta em uma porta UDP e aceita as solicitações não autenticadas usando o protocolo SSRP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A alteração da senha de uma conta entra em vigor imediatamente sem a reinicialização do serviço.  
  
## <a name="options"></a>Opções  
 **Conta Sistema Local**  
 Execute o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no contexto de segurança da conta Sistema Local. Quando possível, use uma conta de baixa permissão.  
  
 **Esta conta**  
 Especifique um local ou conta de usuário do domínio que utilize Autenticação do Windows. É recomendável usar uma conta de usuário do domínio com direitos mínimos para serviços. Para obter informações sobre como selecionar uma conta, consulte "Configurando as contas de serviço do Windows" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Procurar**  
 Procure um usuário ou uma entidade de segurança incorporada.  
  
> [!IMPORTANT]  
>  Use uma conta da baixa-permissão. Para obter informações sobre as permissões necessárias para o Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte a seção Segurança do tópico [Serviço Navegador do SQL Server](../../tools/configuration-manager/sql-server-browser-service.md).  
  
 **Senha**  
 Digite a senha da entidade de segurança.  
  
 **Confirmar senha**  
 Confirme a senha da entidade de segurança.  
  
 **Status do serviço**  
 Indica se este serviço está sendo executado, se está parado ou desabilitado. "**…**" indica que uma alteração no estado está pendente.  
  
 **Iniciar**  
 Iniciar o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Parar**  
 Parar o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Pausar**  
 Pausar o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Retomar**  
 Retomar um serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em pausa.  
  
## <a name="see-also"></a>Consulte também  
 [Serviço Navegador do SQL Server](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
