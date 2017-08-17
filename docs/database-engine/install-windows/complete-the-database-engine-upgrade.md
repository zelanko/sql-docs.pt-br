---
title: Concluir o upgrade do mecanismo de banco de dados | Microsoft Docs
ms.custom: 
ms.date: 07/21/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 581e8cd7a43dd1e4c878cc56b49644e51d7a3a79
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="complete-the-database-engine-upgrade"></a>Concluir a atualização do mecanismo de banco de dados

Após a conclusão do upgrade do SQL Server, há uma série de etapas adicionais que talvez precisem ser realizadas. Entre elas estão as seguintes:  
  
Depois de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], conclua as seguintes tarefas:  
  
- **Fazer backup dos bancos de dados:** faça um backup completo de cada banco de dados.  

- **Habilitar novos recursos:** no SQL Server 2016 e SQL Server 2017, algumas alterações são habilitadas somente quando o nível de DATABASE_COMPATIBILITY de um banco de dados é alterado para 130 ou superior.  Para obter mais informações e para ver o fluxo de trabalho recomendado, consulte [Alterar o modo de compatibilidade do banco de dados e usar o repositório de consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md).  
  
- **Integration Services:**  
  
     Migre pacotes do Integration Services para o formato [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para saber mais, confira [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
- **Reporting Services:** para a atualização de uma nova instalação, restaure as chaves de criptografia do Reporting Services. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
- **Master Data Services:** faça upgrade do esquema de banco de dados do MDS e crie o aplicativo Web do SQL Server 2017. Para saber mais, confira [Upgrade Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md).  
  
- **Data Quality Services:** atualize o esquema de bancos de dados do DQS e verifique a atualização do esquema de bancos de dados do DQS. Para saber mais, confira [Upgrade Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md).  
  
- **Pesquisa de Texto Completo:** popule novamente catálogos de texto completo para garantir a consistência semântica em resultados da consulta. Para obter mais informações, veja [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  

