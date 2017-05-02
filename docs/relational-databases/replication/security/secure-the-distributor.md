---
title: Proteger o Distribuidor | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [SQL Server replication], Distributors
- Distributors [SQL Server replication], security
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0455938e9a9b0c017da7f8546821a9f318a85d6b
ms.lasthandoff: 04/11/2017

---
# <a name="secure-the-distributor"></a>Proteger o distribuidor
  Os agentes de replicação a seguir se conectam ao Distribuidor: o Agente de Leitor de Log, Agente de Instantâneo, Agente de Leitor de Fila, Agente de Distribuição e Agente de Mesclagem. É importante fornecer um logon adequado para cada um desses agentes e seguir o princípio de conceder o mínimo possível de direitos necessários e de proteger também o armazenamento de todas as senhas:  
  
-   Para obter mais informações sobre como gerenciar logons e senhas, consulte [Gerenciar logons e senhas na Replicação](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Para obter informações detalhadas sobre as permissões requeridas por cada agente, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Além de gerenciar os logons e as senhas adequadamente, é importante entender a função do link **repl_distributor** do servidor remoto e a conta **distributor_admin** .  
  
## <a name="securing-the-connection-from-the-publisher-to-the-distributor"></a>Protegendo a conexão do Publicador com o Distribuidor  
 Para dar suporte à comunicação necessária quando os procedimentos administrativos armazenados são executados no Publicador e as informações são atualizadas no Distribuidor, a replicação configura automaticamente o servidor remoto **repl_distributor**. A entrada do servidor remoto **repl_distributor** é usada na comunicação com o banco de dados de distribuição, independentemente de o banco de dados estar incluído na instância do Publicador (um Distribuidor local) ou residir em uma instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (um Distribuidor remoto).  
  
 Quando o banco de dados de distribuição é incluído em uma instância local, uma senha aleatória é gerada e configurada automaticamente. Quando o banco de dados de distribuição estiver localizado em uma instância remota, o administrador configurará uma senha compartilhada durante a instalação do Publicador e do Distribuidor; essa senha, então, será usada para fornecer a autenticação do tráfego que atravessa o link **repl_distributor** .  
  
 O Distribuidor usa a entrada **repl_distributor** do servidor remoto para verificar se o servidor que efetua a chamada está configurado como um Publicador no Distribuidor, valida a senha fornecida pelo Publicador e valida que o procedimento armazenado seja um procedimento de replicação armazenado durante a execução.  
  
 A senha configurada para a entrada **repl_distributor** do servidor remoto durante a instalação é associada a um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], **distributor_admin**, que é adicionado à função de servidor fixa **sysadmin** no Distribuidor. O logon **distributor_admin** é usado pelos procedimentos de replicação armazenados na conexão com o Distribuidor.  
  
> [!NOTE]  
>  Não altere manualmente a senha para o **distributor_admin** . Use sempre o procedimento armazenado **sp_changedistributor_password** , ou as caixas de diálogo **Propriedades do Distribuidor** ou **Atualizar Senhas de Replicação** no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], pois as alterações de senhas serão então aplicadas automaticamente às publicações locais.  
  
## <a name="snapshot-folder-security"></a>Segurança da pasta de instantâneos  
 Certifique-se de que o compartilhamento de instantâneos tenha acesso de leitura para a conta sob a qual o Agente de Mesclagem (para replicação de mesclagem) ou o Agente de Distribuição (para replicação transacional ou de instantâneos) executa, e acesso de gravação concedido à conta sob a qual o Agente de Instantâneo executa. Para obter mais informações sobre a pasta de instantâneos, consulte [Proteger a pasta de instantâneos](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção &#40;Replicação&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
