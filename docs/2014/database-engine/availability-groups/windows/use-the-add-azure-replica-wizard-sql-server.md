---
title: Usar o Assistente para Adicionar Réplica do Azure (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 95cb279c939298256a623d67e3db8f979f65c40f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936257"
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>Use o Assistente para Adicionar Réplica do Azure (SQL Server)
  Use o assistente para adicionar réplica do Azure para ajudá-lo a criar uma nova VM do Azure em ti híbrida e configurá-la como uma réplica secundária para um grupo de disponibilidade AlwaysOn novo ou existente.  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para adicionar uma réplica usando:**  [Assistente para Adicionar Réplica do Azure (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
 Se você nunca adicionou nenhuma réplica de disponibilidade a um grupo de disponibilidade, consulte as seções "instâncias de servidor" e "grupos de disponibilidade e réplicas" em [pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária atual.  
  
-   Você precisa ter um ambiente de TI híbrido onde sua sub-rede local tenha um VPN site a site com o Azure. Para obter mais informações, veja [Configurar um VPN de site a site no Portal de Gerenciamento](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create).  
  
-   Seu grupo de disponibilidade deve conter réplicas de disponibilidade locais.  
  
-   Os clientes para o ouvinte do grupo de disponibilidade precisarão ter conectividade com a Internet se quiserem manter a conectividade com o ouvinte quando o grupo de disponibilidade tiver feito o failover em uma réplica do Azure.  
  
-   **Pré-requisitos para usar sincronização de dados inicial total** Você precisará especificar um compartilhamento de rede para que o assistente crie e acesse backups. Para a réplica primária, a conta usada para iniciar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve ter permissões de leitura e gravação no sistema de arquivos em um compartilhamento de rede. Para réplicas secundárias, a conta deve ter permissão de leitura no compartilhamento de rede.  
  
     Se você não puder usar o assistente para executar a sincronização de dados inicial completa, precisará preparar seus bancos de dados secundários manualmente. Você pode fazer isto antes de ou depois de executar o assistente. Para obter mais informações, consulte [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Consulte [Security](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)  
  
##  <a name="using-the-add-azure-replica-wizard-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o assistente para adicionar réplica do Azure (SQL Server Management Studio)  
 O Assistente para Adicionar Réplica do Azure pode ser iniciado a partir da [Página Especificar Réplicas](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md). Há duas maneiras de chegar a essa página:  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Quando você tiver iniciado o Assistente para Adicionar Réplica do Azure, siga as etapas abaixo:  
  
1.  Primeiro, baixe um certificado de gerenciamento para a sua assinatura do Azure. Clique em **Download** para abrir a página de entrada.  
  
2.  Na página de entrada, entre na sua assinatura do Azure. Quando você estiver conectado, o assistente instalará um certificado de gerenciamento no computador local. Esse certificado de gerenciamento é carregado automaticamente quando você usa esse assistente novamente. Se você baixou vários certificados de gerenciamento, poderá clicar no botão **...** para selecionar o que deseja usar.  
  
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
  
6.  Continue com o restante das etapas de configuração para a [Página Especificar Réplicas](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) da mesma maneira que faria para qualquer nova réplica.  
  
     Depois de concluir o assistente de grupo de disponibilidade ou o assistente para adicionar réplica ao grupo de disponibilidade, o processo de configuração executará todas as operações no Azure para criar a nova VM, associá-la ao domínio do AD, adicioná-la ao cluster do Windows, habilitar a alta disponibilidade AlwaysOn e adicionar a nova réplica ao grupo de disponibilidade.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
