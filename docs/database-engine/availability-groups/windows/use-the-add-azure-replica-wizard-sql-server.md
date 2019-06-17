---
title: Usar o Assistente para Adicionar Réplica do Azure (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: c5dfd05448d59a26ded4672f27ae4ec8ebbdd926
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803425"
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>Use o Assistente para Adicionar Réplica do Azure (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use o Assistente para Adicionar Réplica do Azure para ajudá-lo a criar a nova VM do Microsoft Azure em TI híbrida e a configurá-la como uma réplica secundária para um grupo de disponibilidade AlwaysOn novo ou existente.  
  

##  <a name="BeforeYouBegin"></a> Antes de começar  
 Se você nunca adicionou uma réplica de disponibilidade a um grupo de disponibilidade, veja as seções “Instâncias de servidor” e “Grupos de disponibilidade e réplicas” em [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária atual.  
  
-   Você deve ter um ambiente de TI híbrido onde sua sub-rede local tenha um VPN de site a site com o Windows Azure. Para obter mais informações, veja [Configurar um VPN de site a site no Portal de Gerenciamento](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create).  
  
-   Seu grupo de disponibilidade deve conter réplicas de disponibilidade locais.  
  
-   Os clientes para o ouvinte do grupo de disponibilidade devem ter conectividade com a Internet se quiserem manter a conectividade com o ouvinte quando o grupo de disponibilidade tiver feito o failover em uma réplica do Windows Azure.  
  
-   **Pré-requisitos para usar sincronização de dados inicial total** Você precisará especificar um compartilhamento de rede para que o assistente crie e acesse backups. Para a réplica primária, a conta usada para iniciar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve ter permissões de leitura e gravação no sistema de arquivos em um compartilhamento de rede. Para réplicas secundárias, a conta deve ter permissão de leitura no compartilhamento de rede.  
  
     Se você não puder usar o assistente para executar a sincronização de dados inicial completa, precisará preparar seus bancos de dados secundários manualmente. Você pode fazer isto antes de ou depois de executar o assistente. Para obter mais informações, consulte [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
##  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
 Também requer a permissão CONTROL ON ENDPOINT se você desejar permitir que o Assistente para Adicionar Réplica ao Grupo de Disponibilidade gerencie o ponto de extremidade de espelhamento de banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o Assistente para Adicionar Réplica do Azure (SQL Server Management Studio)  
 O Assistente para Adicionar Réplica do Azure pode ser iniciado a partir da [Página Especificar Réplicas](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md). Há duas maneiras de chegar a essa página:  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Quando você tiver iniciado o Assistente para Adicionar Réplica do Azure, siga as etapas abaixo:  
  
1.  Primeiro, baixe o certificado de gerenciamento para a sua assinatura do Windows Azure. Clique em **Download** para abrir a página de entrada.  
  
2.  Entre no Microsoft Azure com sua conta da Microsoft ou conta organizacional. Sua conta da Microsoft ou organizacional está no formato de um endereço de email, como HYPERLINK “mailto:patc@contoso.com” patc@contoso.com. Para obter mais informações sobre as credenciais do Azure, veja [Perguntas Frequentes sobre a Conta Institucional Microsoft](https://technet.microsoft.com/jj592903) e [Solucionando problemas de logon com sua conta organizacional](https://support.microsoft.com/kb/2756852).  
  
3.  Em seguida, conecte-se à sua assinatura clicando em **Conectar**. Quando você estiver conectado, as listas suspensas serão populadas com seus parâmetros do Microsoft Azure, como **Rede Virtual** e **Sub-Rede de Rede Virtual**.  
  
4.  Especifique as configurações para a máquina virtual do Windows Azure que hospedará a nova réplica secundária:  
  
     image  
     O nome da imagem do SQL Server a ser usada para a máquina virtual do Windows Azure  
  
     Tamanho da máquina virtual  
     O tamanho da máquina virtual do Windows Azure  
  
     Nome da máquina virtual  
     O nome DNS da máquina virtual do Windows Azure  
  
     Nome de usuário da máquina virtual  
     O nome de usuário do administrador padrão para a máquina virtual do Windows Azure  
  
     Senha do administrador da máquina virtual (e confirmar senha)  
     A senha para o administrador padrão para a máquina virtual do Windows Azure  
  
     Rede Virtual  
     A rede virtual na qual colocar a máquina virtual do Windows Azure  
  
     Sub-Rede de Rede Virtual  
     A sub-rede da rede virtual na qual colocar a máquina virtual do Windows Azure  
  
     Domínio  
     O domínio do Active Directory (AD) para adicionar a máquina virtual do Windows Azure  
  
     Nome de usuário de domínio  
     O nome de usuário do AD usado para adicionar a máquina virtual do Windows Azure ao domínio  
  
     Senha  
     A senha usada para adicionar a máquina virtual do Windows Azure ao domínio  
  
5.  Clique em **OK** para confirmar as configurações e sair do Assistente para Adicionar Réplica do Azure.  
  
6.  Continue com o restante das etapas de configuração para a [Página Especificar Réplicas](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) da mesma maneira que faria para qualquer nova réplica.  
  
     Depois que você tiver terminado com o Assistente de Grupo de Disponibilidade ou o Assistente para Adicionar Réplica a Grupo de Disponibilidade, o processo de configuração executará todas as operações no Microsoft Azure para criar a nova VM, adicioná-la ao domínio do AD, adicioná-la ao cluster do Windows, habilitar a alta disponibilidade AlwaysOn e adicionar a nova réplica ao grupo de disponibilidade.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
