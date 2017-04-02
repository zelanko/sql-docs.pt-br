---
title: "Importar Dados de Tabelas (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad5b83b1-8e40-4ef8-9ba8-4ea17a58b672
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Importar Dados de Tabelas (Master Data Services)
  Você pode adicionar dados e fazer alterações de dados a um modelo em [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], em massa.  
  
 **Pré-requisitos**  
  
-   Você deve ter permissão para inserir dados na tabelas stg.\<name>_Leaf, stg.\<name>_Consolidated, stg.\<name>_Relationship do banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
-   Você deve ter permissões para executar o procedimento armazenado stg.udp_\<name>_Leaf, stg.udp\_\<name>_Consolidated ou stg.udp\_\<name>_Relationship, no banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
-   O modelo não deve ter um status de **Confirmado**.  
  
 **Para adicionar, atualizar e excluir dados no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]**  
  
1.  Prepare os membros para importação na tabela de preparo adequada no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , incluindo fornecer valores para os campos requisitados. Para obter uma visão geral das tabelas de preparo, consulte [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
    -   Para membros folha, a tabela é stg.\<name>_Leaf, em que \<name> refere-se à entidade correspondente. Para obter informações sobre os campos obrigatórios, consulte [Tabela de preparo de membros folha &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
    -   Para membros consolidados, a tabela é stg.\<name>_Consolidated. Para obter informações sobre os campos obrigatórios, consulte [Tabela de preparo de membros consolidados &#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md).  
  
    -   Para mover o local dos membros em hierarquias explícitas, a tabela é stg.\<name>_Relationship. Para obter informações sobre os campos obrigatórios, consulte [Tabela de preparo de relações &#40;Master Data Services&#41;](../master-data-services/relationship-staging-table-master-data-services.md).  
  
         Para obter uma visão geral sobre como mover membros em hierarquias explícitas, consulte [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).  
  
    -   Use o valor do campo **ImportType** para especificar que você está criando novos membros, desativando membros ou excluindo membros. Para obter mais informações sobre os valores, consulte [Tabela de preparo de membros folha &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md) e [Tabela de preparo de membros consolidados &#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md).  
  
         Para obter uma visão geral de como desativar e excluir membros, consulte [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).  
  
2.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e conecte-se à instância do mecanismo de banco de dados do seu banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
     Para obter mais informações, consulte [SQL Server Management Studio](../Topic/SQL%20Server%20Management%20Studio.md).  
  
3.  Importe dados para tabelas de preparo usando o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
     Para obter mais informações, consulte [SQL Server Import and Export Wizard](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md).  
  
4.  Carregue os dados das tabelas de preparo para as tabelas do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , seguindo um destes procedimentos  
  
    -   Execute o procedimento armazenado de preparo que corresponde à tabela de preparo para a qual você deseja mover os dados.  
  
         Para obter uma visão geral de procedimentos armazenados de preparo e tabelas de preparo, consulte [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md). Para obter mais informações sobre os parâmetros de preparo de procedimentos armazenados e um exemplo de código, consulte [Preparando um procedimento armazenado &#40;Master Data Services&#41;](../master-data-services/staging-stored-procedure-master-data-services.md).  
  
    -   Use a área funcional **Gerenciamento de Integração** do Gerenciamento de Dados Mestre.  
  
         Na página **Lotes de Preparo**, selecione o modelo ao qual você está adicionando dados na lista suspensa e clique em **Iniciar Lotes**. O status do processamento em lotes é indicado no campo **Status** . Para obter mais informações sobre os status, consulte [Status de importação &#40;Master Data Services&#41;](../master-data-services/import-statuses-master-data-services.md).  
  
         ![Staging Batches Page in Master Data Manager](../master-data-services/media/mds-stagingbatchespage.png "Staging Batches Page in Master Data Manager")  
  
         O processo de preparo é iniciado em intervalos determinados pela configuração de **Intervalo de lotes de preparo** no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
5.  Exiba os erros ocorridos durante o preparo. Para obter mais informações, consulte [Exibir erros que ocorrem durante o preparo &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md) e [Erros de processo de preparo &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).  
  
6.  Valide os dados em relação às regras de negócio.  
  
     No Master Data Manager, navegue até a área funcional **Gerenciador** do seu modelo e, em seguida, aplique as regras de negócio para validar os dados. Para obter mais informações, consulte [Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md). Você também pode usar um procedimento armazenado para validar os dados. Para obter mais informações, consulte [Procedimento armazenado de validação &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md).  
  
     Quando você carrega dados com as tabelas de preparo, os dados não são validados automaticamente em relação às regras de negócio. Para obter mais informações sobre o que é a validação e quando ela ocorre, consulte [Validação &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md).  
  
  