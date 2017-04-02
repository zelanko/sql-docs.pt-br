---
title: "A&#231;&#245;es comuns que requerem um backup atualizado | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "recuperação [replicação do SQL Server], ações que requerem um backup"
  - "restauração [replicação do SQL Server], ações que requerem um backup"
  - "backups [replicação do SQL Server], ações que requerem um backup"
ms.assetid: a5975bf4-183e-42e3-b7d1-ad02f89d2e1d
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# A&#231;&#245;es comuns que requerem um backup atualizado
  Se você executar backups de log regulares, qualquer alteração relacionada à replicação deverá ser capturada nos backups de log. Se você não executar backups de log, execute um backup da publicação, distribuição, assinatura, **msdb**, e **mestre** bancos de dados após fazer alterações ao seu esquema de replicação ou a topologia.  
  
## Banco de dados de publicação  
 Faça o backup do banco de dados de publicação após:  
  
-   Criar novas publicações.  
  
-   Alterar qualquer propriedade de publicação, inclusive filtragem.  
  
-   Adicionar artigos a uma publicação existente.  
  
-   Executar uma reinicialização de publicação abrangente de assinaturas.  
  
-   Fazer uma alteração de esquema em uma tabela publicada.  
  
-   Execução de script sob demanda com [sp_addscriptexec & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md).  
  
-   Alterar qualquer propriedade de artigo.  
  
-   Descartar qualquer publicação.  
  
-   Descartar qualquer artigo.  
  
-   Desabilitar a replicação.  
  
## Banco de dados de distribuição  
 Faça o backup do banco de dados de distribuição após:  
  
-   Criar ou modificar perfis de agente de replicação.  
  
-   Modificar parâmetros de perfil do agente de replicação.  
  
-   Alterar as propriedades do agente de replicação (inclusive agendas) para qualquer assinatura push.  
  
-   Um novo intervalo de identidades é atribuído pelo recurso de gerenciamento automático de intervalo de identidade.  
  
## Banco de dados de assinatura  
 Faça o backup do banco de dados de assinatura após:  
  
-   Alterar qualquer propriedade de assinatura.  
  
-   Alterar a prioridade para uma assinatura de mesclagem no Publicador.  
  
-   Descartar qualquer assinatura.  
  
-   Desabilitar a replicação.  
  
## Banco de dados msdb  
 Backup de **msdb** banco de dados do sistema no nó apropriado após:  
  
-   Habilitar ou desabilitar a replicação.  
  
-   Adicionar ou descartar um banco de dados de distribuição (no Distribuidor).  
  
-   Habilitar ou desabilitar um banco de dados para publicação (no Publicador).  
  
-   Criar ou modificar perfis de agente de replicação (no Distribuidor).  
  
-   Modificar qualquer parâmetro de perfil do agente de replicação (no Distribuidor).  
  
-   Alterar as propriedades do agente de replicação (inclusive agendas) para qualquer assinatura push (no Distribuidor).  
  
-   Alterar as propriedades do agente de replicação (inclusive agendas) para qualquer assinatura pull (no Distribuidor).  
  
-   Criar um pacote DTS associado com uma publicação transacional que usa assinatura transformáveis (no Distribuidor e no Assinante).  
  
-   Adicionar ou descartar uma assinatura transformável (no Distribuidor e no Assinante)).  
  
## Banco de dados mestre  
 Backup de **mestre** banco de dados do sistema no nó apropriado após:  
  
-   Habilitar ou desabilitar a replicação.  
  
-   Adicionar ou descartar um banco de dados de distribuição (no Distribuidor).  
  
-   Habilitar ou desabilitar um banco de dados para publicação (no Publicador).  
  
-   Adicionar a primeira ou descartar a última publicação em qualquer banco de dados (no Publicador).  
  
-   Adicionar a primeira ou descartar a última assinatura em qualquer banco de dados (no Assinante).  
  
-   Habilitar ou desabilitar um Publicador em um Publicador de Distribuição (no Publicador e no Distribuidor).  
  
## Consulte também  
 [Fazer backup e restaurar bancos de dados do SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  