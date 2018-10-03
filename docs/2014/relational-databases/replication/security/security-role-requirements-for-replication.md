---
title: Requisitos da função de segurança para replicação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], roles
- roles [SQL Server], replication
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c57fa5ea252aa66e14628d49529970ceab7eb64
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48146406"
---
# <a name="security-role-requirements-for-replication"></a>Security Role Requirements for Replication
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
  
## <a name="see-also"></a>Consulte também  
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Segurança e proteção &#40;Replicação&#41;](security-and-protection-replication.md)  
  
  
