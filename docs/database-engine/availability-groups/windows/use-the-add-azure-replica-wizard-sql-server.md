---
title: Configurar a VM do Azure como uma réplica secundária em um grupo de disponibilidade
description: Use o Assistente para Adicionar Réplica do Azure para criar uma VM do Azure na TI híbrida e configurá-la como uma réplica secundária para um grupo de disponibilidade Always On novo ou existente.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: cawrites
ms.author: chadam
ms.openlocfilehash: 9ff107b2f3e132015e294ef7ba8174ade5a0c575
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583678"
---
# <a name="configure-azure-vm-as-a-secondary-replica-in-an-availability-group"></a>Configurar a VM do Azure como uma réplica secundária em um grupo de disponibilidade
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Use o Assistente para Adicionar Réplica do Azure para criar uma nova VM do Azure em TI híbrida e configurá-la como uma réplica secundária para um grupo de disponibilidade Always On novo ou existente.  

>  [!IMPORTANT]  
>  O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: Resource Manager e Clássico. Este artigo aborda o uso do modelo de implantação Clássica. A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos. As etapas neste artigo não serão aplicáveis se você estiver implantando a máquina virtual do Azure usando o modelo do Resource Manager.   

##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
 Se você nunca adicionou uma réplica de disponibilidade a um grupo de disponibilidade, veja as seções “Instâncias de servidor” e “Grupos de disponibilidade e réplicas” em [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária atual.  
  
-   Você precisa ter um ambiente de TI híbrido onde sua sub-rede local tenha um VPN site a site com o Azure. Para obter mais informações, veja [Configurar um VPN de site a site no Portal de Gerenciamento](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal).  
  
-   Seu grupo de disponibilidade deve conter réplicas de disponibilidade locais.  
  
-   Os clientes para o ouvinte do grupo de disponibilidade precisarão ter conectividade com a Internet se quiserem manter a conectividade com o ouvinte quando o grupo de disponibilidade tiver feito o failover em uma réplica do Azure.  
  
-   **Pré-requisitos para usar sincronização de dados inicial total** Você precisará especificar um compartilhamento de rede para que o assistente crie e acesse backups. Para a réplica primária, a conta usada para iniciar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve ter permissões de leitura e gravação no sistema de arquivos em um compartilhamento de rede. Para réplicas secundárias, a conta deve ter permissão de leitura no compartilhamento de rede.  
  
     Se você não puder usar o assistente para executar a sincronização de dados inicial completa, precisará preparar seus bancos de dados secundários manualmente. Você pode fazer isto antes de ou depois de executar o assistente. Para obter mais informações, consulte [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
##  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
 Também requer a permissão CONTROL ON ENDPOINT se você desejar permitir que o Assistente para Adicionar Réplica ao Grupo de Disponibilidade gerencie o ponto de extremidade de espelhamento de banco de dados.  
  
##  <a name="using-the-add-azure-replica-wizard-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o Assistente para Adicionar Réplica do Azure (SQL Server Management Studio)  

>  [!IMPORTANT]  
>  O Assistente para Adicionar uma Réplica do Azure dá suporte apenas a máquinas virtuais criadas com o modelo de implantação Clássico. As novas implantações de máquina virtual devem usar o modelo mais novo do Resource Manager. Se você estiver usando máquinas virtuais com o Resource Manager, deverá adicionar manualmente a réplica secundária do Azure usando comandos Transact-SQL (não mostrados aqui). Esse assistente não funcionará no cenário do Resource Manager. 
>
>  O Assistente para Adicionar Réplica do Azure não está disponível nas versões mais recentes (versões 18.x e 17.x) do SQL Server Management Studio.
        
 O Assistente para Adicionar Réplica do Azure pode ser iniciado a partir da [Página Especificar Réplicas](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md). Há duas maneiras de chegar a essa página:  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Quando você tiver iniciado o Assistente para Adicionar Réplica do Azure, siga as etapas abaixo:  
  
1.  Primeiro, baixe um certificado de gerenciamento para a sua assinatura do Azure. Clique em **Download** para abrir a página de entrada.  
  
2.  Entre no Microsoft Azure com sua conta da Microsoft ou conta organizacional. Sua conta da Microsoft ou organizacional está no formato de um endereço de email, como HYPERLINK “mailto:patc@contoso.com” patc@contoso.com. Para obter mais informações sobre as credenciais do Azure, veja [Perguntas Frequentes sobre a Conta Institucional Microsoft](/previous-versions/jj592903(v=msdn.10)) e [Solucionando problemas de logon com sua conta organizacional](https://support.microsoft.com/kb/2756852).  
  
3.  Em seguida, conecte-se à sua assinatura clicando em **Conectar**. Quando você estiver conectado, as listas suspensas serão preenchidas com seus parâmetros do Azure, como **Rede Virtual** e **Sub-Rede de Rede Virtual**.  
  
4.  Especifique as configurações da máquina virtual do Azure que hospedará a nova réplica secundária:  
  
     Imagem  
     O nome da imagem do SQL Server a ser usada para a máquina virtual do Azure  
  
     Tamanho da VM  
     O tamanho da máquina virtual do Azure  
  
     Nome da VM  
     O nome DNS da máquina virtual do Azure  
  
     Nome de usuário da máquina virtual  
     O nome de usuário do administrador padrão da máquina virtual do Azure  
  
     Senha do administrador da máquina virtual (e confirmar senha)  
     A senha do administrador padrão da máquina virtual do Azure  
  
     Rede Virtual  
     A rede virtual em que a máquina virtual do Azure será colocada  
  
     Sub-Rede de Rede Virtual  
     A sub-rede da rede virtual em que a máquina virtual do Azure será colocada  
  
     Domínio  
     O domínio do AD (Active Directory) para adicionar a máquina virtual do Azure  
  
     Nome de usuário de domínio  
     O nome de usuário do AD usado para adicionar a máquina virtual do Azure ao domínio  
  
     Senha  
     A senha usada para adicionar a máquina virtual do Azure ao domínio  
  
5.  Clique em **OK** para confirmar as configurações e sair do Assistente para Adicionar Réplica do Azure.  
  
6.  Continue com o restante das etapas de configuração para a [Página Especificar Réplicas](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) da mesma maneira que faria para qualquer nova réplica.  
  
     Depois que você terminar com o Assistente de Grupo de Disponibilidade ou o Assistente para Adicionar Réplica a Grupo de Disponibilidade, o processo de configuração executará todas as operações no Azure para criar a nova máquina virtual, adicioná-la ao domínio do AD, adicioná-la ao cluster do Windows, habilitar a alta disponibilidade Always On e adicionar a nova réplica ao grupo de disponibilidade.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
