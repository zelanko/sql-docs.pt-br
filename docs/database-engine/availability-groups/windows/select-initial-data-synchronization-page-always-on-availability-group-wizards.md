---
title: "Selecione a P&#225;gina de Sincroniza&#231;&#227;o de Dados Inicial (Assistentes Grupo de Disponibilidade AlwaysOn) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.adddatabasewizard.selectinitialdatasync.f1"
  - "sql13.swb.newagwizard.selectinitialdatasync.f1"
  - "sql13.swb.addreplicawizard.selectinitialdatasync.f1"
ms.assetid: 457b1140-4819-4def-8f7c-54a406e6db12
caps.latest.revision: 39
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 39
---
# Selecione a P&#225;gina de Sincroniza&#231;&#227;o de Dados Inicial (Assistentes Grupo de Disponibilidade AlwaysOn)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Use a página **Selecionar Sincronização de Dados Inicial** do AlwaysOn para indicar sua preferência por sincronização de dados inicial de novos bancos de dados secundários. Essa página é compartilhada por três assistentes: o [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)], o [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] e o [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)].  
  
 As opções possíveis incluem **Total**, **Somente junção**ou **Ignorar a sincronização de dados inicial**. Antes de selecionar **Total** ou **Somente junção** verifique se o ambiente atende aos pré-requisitos.  
  
 **Neste tópico:**  
  
