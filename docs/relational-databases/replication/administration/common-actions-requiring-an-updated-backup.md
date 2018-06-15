---
title: Ações comuns que requerem um backup atualizado | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], actions requiring a backup
- restoring [SQL Server replication], actions requiring a backup
- backups [SQL Server replication], actions requiring a backup
ms.assetid: a5975bf4-183e-42e3-b7d1-ad02f89d2e1d
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70ce579ad6548d0fee933291fdb6c8f9b4e03f42
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32954121"
---
# <a name="common-actions-requiring-an-updated-backup"></a>Ações comuns que requerem um backup atualizado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se você executar backups de log regulares, qualquer alteração relacionada à replicação deverá ser capturada nos backups de log. Se não executar backups de log, faça um backup dos bancos de dados de publicação, distribuição, assinatura, **msdb**e **mestre** após fazer alterações ao seu esquema ou topologia de replicação.  
  
## <a name="publication-database"></a>Banco de dados de publicação  
 Faça o backup do banco de dados de publicação após:  
  
-   Criar novas publicações.  
  
-   Alterar qualquer propriedade de publicação, inclusive filtragem.  
  
-   Adicionar artigos a uma publicação existente.  
  
-   Executar uma reinicialização de publicação abrangente de assinaturas.  
  
-   Fazer uma alteração de esquema em uma tabela publicada.  
  
-   Executando um script sob demanda com [sp_addscriptexec &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md).  
  
-   Alterar qualquer propriedade de artigo.  
  
-   Descartar qualquer publicação.  
  
-   Descartar qualquer artigo.  
  
-   Desabilitar a replicação.  
  
## <a name="distribution-database"></a>Banco de dados de distribuição  
 Faça o backup do banco de dados de distribuição após:  
  
-   Criar ou modificar perfis de agente de replicação.  
  
-   Modificar parâmetros de perfil do agente de replicação.  
  
-   Alterar as propriedades do agente de replicação (inclusive agendas) para qualquer assinatura push.  
  
-   Um novo intervalo de identidades é atribuído pelo recurso de gerenciamento automático de intervalo de identidade.  
  
## <a name="subscription-database"></a>Banco de dados de assinatura  
 Faça o backup do banco de dados de assinatura após:  
  
-   Alterar qualquer propriedade de assinatura.  
  
-   Alterar a prioridade para uma assinatura de mesclagem no Publicador.  
  
-   Descartar qualquer assinatura.  
  
-   Desabilitar a replicação.  
  
## <a name="msdb-database"></a>Banco de dados msdb  
 Faça o backup do banco de dados de sistema **msdb** no nó apropriado após:  
  
-   Habilitar ou desabilitar a replicação.  
  
-   Adicionar ou descartar um banco de dados de distribuição (no Distribuidor).  
  
-   Habilitar ou desabilitar um banco de dados para publicação (no Publicador).  
  
-   Criar ou modificar perfis de agente de replicação (no Distribuidor).  
  
-   Modificar qualquer parâmetro de perfil do agente de replicação (no Distribuidor).  
  
-   Alterar as propriedades do agente de replicação (inclusive agendas) para qualquer assinatura push (no Distribuidor).  
  
-   Alterar as propriedades do agente de replicação (inclusive agendas) para qualquer assinatura pull (no Distribuidor).  
  
-   Criar um pacote DTS associado com uma publicação transacional que usa assinatura transformáveis (no Distribuidor e no Assinante).  
  
-   Adicionar ou descartar uma assinatura transformável (no Distribuidor e no Assinante)).  
  
## <a name="master-database"></a>Banco de dados mestre  
 Faça o backup do banco de dados de sistema **mestre** no nó apropriado após:  
  
-   Habilitar ou desabilitar a replicação.  
  
-   Adicionar ou descartar um banco de dados de distribuição (no Distribuidor).  
  
-   Habilitar ou desabilitar um banco de dados para publicação (no Publicador).  
  
-   Adicionar a primeira ou descartar a última publicação em qualquer banco de dados (no Publicador).  
  
-   Adicionar a primeira ou descartar a última assinatura em qualquer banco de dados (no Assinante).  
  
-   Habilitar ou desabilitar um Publicador em um Publicador de Distribuição (no Publicador e no Distribuidor).  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e Restauração de bancos de dados do SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  
