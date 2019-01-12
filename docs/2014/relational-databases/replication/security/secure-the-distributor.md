---
title: Proteger o Distribuidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], Distributors
- Distributors [SQL Server replication], security
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1bb6f278b18381d1b3d3defdb53a7c40a6f673ad
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135496"
---
# <a name="secure-the-distributor"></a>Proteger o distribuidor
  Os agentes de replicação a seguir se conectam ao Distribuidor: o Agente de Leitor de Log, Agente de Instantâneo, Agente de Leitor de Fila, Agente de Distribuição e Agente de Mesclagem. É importante fornecer um logon adequado para cada um desses agentes e seguir o princípio de conceder o mínimo possível de direitos necessários e de proteger também o armazenamento de todas as senhas:  
  
-   Para obter mais informações sobre como gerenciar logons e senhas, consulte [Gerenciar logons e senhas na Replicação](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication).  
  
-   Para obter informações detalhadas sobre as permissões requeridas por cada agente, consulte [Replication Agent Security Model](replication-agent-security-model.md).  
  
 Além de gerenciar os logons e as senhas adequadamente, é importante entender a função do link **repl_distributor** do servidor remoto e a conta **distributor_admin** .  
  
## <a name="securing-the-connection-from-the-publisher-to-the-distributor"></a>Protegendo a conexão do Publicador com o Distribuidor  
 Para dar suporte à comunicação necessária quando os procedimentos administrativos armazenados são executados no Publicador e as informações são atualizadas no Distribuidor, a replicação configura automaticamente o servidor remoto **repl_distributor**. A entrada do servidor remoto **repl_distributor** é usada na comunicação com o banco de dados de distribuição, independentemente de o banco de dados estar incluído na instância do Publicador (um Distribuidor local) ou residir em uma instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (um Distribuidor remoto).  
  
 Quando o banco de dados de distribuição é incluído em uma instância local, uma senha aleatória é gerada e configurada automaticamente. Quando o banco de dados de distribuição estiver localizado em uma instância remota, o administrador configurará uma senha compartilhada durante a instalação do Publicador e do Distribuidor; essa senha, então, será usada para fornecer a autenticação do tráfego que atravessa o link **repl_distributor** .  
  
 O Distribuidor usa a entrada **repl_distributor** do servidor remoto para verificar se o servidor que efetua a chamada está configurado como um Publicador no Distribuidor, valida a senha fornecida pelo Publicador e valida que o procedimento armazenado seja um procedimento de replicação armazenado durante a execução.  
  
 A senha configurada para a entrada **repl_distributor** do servidor remoto durante a instalação é associada a um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], **distributor_admin**, que é adicionado à função de servidor fixa **sysadmin** no Distribuidor. O logon **distributor_admin** é usado pelos procedimentos de replicação armazenados na conexão com o Distribuidor.  
  
> [!NOTE]  
>  Não altere manualmente a senha para o **distributor_admin** . Use sempre o procedimento armazenado **sp_changedistributor_password** , ou as caixas de diálogo **Propriedades do Distribuidor** ou **Atualizar Senhas de Replicação** no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], pois as alterações de senhas serão então aplicadas automaticamente às publicações locais.  
  
## <a name="snapshot-folder-security"></a>Segurança da pasta de instantâneos  
 Certifique-se de que o compartilhamento de instantâneos tenha acesso de leitura para a conta sob a qual o Agente de Mesclagem (para replicação de mesclagem) ou o Agente de Distribuição (para replicação transacional ou de instantâneos) executa, e acesso de gravação concedido à conta sob a qual o Agente de Instantâneo executa. Para obter mais informações sobre a pasta de instantâneos, consulte [Proteger a pasta de instantâneos](secure-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar configurações de segurança de replicação](view-and-modify-replication-security-settings.md)   
 [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Segurança de replicação do SQL Server](view-and-modify-replication-security-settings.md)  
  
  