-   [Recomendações](#Recommendations)  
  
-   [Full (cheio)](#Full)  
  
-   [Somente junção](#Joinonly)  
  
-   [Ignorar sincronização de dados inicial](#Skip)  
  
-   [Para preparar manualmente bancos de dados secundários](#PrepareSecondaryDbs)  
  
-   [Tarefas relacionadas](#LaunchWiz)  
  
##  <a name="Recommendations"></a> Recomendações  
  
-   Suspenda as tarefas de backup de log para os bancos de dados primários durante a sincronização de dados inicial.  
  
-   Para bancos de dados grandes, as operações de backup completo e de restauração podem utilizar tempo e recursos extensivos. Nesses casos, é recomendável preparar os próprios bancos de dados secundários. Para obter mais informações, consulte [Para preparar manualmente bancos de dados secundários](#PrepareSecondaryDbs)posteriormente neste tópico.  
  
-   A sincronização de dados inicial completa exige que você especifique um compartilhamento de rede. Antes de usar um assistente para executar a sincronização de dados inicial total, é recomendável implementar um plano de segurança para as permissões de acesso na pasta de compartilhamento de rede. Essa precaução é importante porque, potencialmente, dados confidenciais no arquivo de backup podem ser acessados por qualquer pessoa que tenha permissão READ na pasta. Além disso, para proteger as operações de backup e restauração, é recomendável que você proteja os canais de rede entre cada instância do servidor que hospede uma réplica de disponibilidade e a pasta de compartilhamento de rede.  
  
     Se for necessário que as operações de backup e restauração sejam altamente protegidas, é recomendável selecionar a opção **Somente junção** ou **Ignorar a sincronização de dados inicial** .  
  
##  <a name="Full"></a> Total  
 Para cada banco de dados primário, a opção **Total** executará várias operações em um fluxo de trabalho: criará um backup completo e um backup de log do banco de dados primário, criará os bancos de dados secundários correspondentes restaurando esses backups em cada instância do servidor que estiver hospedando uma réplica secundária e unirá cada banco de dados secundário ao grupo de disponibilidade.  
  
 Selecione essa opção apenas se o ambiente atender os seguintes pré-requisitos para usar a sincronização de dados inicial completa, e se você desejar que o assistente inicie automaticamente a sincronização de dados.  
  
 **Pré-requisitos para usar sincronização de dados inicial total**  
  
-   Todos os caminhos de arquivos do banco de dados devem ser idênticos em cada instância de servidor que hospede uma réplica para o grupo de disponibilidade.  
  
    > [!NOTE]  
    >  Se o backup e os caminhos do arquivo de restauração forem diferentes entre a instância de servidor onde você executa o assistente e qualquer instância de servidor que hospede uma réplica secundária. As operações de backup e restauração devem ser executadas manualmente usando a opção WITH MOVE. Para obter mais informações, consulte [Para preparar manualmente bancos de dados secundários](#PrepareSecondaryDbs)posteriormente neste tópico.  
  
-   Não pode haver nome de banco de dados em nenhuma instância de servidor que hospeda uma réplica secundária. Isto significa que nenhum dos novos bancos de dados secundários pode existir ainda.  
  
-   Você precisará especificar um compartilhamento de rede para que o assistente crie e acesse backups. Para a réplica primária, a conta usada para iniciar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve ter permissões de leitura e gravação no sistema de arquivos em um compartilhamento de rede. Para réplicas secundárias, a conta deve ter permissão de leitura no compartilhamento de rede.  
  
    > [!IMPORTANT]  
    >  Os backups de log farão parte de sua cadeia de backup de log. Armazene os arquivos de backup de log adequadamente.  
  
 **Se os pré-requisitos não forem atendidos**  
  
 O assistente não poderá criar os bancos de dados secundários para esse grupo de disponibilidade. Para obter mais informações sobre como prepará-los, consulte [Para preparar manualmente bancos de dados secundários](#PrepareSecondaryDbs)posteriormente neste tópico.  
  
 **Se os pré-requisitos forem atendidos**  
  
 Se estes pré-requisitos forem todos atendidos e você quiser que o assistente execute a sincronização de dados inicial completa, selecione a opção **Completa** e especifique um compartilhamento de rede. Isto fará o assistente criar um banco de dados completo e backups de log de todos os bancos de dados selecionados e colocar estes backups no compartilhamento de rede que você especificar. Em seguida, em cada instância do servidor que hospeda uma das novas réplicas secundárias, o assistente criará os bancos de dados secundários restaurando os backups com RESTORE WITH NORECOVERY. Depois de criar cada um dos bancos de dados secundários, o assistente unirá o novo banco de dados secundário ao grupo de disponibilidade. Assim que um banco de dados secundário é unido, as sincronização de dados é iniciada naquele banco de dados.  
  
 **Especifique um local de rede compartilhado acessível por todas as réplicas**  
 Para criar e restaurar backups, o assistente requer que você especifique um compartilhamento de rede. A conta usada para iniciar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] em cada instância de servidor que hospedará uma réplica de disponibilidade deve ter permissões de leitura e gravação no sistema de arquivos do compartilhamento de rede.  
  
> [!IMPORTANT]  
>  Os backups de log farão parte de sua cadeia de backup de log. Armazene os arquivos de backup adequadamente.  
  
##  <a name="Joinonly"></a> Somente junção  
 Selecione essa opção apenas se os novos bancos de dados secundários já existirem em cada instância do servidor que hospeda uma réplica secundária para o grupo de disponibilidade. Para obter informações sobre como preparar bancos de dados secundários, consulte [Para preparar bancos de dados secundários manualmente](#PrepareSecondaryDbs), posteriormente nesta seção.  
  
 Se você selecionar **Somente junção**, o assistente tentará unir cada banco de dados secundário existente ao grupo de disponibilidade.  
  
## <a name="Skip"></a> Ignorar a sincronização de dados inicial  
 Selecione esta opção se você desejar executar seus próprios backups de banco de dados e de log de cada banco de dados primário e, em seguida, restaurá-los em cada instância de servidor que hospeda uma réplica secundária. Quando sair do assistente, você precisará unir cada banco de dados secundário em cada réplica secundária.  
  
> [!NOTE]  
>  Para obter mais informações, veja [Iniciar movimentação de dados em um banco de dados secundário AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
##  <a name="PrepareSecondaryDbs"></a> Para preparar manualmente bancos de dados secundários  
 Para preparar bancos de dados secundários independentemente de qualquer assistente do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , você pode usar uma das seguintes abordagens:  
  
-   Restaurar manualmente um backup recente do banco de dados primário usando RESTORE WITH NORECOVERY e, em seguida, restaurar cada backup de log subsequente usando RESTORE WITH NORECOVERY. Se os bancos de dados primários e secundários tiverem caminhos de arquivos diferentes, você deverá usar a opção WITH MOVE. Executar essa sequência de restauração em cada instância do servidor que hospeda uma réplica secundária para o grupo de disponibilidade.  Você pode usar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou PowerShell para executar estas operações de backup e restauração.  
  
     **Para obter mais informações, consulte:**  
  
     [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   Se você estiver adicionando um ou mais bancos de dados primários de envio de logs a um grupo de disponibilidade, poderá ser capaz de migrar um ou mais dos bancos de dados secundários correspondentes de envio de logs para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obter mais informações, veja [Pré-requisitos para migrar do envio de logs para os grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs migrating log shipping to always on availability groups.md).  
  
    > [!NOTE]  
    >  Depois que você criar todos os bancos de dados secundários para o grupo de disponibilidade, se você desejar executar backups em réplicas secundárias, precisará reconfigurar a preferência de backup automatizada do grupo de disponibilidade.  
  
     **Para obter mais informações, consulte:**  
  
     [Pré-requisitos para migrar de envio de logs para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs migrating log shipping to always on availability groups.md)  
  
     [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
 Depois de criar um banco de dados secundário, aplique todos os backups de log atuais ao novo banco de dados secundário.  
  
 Opcionalmente, você pode preparar todos os bancos de dados secundários antes de executar o assistente. Em seguida, na página **Especificar a Sincronização de Dados Inicial** do assistente, selecione **Somente junção** para unir automaticamente seus novos bancos de dados secundários ao grupo de disponibilidade.  
  
##  <a name="LaunchWiz"></a> Tarefas relacionadas  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-database-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente de Grupo de Disponibilidade de Failover &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Iniciar movimentação de dados em um banco de dados secundário &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
## Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  