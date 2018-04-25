---
title: Iniciador do Daemon de Filtro de Texto Completo do SQL (guia Fazer Logon)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 13e260f9-a75f-430b-88a3-959ddcead8fe
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f54e45734a06030f3a216eea5247a555a94673c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sql-full-text-filter-daemon-launcher-log-on-tab"></a>Iniciador do Daemon de Filtro de Texto Completo do SQL (guia Fazer Logon)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o serviço do Iniciador do Daemon de Filtro de Texto Completo do SQL (Iniciador FDHOST) é usado pela pesquisa de texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este serviço deverá estar em execução se você usar a pesquisa de texto completo. Para obter informações sobre os processos do host do daemon de filtro, consulte "Arquitetura da pesquisa de texto completo" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Use a guia **Fazer Logon** da caixa de diálogo **Propriedades do Iniciador do Daemon de Filtro de Texto Completo do SQL** para especificar a conta usada pelo serviço de texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , para alterar a senha de uma conta e para iniciar e parar o serviço. A alteração da senha de uma conta entra em vigor após o reinício do serviço.  
  
> [!NOTE]  
>  Ao alterar o nome da conta usado por um serviço em uma instância clusterizada, a nova conta deverá ser membro do grupo de domínio especificado durante a instalação do serviço ou você deverá ter permissão para adicionar membros a esse grupo. Se você não tiver permissão para modificar a associação de grupo, contate o administrador de domínio.  
>   
>  Para obter mais informações sobre como selecionar uma conta para executar o serviço, consulte "Configurando as contas de serviço do Windows" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Conta interna**  
 **Sistema Local**  
 Especifique a conta Sistema Local. Essa conta não requer uma senha. No entanto, ela pode impedir a interação do serviço com outros servidores, dependendo dos privilégios concedidos a ela.  
  
 **Serviço Local**  
 Especifique a conta de serviço local. Essa conta não requer uma senha. No entanto, ela pode impedir a interação do serviço com outros servidores, dependendo dos privilégios concedidos a ela.  
  
 **Serviço de Rede**  
 É recomendável não usar a conta do Serviço de Rede para os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. As contas de Usuário Local ou Usuário de Domínio são mais apropriadas para esses serviços.  
  
 **Esta conta**  
 Especifique um local ou conta de usuário do domínio que utilize Autenticação do Windows. É recomendável usar uma conta de usuário de domínio com direitos mínimos para serviços.  
  
 **Nome da Conta**  
 Especifique o nome da conta local ou de usuário de domínio.  
  
 **Senha**  
 Digite a senha da conta.  
  
 **Confirmar senha**  
 Digite a senha da conta novamente.  
  
 **Iniciar**  
 Inicie o serviço.  
  
 **Parar**  
 Parar o serviço.  
  
 **Pausar**  
 Pausar o serviço. Não disponível para este serviço.  
  
 **Retomar**  
 Retomar um serviço pausado.  
  
  
