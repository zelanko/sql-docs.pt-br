---
title: "Práticas recomendadas de segurança de replicação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [SQL Server replication], best practices
- security [SQL Server replication], between domains
- authentication [SQL Server replication]
- Internet [SQL Server replication], security
ms.assetid: 1ab2635d-0992-4c99-b17d-041d02ec9a7c
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 367496f0a4501277a4879464cea31bd1a1c96436
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="replication-security-best-practices"></a>Práticas recomendadas em relação à segurança de replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A replicação move dados em ambientes distribuídos variando deste intranets em um único domínio até aplicativos que acessam dados entre domínios não confiáveis e na internet. É importante para entender a melhor abordagem para proteger as conexões de replicação sob essas diversas circunstâncias.  
  
 As informações abaixo são relevantes para a replicação em todos os ambientes:  
  
-   Criptografar as conexão entre computadores é uma topologia de replicação que usa um método padrão da indústria, como VPN (Virtual Private Networks), SSL (Secure Sockets Layer) ou IPSEC (IP Security). Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md). Para obter informações sobre como usar VPN e SSL para replicar dados na Internet, consulte [Securing Replication Over the Internet](../../../relational-databases/replication/security/securing-replication-over-the-internet.md).  
  
     Se você usar SSL para proteger as conexões entre computadores em uma topologia de replicação, especifique um valor de **1** ou **2** para o parâmetro **-EncryptionLevel** de cada agente de replicação (um valor de **2** é recomendado). Um valor de **1** especifica que é usada criptografia, porém o agente não verifica se o certificado do servidor SSL está assinado por um emissor confiável; um valor **2** especifica que o certificado é verificado. Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
    -   [Trabalhar com perfis do Agente de Replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Exibir e modificar parâmetros do prompt de comando do agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   Execute cada agente de replicação em uma conta diferente do Windows e use a Autenticação do Windows para todas as conexões de agente de replicação. Para obter mais informações sobre como especificar contas, consulte [Gerenciar logons e senhas na replicação](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Conceda somente as permissões exigidas para cada agente. Para obter mais informações, consulte a seção "Permissões necessárias para agentes" em [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Certifique-se de que todas as contas Agente de Mesclagem e Agente de Distribuição estão na lista de acesso à publicação (PAL). Para obter mais informações, consulte [Secure the Publisher](../../../relational-databases/replication/security/secure-the-publisher.md) (Proteger o publicador).  
  
-   Siga o princípio de menos privilégios concedendo às contas na PAL somente as permissões que necessitam para executar tarefas de replicação. Não adicione os logons a qualquer função de servidor fixa que não seja necessária para replicação.  
  
-   Configure o compartilhamento de instantâneo para permitir acesso de leitura a todos os Agente de Mesclagems e Agente de Distribuiçãos. No caso de instantâneos para publicação com filtros com parâmetros, assegure que cada pasta está configurada para permitir acesso somente às contas do Agente de Mesclagem adequadas.  
  
-   Configure o compartilhamento de instantâneo para permitir acesso de gravação pelo Agente de Instantâneo.  
  
-   Se você usar assinaturas pull, use um compartilhamento de rede ao invés de um caminho local para a pasta de instantâneo.  
  
 Se a sua topologia de replicação incluir computadores que não estejam no mesmo domínio ou que estejam em domínios que não possuam relação segura um com o outro, você poderá usar a Autenticação do Windows ou a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para as conexões feitas por agentes (para obter mais informações sobre domínios, consulte a documentação do Windows). Sugerimos como prática recomendada de segurança que você use a Autenticação do Windows.  
  
-   Para usar a Autenticação do Windows:  
  
    -   Adicione uma conta local do Windows (não uma conta de domínio) para cada agente nos nós adequados (use o mesmo nome e senha em cada nó). Por exemplo, o Agente de Distribuição para uma assinatura push executa no Distribuidor e faz conexões para o Distribuidor e para o Assinante. A conta do Windows para o Agente de Distribuição deve ser adicionada ao Distribuidor e ao Assinante.  
  
    -   Certifique-se que um determinado agente (por exemplo, o Agente de Distribuição para uma assinatura) é executado na mesma conta em cada computador.  
  
-   Para usar a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
    -   Adicione uma conta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para cada agente nos nós adequados (use o mesmo nome e senha em cada nó). Por exemplo, o Agente de Distribuição para uma assinatura push executa no Distribuidor e faz conexões para o Distribuidor e para o Assinante. A conta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o Agente de Distribuição deve ser adicionada ao Distribuidor e ao Assinante.  
  
    -   Certifique-se que um determinado agente (por exemplo, o Agente de Distribuição para uma assinatura) faz conexões na mesma conta em cada computador.  
  
    -   Quando for necessária a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , normalmente o acesso ao compartilhamento de instantâneo UNC não estará disponível (por exemplo, o acesso poderá ser bloqueado por um firewall). Neste caso, você pode transferir o instantâneo aos Assinantes por FTP (File Transfer Protocol). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replicação na Internet](../../../relational-databases/replication/replication-over-the-internet.md)   
 [Proteger o Assinante](../../../relational-databases/replication/security/secure-the-subscriber.md)   
 [Proteger o Distribuidor](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [Proteger o Publicador](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [Segurança e proteção &#40;Replicação&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
