---
title: Concluir o upgrade do mecanismo de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.technology: install
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 4fe57da44076bd33c585d4ab9986cf373e311f8e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794992"
---
# <a name="complete-the-database-engine-upgrade"></a>Concluir a atualização do mecanismo de banco de dados

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Após a conclusão do upgrade do SQL Server, há uma série de etapas adicionais que talvez precisem ser realizadas. Entre elas estão as seguintes:  
  
Depois de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], conclua as seguintes tarefas:  
  
- **Fazer backup de seus bancos de dados:** realize um backup completo de cada banco de dados.  

- **Habilitar novos recursos:** no SQL Server 2016 e SQL Server 2017, algumas alterações são habilitadas somente quando o nível de DATABASE_COMPATIBILITY de um banco de dados é alterado para 130 ou superior.  Para obter mais informações e para ver o fluxo de trabalho recomendado, consulte [Alterar o modo de compatibilidade do banco de dados e usar o repositório de consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md). Se o banco de dados tiver tabelas com otimização de memória criadas no SQL Server 2014, examine [Estatísticas para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md).
  
- **Integration Services:**  
  
     Migre pacotes do Integration Services para o formato [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para saber mais, confira [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
- **Reporting Services:** para a atualização de uma nova instalação, restaure as chaves de criptografia do Reporting Services. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
- **Master Data Services:**  atualize do esquema de banco de dados do MDS e crie o aplicativo Web do SQL Server 2017. Para saber mais, confira [Upgrade Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md).  
  
- **Data Quality Services:** atualize o esquema de bancos de dados do DQS e verifique a atualização do esquema de bancos de dados do DQS. Para saber mais, confira [Upgrade Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md).  
  
- **Pesquisa de Texto Completo:** Preencha novamente catálogos de texto completo para garantir a consistência semântica em resultados da consulta. Para obter mais informações, veja [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
