---
title: Requisitos da função de segurança para replicação | Microsoft Docs
description: Saiba mais sobre o nível de autenticação necessário para tarefas comuns de configuração de replicação e para tarefas comuns de manutenção de replicação no SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], roles
- roles [SQL Server], replication
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 85c71b94355aa845dcc15903552bbf77b6e8b206
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914319"
---
# <a name="security-role-requirements-for-replication"></a>Security Role Requirements for Replication
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  A replicação restringe as ações específicas que um usuário pode executar, baseada nas funções que o logon do usuário é mapeado. A replicação concede determinadas permissões para os membros da função de servidor fixa **sysadmin** , função de banco de dados fixa, **db_owner** e os logons na PAL (Publication Access List).  
  
## <a name="security-role-requirements-for-replication-setup"></a>Requisitos da função de segurança para a instalação de replicação  
 A tabela a seguir resume o nível de autenticação necessário para as tarefas de instalação de replicação comuns:  
  
|Tarefa de instalação|Requisito de associação|  
|----------------|----------------------------|  
|Habilite um Distribuidor, um Publicador ou um Assinante.|Função de servidor**sysadmin** no Publicador.|  
|Habilite um banco de dados para a replicação.|Função de servidor**sysadmin** no Publicador.|  
|Crie uma publicação.|Função de banco de dados**db_owner** no banco de dados de publicação do Publicador ou função de servidor **sysadmin** no Publicador.|  
|Exiba as propriedades de publicação.|Membro da PAL no Publicador, função de banco de dados **db_owner** no banco de dados de publicação do Publicador ou função de servidor **sysadmin** no Publicador.|  
|Criar uma assinatura.|Função de banco de dados**db_owner** no banco de dados de publicação do Publicador ou função de servidor **sysadmin** no Publicador.<br /><br /> Função de banco de dados**db_owner** no banco de dados de assinatura do Assinante ou função de servidor **sysadmin** no Assinante.|  
|Configure os perfis de agente.|Função de servidor**sysadmin** no Distribuidor.|  
  
## <a name="security-role-requirements-for-replication-maintenance"></a>Requisitos da função de segurança para a instalação de manutenção  
 A tabela a seguir resume o nível de autenticação necessário para as tarefas de manutenção de replicação comuns:  
  
|Tarefa de manutenção|Requisito de associação|  
|----------------------|----------------------------|  
|Modifique ou descarte um Distribuidor, Publicador ou Assinante.|Função de servidor**sysadmin** no servidor apropriado.|  
|Modifique ou descarte uma publicação.|Função de banco de dados**db_owner** no banco de dados de publicação do Publicador ou função de servidor **sysadmin** no Publicador.|  
|Modifique ou descarte uma assinatura no Publicador.|Função de banco de dados**db_owner** no banco de dados de publicação do Publicador ou função de servidor **sysadmin** no Publicador.|  
|Modifique ou descarte uma assinatura no Assinante.|Função de banco de dados**db_owner** no banco de dados de assinatura do Assinante ou função de servidor **sysadmin** no Assinante.|  
|Marque uma assinatura para reinicialização.|Assinatura push: função de banco de dados **db_owner** no banco de dados de publicação do Publicador ou função de servidor **sysadmin** no Publicador.<br /><br /> Assinatura pull: função de banco de dados **db_owner** no banco de dados de assinatura do Assinante ou função de servidor **sysadmin** no Assinante.|  
|Exiba a atividade, os erros e o histórico de replicação que usam o Replication Monitor. Um usuário não pode modificar perfis de agente, agendas, e assim por diante, exceto se o usuário for um membro da função de servidor **sysadmin** .|Função de banco de dados**replmonitor** no banco de dados de distribuição do Distribuidor ou função de servidor **sysadmin** no Distribuidor.|  
|Mantenha os agentes de replicação.|Função de banco de dados**db_owner** no banco de dados apropriado ou função de servidor **sysadmin** no servidor apropriado.<br /><br /> Se o agente foi criado pelo usuário na função **sysadmin** , e uma conta proxy não foi especificada para o agente, o agente executa em um contexto de conta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. Nesse caso, um usuário na função **db_owner** não pode modificar o trabalho associado ao agente.|  
|Inicie ou pare um agente de replicação.|Proprietário do trabalho de agente ou função de servidor **sysadmin** no servidor apropriado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Exibir e modificar configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
