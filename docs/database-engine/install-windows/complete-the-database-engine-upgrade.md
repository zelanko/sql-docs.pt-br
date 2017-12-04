---
title: Concluir o upgrade do mecanismo de banco de dados | Microsoft Docs
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: "10"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: f02ff71df24b1e1a8f6c17fd8c6edbdfa02c60a5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="complete-the-database-engine-upgrade"></a>Concluir a atualização do mecanismo de banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Após a conclusão da atualização do SQL Server, há uma série de etapas adicionais que talvez precisem ser realizadas. Entre elas estão as seguintes:  
  
Depois de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], conclua as seguintes tarefas:  
  
- **Fazer backup dos bancos de dados:** faça um backup completo de cada banco de dados.  

- **Habilitar novos recursos:** no SQL Server 2016 e SQL Server 2017, algumas alterações são habilitadas somente quando o nível de DATABASE_COMPATIBILITY de um banco de dados é alterado para 130 ou superior.  Para obter mais informações e para ver o fluxo de trabalho recomendado, consulte [Alterar o modo de compatibilidade do banco de dados e usar o repositório de consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md). Se o banco de dados tiver tabelas com otimização de memória criadas no SQL Server 2014, examine [Estatísticas para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md).
  
- **Integration Services:**  
  
     Migre pacotes do Integration Services para o formato [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para saber mais, confira [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
- **Reporting Services:** para a atualização de uma nova instalação, restaure as chaves de criptografia do Reporting Services. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
- **Master Data Services:** faça upgrade do esquema de banco de dados do MDS e crie o aplicativo Web do SQL Server 2017. Para saber mais, confira [Upgrade Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md).  
  
- **Data Quality Services:** atualize o esquema de bancos de dados do DQS e verifique a atualização do esquema de bancos de dados do DQS. Para saber mais, confira [Upgrade Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md).  
  
- **Pesquisa de Texto Completo:** popule novamente catálogos de texto completo para garantir a consistência semântica em resultados da consulta. Para obter mais informações, veja [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
