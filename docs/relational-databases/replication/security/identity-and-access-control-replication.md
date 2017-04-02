---
title: "Identidade e controle de acesso (Replica&#231;&#227;o) | Microsoft Docs"
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
  - "controles de acesso [replicação do SQL Server]"
  - "segurança [replicação do SQL Server], controle de acesso e identidades"
  - "autenticação [replicação do SQL Server]"
  - "identidade [Replicação]"
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# Identidade e controle de acesso (Replica&#231;&#227;o)
  Autenticação é o processo pelo qual uma entidade (geralmente um computador neste contexto) verifica se outra entidade, também chamada de um *principal*, (geralmente um outro computador ou usuário) é quem ou o que afirma ser. A autorização é o processo pelo qual um principal autenticado obtém acesso aos recursos, como um arquivo no sistema de arquivos ou  uma tabela no banco de dados.  
  
 A segurança de replicação usa a autenticação e a autorização para controlar o acesso aos objetos de banco de dados replicados e aos computadores e agentes envolvidos no processamento de replicação. Isso é realizado por meio de três mecanismos:  
  
-   Segurança do agente  
  
     O modelo de segurança do agente de replicação permite um controle refinado das contas nas quais os agentes de replicação executam e efetuam conexões. Para obter informações detalhadas sobre o modelo de segurança do agente, consulte [modelo de segurança do agente de replicação](../../../relational-databases/replication/security/replication-agent-security-model.md). Para obter informações sobre como definir logons e senhas para agentes, consulte [Gerenciar logons e senhas na replicação](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Funções de administração  
  
     Certifique-se de que  o servidor e as funções do banco de dados corretos sejam usados na configuração, manutenção e processamento da replicação. Para obter mais informações, consulte [requisitos da função de segurança para replicação](../../../relational-databases/replication/security/security-role-requirements-for-replication.md).  
  
-   A lista de acesso à publicação (PAL)  
  
     Conceda acesso a publicações por meio da PAL. A PAL funciona de modo semelhante à lista de controle de acesso do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Quando um Assinante se conecta ao Publicador ou ao Distribuidor e solicita acesso à publicação, as informações de autenticação passadas pelo agente são verificadas de acordo com a PAL. Para obter mais informações e práticas recomendadas para a PAL, consulte [proteger o publicador](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
## Filtrando dados publicados  
 Além de usar a autenticação e a autorização para controlar o acesso aos dados e objetos replicados, a replicação inclui duas opções para controlar quais dados estão disponíveis no Assinante: a filtragem de colunas e a filtragem de linhas. Para obter mais informações sobre filtragem, consulte [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
 Ao definir um artigo, você pode publicar apenas as colunas que são necessárias para a publicação e omitir as desnecessárias ou aquelas que contêm dados confidenciais. Por exemplo, ao publicar o **cliente** tabela do banco de dados Adventure Works para representantes de vendas no campo, você pode omitir o **AnnualSales** coluna, que pode ser relevante apenas para os executivos da empresa.  
  
 A filtragem de dados publicados restringe o acesso aos dados e permite que você especifique os dados disponíveis no Assistente. Por exemplo, você pode filtrar o **cliente** tabela para que parceiros da corporação recebam apenas as informações sobre os clientes cujo **ShareInfo** coluna tiver um valor de "Sim". Para a replicação de mesclagem, haverá considerações de segurança se você usar um filtro com parâmetros que inclua HOST_NAME(). Para obter mais informações, consulte a seção "Filtragem com HOST_NAME ()" em [filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
## Consulte também  
 [Segurança e proteção e 40; Replicação e 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Visão geral de segurança e 40; Replicação e 41;](../../../relational-databases/replication/security/security-overview-replication.md)   
 [Ameaça e mitigação de vulnerabilidade e 40; Replicação e 41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md)  
  
  