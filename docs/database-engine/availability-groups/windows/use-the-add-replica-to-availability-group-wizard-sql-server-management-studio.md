---
title: Adicionar réplica a um grupo de disponibilidade (SSMS)
ms.description: Add a replica to an Always On availability group using the wizard found in SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], wizards
ms.assetid: 60d962b6-2af4-4394-9190-61939a102bc0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: afca5e00f95056fc201f37260088c90004ff3d1f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75244977"
---
# <a name="add-a-replica-to-your-always-on-availability-group-using-the-availability-group-wizard-in-sql-server-management"></a>Adicionar uma réplica ao grupo de disponibilidade Always On usando o Assistente de Grupo de Disponibilidade no SQL Server Management
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use o **Assistente para Adicionar Réplica ao Grupo de Disponibilidade** para ajudá-lo a adicionar uma nova réplica secundária a um grupo de disponibilidade AlwaysOn existente.  
  
> [!NOTE]  
>  Para obter informações sobre como usar [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell para adicionar uma réplica secundária a um grupo de disponibilidade, veja [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md).  
    
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Se você nunca adicionou uma réplica de disponibilidade a um grupo de disponibilidade, veja as seções “Instâncias de servidor” e “Grupos de disponibilidade e réplicas” em [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária atual.  
  
-   Antes de adicionar uma réplica secundária, verifique se a instância host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está no mesmo WSFC (Cluster de Failover do Windows Server) das réplicas existentes, mas reside em um nó de cluster diferente. Verifique também se essa instância de servidor atende a todos os outros pré-requisitos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Para obter mais informações, veja [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Se uma instância de servidor selecionada para hospedar uma réplica de disponibilidade estiver sendo executada em uma conta de usuário de domínio e ainda não tiver um ponto de extremidade de espelhamento de banco de dados, o assistente poderá criar o ponto de extremidade e conceder a permissão CONNECT à conta de serviço da instância de servidor. No entanto, se o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estiver sendo executado como uma conta interna, como Sistema Local, Serviço Local ou Serviço de Rede, ou como uma conta que não pertença a um domínio, você deverá usar certificados para autenticação de ponto de extremidade, e o assistente não poderá criar um ponto de extremidade de espelhamento de banco de dados na instância de servidor. Nesse caso, é recomendável criar pontos de extremidade de espelhamento de banco de dados manualmente antes de iniciar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade.  
  
     **Para usar certificados para um ponto de extremidade de espelhamento de banco de dados:**  
  
     [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)  
  
     [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   **Pré-requisitos para usar sincronização de dados inicial total**  
  
    -   Todos os caminhos de arquivos do banco de dados devem ser idênticos em cada instância de servidor que hospede uma réplica para o grupo de disponibilidade.  
  
    -   Não pode haver nome de banco de dados em nenhuma instância de servidor que hospeda uma réplica secundária. Isto significa que nenhum dos novos bancos de dados secundários pode existir ainda.  
  
    -   Você precisará especificar um compartilhamento de rede para que o assistente crie e acesse backups. Para a réplica primária, a conta usada para iniciar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve ter permissões de leitura e gravação no sistema de arquivos em um compartilhamento de rede. Para réplicas secundárias, a conta deve ter permissão de leitura no compartilhamento de rede.  
  
     Se você não puder usar o assistente para executar a sincronização de dados inicial completa, precisará preparar seus bancos de dados secundários manualmente. Você pode fazer isto antes de ou depois de executar o assistente. Para obter mais informações, consulte [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
   
## <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
 Também requer a permissão CONTROL ON ENDPOINT se você desejar permitir que o Assistente para Adicionar Réplica ao Grupo de Disponibilidade gerencie o ponto de extremidade de espelhamento de banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o Assistente para Adicionar Réplica ao Grupo de Disponibilidade (SQL Server Management Studio)  
 **Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância do servidor que hospeda a réplica primária do grupo de disponibilidade e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade**.  
  
3.  Clique com o botão direito do mouse no grupo de disponibilidade ao qual uma réplica secundária está sendo adicionada e selecione **Adicionar Réplica** . Isso inicia o Assistente para Adicionar Réplica ao Grupo de Disponibilidade.  
  
4.  Na página **Conectar a Réplicas Secundárias Existentes** , conecte-se a cada réplica secundária do grupo de disponibilidade. Para obter mais informações, veja [Conectar à página Réplicas Secundárias Existentes &#40;Assistente para Adicionar Réplica: Assistente para Adicionar Bancos de Dados&#41;](../../../database-engine/availability-groups/windows/connect-to-existing-secondary-replicas-page.md).  
  
5.  Na página **Especificar Réplicas** , especifique e configure uma ou mais novas réplicas secundárias para o grupo de disponibilidade. Essa página contém três guias. A tabela a seguir apresenta essas guias. Para obter mais informações, veja [Página Especificar Réplicas &#40;Assistente de Novo Grupo de Disponibilidade: Assistente para Adicionar Réplica&#41;](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md).  
  
    |Tab|Breve descrição|  
    |---------|-----------------------|  
    |**Réplicas**|Use esta guia para especificar cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedará uma nova réplica secundária.|  
    |**Pontos de extremidade**|Use esta guia para verificar o ponto de extremidade de espelhamento de banco de dados existente, se houver, para cada nova réplica secundária. Se esse ponto de extremidade estiver ausente em uma instância de servidor cujas contas de serviço usam a Autenticação do Windows, o assistente tentará criar o ponto de extremidade automaticamente.<br /><br /> <br /><br /> Observação: se alguma instância de servidor estiver sendo executada em uma conta de usuário que não pertença a um domínio, você precisará fazer uma alteração manual na instância de servidor para que possa continuar as etapas do assistente. Para obter mais informações, consulte [Pré-requisitos](#Prerequisites)anteriormente neste tópico.|  
    |**Preferências de backup**|Use esta guia para especificar sua preferência de backup para o grupo de disponibilidade como um todo, se você deseja modificar a configuração atual, e para especificar suas prioridades de backup para as réplicas de disponibilidade individuais.|  
  
6.  Se as réplicas selecionadas contiverem bancos de dados que têm uma chave mestra de banco de dados, insira as senhas das chaves mestras de banco de dados na coluna **Senha**. A coluna **Status** indica **Senha necessária** para os bancos de dados que têm uma chave mestra de banco de dados. **Próximo** fica esmaecido até que a senha correta seja inserida na coluna **Senha**. Depois de inserir as senhas, clique em **Atualizar**. Se você tiver digitado as senhas corretamente, a coluna Status indicará **Senha digitada** e a opção **Próximo** se tornará disponível.  
  
7.  Na página **Selecionar Sincronização de Dados Inicial** , escolha como você deseja que seus novos bancos de dados secundários sejam criados e unidos ao grupo de disponibilidade. Escolha uma das seguintes opções:  
  
    -   **Full**  
  
         Selecione esta opção se seu ambiente atender aos requisitos para iniciar automaticamente a sincronização de dados inicial (para obter mais informações, veja [Pré-requisitos, restrições e recomendações](#Prerequisites), anteriormente neste tópico).  
  
         Se você selecionar **Total**, depois de criar o grupo de disponibilidade, o assistente fará backup de todos os bancos de dados primários e de seu log de transações em um compartilhamento de rede e restaurará os backups em todas as instâncias de servidor que hospedam uma nova réplica secundária. Em seguida, o assistente unirá cada novo banco de dados secundário ao grupo de disponibilidade.  
  
         No campo **Especificar um local de rede compartilhado acessível por todas as réplicas:** , especifique um compartilhamento de backup ao qual todas as instâncias do servidor que hospedam réplicas de host têm acesso de leitura/gravação. Os backups de log farão parte de sua cadeia de backup de log. Armazene os arquivos de backup de log adequadamente.  
  
        > [!IMPORTANT]  
        >  Para obter informações sobre as permissões necessárias do sistema de arquivos, veja [Pré-requisitos](#Prerequisites), acima neste tópico.  
  
    -   **Somente junção**  
  
         Se preparou bancos de dados secundários manualmente nas instâncias do servidor que hospedam as novas réplicas secundárias, você poderá selecionar essa opção. O assistente unirá esses novos bancos de dados secundários ao grupo de disponibilidade.  
  
    -   **Ignorar sincronização de dados inicial**  
  
         Selecione esta opção se desejar usar seus próprios backups de banco de dados e de log de seus bancos de dados primários. Para obter mais informações, veja [Iniciar movimentação de dados em um banco de dados secundário &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
8.  A página **Validação** verifica se os valores especificados neste Assistente atendem aos requisitos do Assistente para Adicionar Réplica ao Grupo de Disponibilidade. Para fazer uma alteração, clique em **Anterior** para retornar a uma página anterior do assistente para alterar um ou mais valores. Clique em **Avançar** para retornar à página **Validação** e clique em **Executar Novamente a Validação**.  
  
9. Na página **Resumo** , revise as opções escolhidas para o novo grupo de disponibilidade. Para fazer uma alteração, clique em **Anterior** para retornar à página relevante. Após fazer a alteração, clique em **Avançar** para retornar à página **Resumo** .  
  
     Se estiver satisfeito com a seleções, opcionalmente, clique em Script para criar um script das etapas que o assistente executará. Em seguida, para criar e configurar o novo grupo de disponibilidade, clique em **Concluir**.  
  
10. A página **Progresso** exibe o progresso das etapas de criação do grupo de disponibilidade (configuração de pontos de extremidade, criação do grupo de disponibilidade e ingresso da réplica secundária no grupo).  
  
11. Quando essas etapas forem concluídas, a página **Resultados** exibirá o resultado de cada etapa. Se todas essas etapas tiverem êxito, o novo grupo de disponibilidade será configurado completamente. Se quaisquer das etapas resultar em um erro, você poderá precisar concluir a configuração manualmente. Para obter informações sobre a causa de um determinado erro, clique no link de "Erro" associado na coluna **Resultado** .  
  
     Quando o assistente for concluído, clique em **Fechar** para sair.  
  
> [!IMPORTANT]  
>  Depois de adicionar uma réplica, veja a seção “Acompanhamento: depois de adicionar uma réplica secundária” em [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
