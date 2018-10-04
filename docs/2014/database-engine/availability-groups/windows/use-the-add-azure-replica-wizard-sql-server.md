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
manager: craigg
ms.openlocfilehash: f2b925540844a45d94fb2ee823a8ac5e9bc7ef2a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095636"
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>Use o Assistente para Adicionar Réplica do Azure (SQL Server)
  Use o Assistente para Adicionar Réplica do Azure para ajudá-lo a criar a nova máquina virtual do Windows Azure em TI híbrida e a configurá-la como uma réplica secundária para um novo ou grupo de disponibilidade AlwaysOn existente.  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para adicionar uma réplica usando:**  [Assistente para Adicionar Réplica do Azure (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Se você nunca adicionou uma réplica de disponibilidade para um grupo de disponibilidade, consulte "Instâncias de servidor" e "grupos de disponibilidade e réplicas" seções [pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária atual.  
  
-   Você deve ter um ambiente de TI híbrido onde sua sub-rede local tenha um VPN de site a site com o Windows Azure. Para obter mais informações, veja [Configurar um VPN de site a site no Portal de Gerenciamento](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create).  
  
-   Seu grupo de disponibilidade deve conter réplicas de disponibilidade locais.  
  
-   Os clientes para o ouvinte do grupo de disponibilidade devem ter conectividade com a Internet se quiserem manter a conectividade com o ouvinte quando o grupo de disponibilidade tiver feito o failover em uma réplica do Windows Azure.  
  
-   **Pré-requisitos para usar sincronização de dados inicial total** Você precisará especificar um compartilhamento de rede para que o assistente crie e acesse backups. Para a réplica primária, a conta usada para iniciar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve ter permissões de leitura e gravação no sistema de arquivos em um compartilhamento de rede. Para réplicas secundárias, a conta deve ter permissão de leitura no compartilhamento de rede.  
  
     Se você não puder usar o assistente para executar a sincronização de dados inicial completa, precisará preparar seus bancos de dados secundários manualmente. Você pode fazer isto antes de ou depois de executar o assistente. Para obter mais informações, consulte [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Consulte [Security](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)  
  
##  <a name="SSMSProcedure"></a> Usando o Assistente para Adicionar Réplica do Azure (SQL Server Management Studio)  
 O Assistente para Adicionar Réplica do Azure pode ser iniciado a partir da [Página Especificar Réplicas](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md). Há duas maneiras de chegar a essa página:  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Quando você tiver iniciado o Assistente para Adicionar Réplica do Azure, siga as etapas abaixo:  
  
1.  Primeiro, baixe o certificado de gerenciamento para a sua assinatura do Windows Azure. Clique em **Download** para abrir a página de entrada.  
  
2.  Na página de entrada, entre com a sua assinatura do Windows Azure. Quando você estiver conectado, o assistente instalará um certificado de gerenciamento no computador local. Esse certificado de gerenciamento é carregado automaticamente quando você usa esse assistente novamente. Se você baixou vários certificados de gerenciamento, poderá clicar no botão **...** para selecionar o que deseja usar.  
  
3.  Em seguida, conecte-se à sua assinatura clicando em **Conectar**. Quando você estiver conectado, as listas suspensas serão populadas com seus parâmetros do Microsoft Azure, como **Rede Virtual** e **Sub-Rede de Rede Virtual**.  
  
4.  Especifique as configurações para a máquina virtual do Windows Azure que hospedará a nova réplica secundária:  
  
     Imagem  
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
  
6.  Continue com o restante das etapas de configuração para a [Página Especificar Réplicas](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) da mesma maneira que faria para qualquer nova réplica.  
  
     Depois que você tiver terminado com o Assistente de Grupo de Disponibilidade ou o Assistente para Adicionar Réplica a Grupo de Disponibilidade, o processo de configuração executará todas as operações no Windows Azure para criar a nova máquina virtual, adicioná-la ao domínio do AD, adicioná-la ao cluster do Windows, habilitar a alta disponibilidade AlwaysOn e adicionar a nova réplica ao grupo de disponibilidade.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
