---
title: "Requisitos da fun&#231;&#227;o de seguran&#231;a para replica&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "segurança [replicação do SQL Server], funções"
  - "funções [replicação do SQL Server], replicação"
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Requisitos da fun&#231;&#227;o de seguran&#231;a para replica&#231;&#227;o
  A replicação restringe as ações específicas que um usuário pode executar, baseada nas funções que o logon do usuário é mapeado. Replicação concedeu permissões específicas para o **sysadmin** função de servidor fixa, o **db_owner** fixa de funções de banco de dados e os logons na lista de acesso da publicação (PAL).  
  
## Requisitos da função de segurança para a instalação de replicação  
 A tabela a seguir resume o nível de autenticação necessário para as tarefas de instalação de replicação comuns:  
  
|Tarefa de instalação|Requisito de associação|  
|----------------|----------------------------|  
|Habilite um Distribuidor, um Publicador ou um Assinante.|Função de servidor**sysadmin** no Publicador.|  
|Habilite um banco de dados para a replicação.|Função de servidor**sysadmin** no Publicador.|  
|Crie uma publicação.|**db_owner** função de banco de dados do banco de dados de publicação no publicador ou **sysadmin** a função de servidor no Editor.|  
|Exiba as propriedades de publicação.|Membro da PAL no publicador, **db_owner** função de banco de dados do banco de dados de publicação no publicador, ou **sysadmin** a função de servidor no Editor.|  
|Criar uma assinatura.|**db_owner** função de banco de dados do banco de dados de publicação no publicador ou **sysadmin** a função de servidor no Editor.<br /><br /> **db_owner** função de banco de dados do banco de dados no assinante ou **sysadmin** a função de servidor no assinante.|  
|Configure os perfis de agente.|Função de servidor**sysadmin** no Distribuidor.|  
  
## Requisitos da função de segurança para a instalação de manutenção  
 A tabela a seguir resume o nível de autenticação necessário para as tarefas de manutenção de replicação comuns:  
  
|Tarefa de manutenção|Requisito de associação|  
|----------------------|----------------------------|  
|Modifique ou descarte um Distribuidor, Publicador ou Assinante.|Função de servidor**sysadmin** no servidor apropriado.|  
|Modifique ou descarte uma publicação.|**db_owner** função de banco de dados do banco de dados de publicação no publicador ou **sysadmin** a função de servidor no Editor.|  
|Modifique ou descarte uma assinatura no Publicador.|**db_owner** função de banco de dados do banco de dados de publicação no publicador ou **sysadmin** a função de servidor no Editor.|  
|Modifique ou descarte uma assinatura no Assinante.|**db_owner** função de banco de dados do banco de dados no assinante ou **sysadmin** a função de servidor no assinante.|  
|Marque uma assinatura para reinicialização.|Assinatura Push: **db_owner** função de banco de dados no banco de dados de publicação no publicador ou **sysadmin** a função de servidor no Editor.<br /><br /> Assinatura Pull: **db_owner** função de banco de dados no banco de dados de assinatura no assinante ou **sysadmin** a função de servidor no assinante.|  
|Exiba a atividade, os erros e o histórico de replicação que usam o Replication Monitor. Um usuário não pode modificar perfis de agente, agendas, e assim por diante, exceto se o usuário for um membro da função de servidor **sysadmin** .|Função de banco de dados**replmonitor** no banco de dados de distribuição do Distribuidor ou função de servidor **sysadmin** no Distribuidor.|  
|Mantenha os agentes de replicação.|**db_owner** função de banco de dados no banco de dados apropriado ou **sysadmin** a função de servidor no servidor apropriado.<br /><br /> Se o agente foi criado pelo usuário na função **sysadmin** , e uma conta proxy não foi especificada para o agente, o agente executa em um contexto de conta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. Nesse caso, um usuário na **db_owner** função não é possível modificar o trabalho associado ao agente.|  
|Inicie ou pare um agente de replicação.|Proprietário do trabalho de agente ou função de servidor **sysadmin** no servidor apropriado.|  
  
## Consulte também  
 [Práticas recomendadas em relação à segurança de replicação](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção e 40; Replicação e 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  