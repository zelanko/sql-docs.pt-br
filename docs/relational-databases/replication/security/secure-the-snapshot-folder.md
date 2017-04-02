---
title: "Proteger uma pasta de instant&#226;neo | Microsoft Docs"
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
  - "instantâneos [replicação do SQL Server], segurança"
ms.assetid: 3cd877d1-ffb8-48fd-a72b-98eb948aad27
caps.latest.revision: 46
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# Proteger uma pasta de instant&#226;neo
  A pasta de instantâneo é um diretório que armazena arquivos de instantâneos, recomendamos que você dedique o diretório para o armazenamento de instantâneos. Conceda permissão de gravação ao Agente de Instantâneo para a pasta e assegure que a permissão de leitura seja fornecida somente para a conta do Windows usada pelo Agente de Distribuição ou Agente de Mesclagem para acessar a pasta. A conta do Windows associada com o agente deve ser uma conta de domínio para acessar uma pasta de instantâneo que está localiza em um computador remoto.  
  
> [!NOTE]  
>  Controle de conta de usuário (UAC) ajuda os administradores a gerenciar seus direitos de usuário elevados (algumas vezes chamado *privilégios*). Ao ser executado em sistemas operacionais com UAC habilitado, os administradores não usam seus direitos administrativos. Em vez disso, eles executam a maioria das ações como usuários padrão (não administrativos), assumindo temporariamente seus direitos administrativos somente quando necessário. O UAC pode impedir o acesso administrativo ao compartilhamento de instantâneos. Portanto, você deve conceder permissões de compartilhamento de instantâneos explicitamente às contas do Windows usadas pelo Agente de Instantâneo, pelo Agente de Distribuição, e pelo Agente de Mesclagem. Faça isso, mesmo se as contas do Windows forem membros do grupo de Administradores.  
  
 Ao configurar um distribuidor por meio do Assistente para configurar distribuição ou o Assistente para nova publicação, a pasta de instantâneo padrão de um caminho local: X:\Program Files\Microsoft SQL Server\\*\< instância>*\mssql\repldata.. Se você estiver usando um distribuidor remoto ou assinaturas pull, você deve especificar um compartilhamento de rede UNC (como \\\\<*computername >*\snapshot) em vez de um caminho local.  
  
 Ao fornecer permissões de acesso para a pasta de instantâneos, você deve fornecê-las de acordo com o modo como a pasta é acessada. As guias de caixa de diálogo abaixo são usadas no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2003:  
  
-   Se você especificar um caminho local, conceda permissões por meio de **segurança** Guia do **propriedades** caixa de diálogo para a pasta.  
  
-   Se você especificar um compartilhamento de rede, conceder permissões por meio de **compartilhamento** Guia do **propriedades** caixa de diálogo para a pasta.  
  
    > [!NOTE]  
    >  Se o agente de replicação é executado no distribuidor, use o **segurança** guia o **propriedades** caixa de diálogo para a pasta para conceder permissões para a conta do Windows usada para executar o agente. Faça isso até mesmo quando for usado um compartilhamento de rede. Isso se aplica ao Agente de Distribuição e ao Agente de Mesclagem para uma assinatura push e ao Agente de Instantâneo quando o Publicador e o Distribuidor estiverem no mesmo computador.  
  
 Para obter mais informações sobre como configurar permissões para caminhos locais e compartilhamentos de rede, consulte a documentação do Windows.  
  
> [!NOTE]  
>  Se uma publicação for cancelada, a replicação tentará remover a pasta de instantâneo no contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Caso esta conta não tenha privilégios suficientes, faça logon com uma conta que possua privilégios suficientes e remova a pasta manualmente. Requer a remoção de uma pasta de **modificar** privilégio se a pasta é um caminho local ou o **controle total** privilégio se a pasta é um caminho de rede.  
  
## Entregando instantâneos por FTP  
 Sugerimos como prática recomendada que os instantâneos sejam armazenados em um compartilhamento UNC, porém os instantâneos podem ser armazenados em um compartilhamento FTP e então enviados a um Assinante via FTP. Ao configurar o servidor FTP, assegure que o diretório virtual expõe um compartilhamento UNC subjacente que permite o acesso de gravação pelo Agente de Instantâneo para a publicação.  
  
 Para configurar um Assinante para recuperar o Instantâneo via FTP, defina primeiro um servidor FTP com um logon e senha que permita aos Assinantes acesso de leitura (ou “obter”) para permitir que os arquivos dos instantâneos possam ser baixados.  
  
 Para entregar instantâneos por FTP, consulte [entregar um instantâneo por meio de FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
 Para obter informações sobre como definir e alterar a senha para acesso a instantâneos via FTP, consulte a seção "Entrega de instantâneo de FTP" no tópico [proteger o publicador](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
## Consulte também  
 [Locais da pasta de instantâneos alternativos](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Inicializar uma assinatura com um instantâneo](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção e 40; Replicação e 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Transferir instantâneos pelo FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)  
  
  