---
title: Adicionar um banco de dados a um grupo de disponibilidade com o 'Assistente de Grupo de Disponibilidade'
description: Adicione um banco de dados a um grupo de disponibilidade Always On usando o 'Assistente de Grupo de Disponibilidade' no SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.adddatabasewizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], databases
ms.assetid: 81e5e36d-735d-4731-8017-2654673abb88
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 80c63fa27f1ba85882b18f47910f38c06dd09f51
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800134"
---
# <a name="add-a-database-to-an-always-on-availability-group-with-the-availability-group-wizard"></a>Adicionar um banco de dados a um Grupo de Disponibilidade Always On com o 'Assistente de Grupo de Disponibilidade'
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade para ajudá-lo a adicionar um ou mais bancos de dados a um grupo de disponibilidade AlwaysOn existente.  
  
> [!NOTE]  
>  Para obter informações sobre como usar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell para adicionar um banco de dados, veja [Adicionar um banco de dados a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md).  
  

  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Se você nunca adicionou um banco de dados a um grupo de disponibilidade, veja a seção “Bancos de dados de disponibilidade” em [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
##  <a name="Prerequisites"></a> Pré-requisitos, restrições e recomendações  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária atual.  
  
-   **Pré-requisitos para usar sincronização de dados inicial total**  
  
    -   Todos os caminhos de arquivos do banco de dados devem ser idênticos em cada instância de servidor que hospede uma réplica para o grupo de disponibilidade.  
  
    -   Não pode haver nome de banco de dados em nenhuma instância de servidor que hospeda uma réplica secundária. Isto significa que nenhum dos novos bancos de dados secundários pode existir ainda.  
  
    -   Você precisará especificar um compartilhamento de rede para que o assistente crie e acesse backups. Para a réplica primária, a conta usada para iniciar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve ter permissões de leitura e gravação no sistema de arquivos em um compartilhamento de rede. Para réplicas secundárias, a conta deve ter permissão de leitura no compartilhamento de rede.  
  
     Se você não puder usar o assistente para executar a sincronização de dados inicial completa, precisará preparar seus bancos de dados secundários manualmente. Você pode fazer isto antes de ou depois de executar o assistente. Para obter mais informações, consulte [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
  
##  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="use-the-new-availability-group-wizard"></a>Usar o Assistente de 'Novo Grupo de Disponibilidade'
  
1.  No Pesquisador de Objetos, conecte-se à instância do servidor que hospeda a réplica primária do grupo de disponibilidade e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade**.  
  
3.  Clique com o botão direito do mouse no grupo de disponibilidade no qual você está adicionando um banco de dados e selecione **Adicionar Banco de Dados** . Esse comando inicia o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade.  
  
4.  Na página **Selecionar Bancos de Dados** , selecione um ou mais Bancos de Dados. Para obter mais informações, veja [Página Selecionar Bancos de Dados &#40;Assistente de Novo Grupo de Disponibilidade e Assistente para Adicionar Banco de Dados&#41;](../../../database-engine/availability-groups/windows/select-databases-page-new-availability-group-wizard-and-add-database-wizard.md).  
  
     Se o banco de dados contiver uma chave mestra de banco de dados, insira a senha para a chave mestra de banco de dados na coluna **Senha**.  
  
5.  Na página **Selecionar Sincronização de Dados Inicial** , escolha como você deseja que seus novos bancos de dados secundários sejam criados e unidos ao grupo de disponibilidade. Escolha uma das seguintes opções:  
  
    -   **Full (cheio)**  
  
         Selecione esta opção se seu ambiente atender aos requisitos para iniciar automaticamente a sincronização de dados inicial (para obter mais informações, veja [Pré-requisitos, restrições e recomendações](#Prerequisites), anteriormente neste tópico).  
  
         Se você selecionar **Total**, depois de criar o grupo de disponibilidade, o assistente tentará fazer backup de todos os bancos de dados primários e de seu log de transações em um compartilhamento de rede e restaurará os backups em todas as instâncias de servidor que hospedam uma réplica secundária. Em seguida, o assistente unirá cada banco de dados secundário ao grupo de disponibilidade.  
  
         No campo **Especificar um local de rede compartilhado acessível por todas as réplicas:** , especifique um compartilhamento de backup ao qual todas as instâncias do servidor que hospedam réplicas de host têm acesso de leitura/gravação. Os backups de log farão parte de sua cadeia de backup de log. Armazene os arquivos de backup de log adequadamente.  
  
        > [!IMPORTANT]  
        >  Para obter informações sobre as permissões necessárias do sistema de arquivos, veja [Pré-requisitos](#Prerequisites), acima neste tópico.  
  
    -   **Somente junção**  
  
         Se preparou bancos de dados secundários manualmente nas instâncias do servidor que hospedam réplicas secundárias, você poderá selecionar essa opção. O assistente unirá os bancos de dados secundários existentes ao grupo de disponibilidade.  
  
    -   **Ignorar sincronização de dados inicial**  
  
         Selecione esta opção se desejar usar seus próprios backups de banco de dados e de log de seus bancos de dados primários. Para obter mais informações, veja [Iniciar movimentação de dados em um banco de dados secundário AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
     Para obter mais informações, veja [Página Selecionar Sincronização de Dados Inicial &#40;Assistentes do Grupo de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/select-initial-data-synchronization-page-always-on-availability-group-wizards.md).  
  
6.  Na página **Conectar a Réplicas Secundárias Existentes** , se as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedam réplicas de disponibilidade para esse grupo de disponibilidade estiverem todas executando como um serviço na mesma conta de usuário, clique em **Conectar tudo**. Se qualquer uma das instâncias de servidor estiver executando como um serviço sob conta diferente, clique no **Conectar** individual à direita de cada nome de instância de servidor.  
  
     Para obter mais informações, confira [Página Conectar-se às Réplicas Secundárias Existentes &#40;Assistente para Adicionar Réplica: Assistente para Adicionar Bancos de Dados&#41;](../../../database-engine/availability-groups/windows/connect-to-existing-secondary-replicas-page.md).  
  
7.  A página **Validação** verifica se os valores especificados neste Assistente atendem aos requisitos do Assistente de Novo Grupo de Disponibilidade. Para fazer uma alteração, clique em **Anterior** para retornar a uma página anterior do assistente para alterar um ou mais valores. Clique em **Avançar** para retornar à página **Validação** e clique em **Executar Novamente a Validação**.  
  
     Para obter mais informações, veja [Página Validação &#40;Assistentes do Grupo de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/validation-page-always-on-availability-group-wizards.md).  
  
8.  Na página **Resumo** , revise as opções escolhidas para o novo grupo de disponibilidade. Para fazer uma alteração, clique em **Anterior** para retornar à página relevante. Após fazer a alteração, clique em **Avançar** para retornar à página **Resumo** .  
  
     Para obter mais informações, veja [Página Resumo &#40;Assistentes do Grupo de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/summary-page-always-on-availability-group-wizards.md).  
  
     Se estiver satisfeito com a seleções, opcionalmente, clique em Script para criar um script das etapas que o assistente executará. Em seguida, para criar e configurar o novo grupo de disponibilidade, clique em **Concluir**.  
  
9. A página **Progresso** exibe o progresso das etapas de criação do grupo de disponibilidade (configuração de pontos de extremidade, criação do grupo de disponibilidade e ingresso da réplica secundária no grupo).  
  
     Para obter mais informações, veja [Página Progresso &#40;Assistentes do Grupo de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/progress-page-always-on-availability-group-wizards.md).  
  
10. Quando essas etapas forem concluídas, a página **Resultados** exibirá o resultado de cada etapa. Se todas essas etapas tiverem êxito, o novo grupo de disponibilidade será configurado completamente. Se quaisquer das etapas resultar em um erro, você poderá precisar concluir a configuração manualmente. Para obter informações sobre a causa de um determinado erro, clique no link de "Erro" associado na coluna **Resultado** .  
  
     Quando o assistente for concluído, clique em **Fechar** para sair.  
  
     Para obter mais informações, veja [Página Resultados &#40;Assistentes do Grupo de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/results-page-always-on-availability-group-wizards.md).  
  
11. Se a sincronização de dados inicial não foi iniciada automaticamente em todos os seus bancos de dados secundários, você precisará configurar qualquer banco de dados secundário que ainda não foi unido. Para obter mais informações, veja [Iniciar movimentação de dados em um banco de dados secundário &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Adicionar um banco de dados a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)   
 [Iniciar a movimentação de dados em um banco de dados secundário &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)   
 [Adicionar um banco de dados a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)  
  
  
