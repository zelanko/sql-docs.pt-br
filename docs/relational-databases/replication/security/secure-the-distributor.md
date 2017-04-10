---
title: "Proteger o distribuidor | Microsoft Docs"
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
  - "segurança [replicação do SQL Server], Distribuidores"
  - "Distribuidores [replicação do SQL Server], segurança"
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Proteger o distribuidor
  Os agentes de replicação a seguir se conectam ao Distribuidor: o Agente de Leitor de Log, Agente de Instantâneo, Agente de Leitor de Fila, Agente de Distribuição e Agente de Mesclagem. É importante fornecer um logon adequado para cada um desses agentes e seguir o princípio de conceder o mínimo possível de direitos necessários e de proteger também o armazenamento de todas as senhas:  
  
-   Para obter informações sobre como gerenciar logons e senhas, consulte [Gerenciar logons e senhas na replicação](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Para obter informações detalhadas sobre as permissões necessárias para cada agente, consulte [modelo de segurança do agente de replicação](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Além de gerenciar adequadamente logons e senhas, é importante entender a função do **repl_distributor** link de servidor remoto e o **distributor_admin** conta.  
  
## Protegendo a conexão do Publicador com o Distribuidor  
 Para dar suporte à comunicação necessária quando os procedimentos administrativos armazenados são executados no publicador e atualizar as informações no distribuidor, replicação configura automaticamente o servidor remoto **repl_distributor**. O **repl_distributor** entrada do servidor remoto é usada para comunicação com o banco de dados de distribuição, independentemente do banco de dados de distribuição está contido dentro da instância do publicador (um distribuidor local) ou reside em um controle remoto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância (um distribuidor remoto).  
  
 Quando o banco de dados de distribuição é incluído em uma instância local, uma senha aleatória é gerada e configurada automaticamente. Quando o banco de dados de distribuição estiver localizado em uma instância remota, o administrador configura uma senha compartilhada durante a instalação do publicador e distribuidor; Essa senha, em seguida, é usada para fornecer autenticação do tráfego que atravessa o **repl_distributor** link.  
  
 O distribuidor usa o **repl_distributor** entrada do servidor remoto para verificar se o servidor de chamada está configurado como um editor no distribuidor, valida a senha fornecida pelo editor e valida que o procedimento armazenado é uma replicação de procedimento armazenado durante a execução.  
  
 A senha configurada para o **repl_distributor** entrada do servidor remoto durante a instalação está associada a um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] login, **distributor_admin**, que é adicionado ao **sysadmin** a função de servidor fixa no distribuidor. O **distributor_admin** logon é usado por procedimentos armazenados de replicação ao conectar-se ao distribuidor.  
  
> [!NOTE]  
>  Não altere a senha para o **distributor_admin** manualmente. Sempre use o **sp_changedistributor_password** procedimento armazenado, ou o **Propriedades do distribuidor** ou **Atualizar senhas de replicação** caixas de diálogo do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], porque as alterações de senha são então aplicados a local publicações automaticamente.  
  
## Segurança da pasta de instantâneos  
 Certifique-se de que o compartilhamento de instantâneos tenha acesso de leitura para a conta sob a qual o Agente de Mesclagem (para replicação de mesclagem) ou o Agente de Distribuição (para replicação transacional ou de instantâneos) executa, e acesso de gravação concedido à conta sob a qual o Agente de Instantâneo executa. Para obter mais informações sobre a pasta de instantâneo, consulte [proteger a pasta de instantâneo](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
## Consulte também  
 [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção e 40; Replicação e 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  