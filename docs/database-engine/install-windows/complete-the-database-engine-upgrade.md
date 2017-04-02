---
title: "Concluir a atualiza&#231;&#227;o do mecanismo de banco de dados | Microsoft Docs"
ms.custom: ""
ms.date: "09/22/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: 10
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 10
---
# Concluir a atualiza&#231;&#227;o do mecanismo de banco de dados
  Após a conclusão da atualização para o SQL Server 2016, há uma série de etapas adicionais que talvez você precise executar. Entre elas estão as seguintes:  
  
 Depois de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], conclua as seguintes tarefas:  
  
-   **Fazer backup de seus bancos de dados:** faça um backup completo de cada banco de dados atualizado.  
  
-   **Habilitar novos recursos:** no SQL Server 2016, algumas alterações são habilitadas somente quando o nível de DATABASE_COMPATIBILITY para um banco de dados é alterado para 130.  Para obter mais informações e para ver o fluxo de trabalho recomendado, consulte [Alterar o modo de compatibilidade do banco de dados e usar o repositório de consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md).  
  
-   **Integration Services:**  
  
     Migre pacotes do Integration Services para o formato [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para saber mais, confira [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
-   **Reporting Services:** para a atualização de uma nova instalação, restaure as chaves de criptografia do Reporting Services. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/back-up-and-restore-reporting-services-encryption-keys.md).  
  
-   **Master Data Services:**  atualize o esquema de banco de dados do MDS e crie o aplicativo Web do SQL Server 2016. Para saber mais, confira [Upgrade Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md).  
  
-   **Data Quality Services:** atualize o esquema de bancos de dados do DQS e verifique a atualização do esquema de bancos de dados do DQS. Para saber mais, confira [Upgrade Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md).  
  
-   **Pesquisa de Texto Completo:** popule novamente catálogos de texto completo para garantir a consistência semântica em resultados da consulta. Para obter mais informações, veja [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
## Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários a [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Complete%20the%20Database%20Engine%20Upgrade%20page).  
  
  