---
title: Proteger a pasta de instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], security
ms.assetid: 3cd877d1-ffb8-48fd-a72b-98eb948aad27
caps.latest.revision: 46
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2884a1cd4507775e75764d632dfab50185596949
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="secure-the-snapshot-folder"></a>Proteger uma pasta de instantâneo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A pasta de instantâneo é um diretório que armazena arquivos de instantâneos, recomendamos que você dedique o diretório para o armazenamento de instantâneos. Conceda permissão de gravação ao Agente de Instantâneo para a pasta e assegure que a permissão de leitura seja fornecida somente para a conta do Windows usada pelo Agente de Distribuição ou Agente de Mesclagem para acessar a pasta. A conta do Windows associada com o agente deve ser uma conta de domínio para acessar uma pasta de instantâneo que está localiza em um computador remoto.  
  
> [!NOTE]  
>  O UAC (Controle de Conta de Usuário) ajuda os administradores a gerenciar o uso de direitos do usuário elevados (algumas vezes chamados de *privilégios*). Ao ser executado em sistemas operacionais com UAC habilitado, os administradores não usam seus direitos administrativos. Em vez disso, eles executam a maioria das ações como usuários padrão (não administrativos), assumindo temporariamente seus direitos administrativos somente quando necessário. O UAC pode impedir o acesso administrativo ao compartilhamento de instantâneos. Portanto, você deve conceder permissões de compartilhamento de instantâneos explicitamente às contas do Windows usadas pelo Agente de Instantâneo, pelo Agente de Distribuição, e pelo Agente de Mesclagem. Faça isso, mesmo se as contas do Windows forem membros do grupo de Administradores.  
  
 Ao configurar um Distribuidor por meio do Assistente para Configurar a Distribuição ou o Assistente para Nova Publicação, a pasta de instantâneos fica, por padrão, no caminho local: X:\Arquivos de Programas\Microsoft SQL Server\\*\<instância>* \MSSQL\ReplData. Se estiver usando um Distribuidor remoto ou assinaturas pull, você deverá especificar um compartilhamento de rede UNC (como \\\\<*computername>* \snapshot) em vez de um caminho local.  
  
 Ao fornecer permissões de acesso para a pasta de instantâneos, você deve fornecê-las de acordo com o modo como a pasta é acessada. As guias de caixa de diálogo abaixo são usadas no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2003:  
  
-   Se você especificar um caminho local, forneça permissões para a pasta por meio da guia **Segurança** da caixa de diálogo **Propriedades** .  
  
-   Se você especificar um compartilhamento de rede, forneça permissões para a pasta por meio da guia **Compartilhamento** da caixa de diálogo **Propriedades** .  
  
    > [!NOTE]  
    >  Se o agente de replicação for executado no Distribuidor, use a guia **Segurança** da caixa de diálogo **Propriedades** da pasta para conceder permissões para a conta do Windows usada para executar o agente. Faça isso até mesmo quando for usado um compartilhamento de rede. Isso se aplica ao Agente de Distribuição e ao Agente de Mesclagem para uma assinatura push e ao Agente de Instantâneo quando o Publicador e o Distribuidor estiverem no mesmo computador.  
  
 Para obter mais informações sobre como configurar permissões para caminhos locais e compartilhamentos de rede, consulte a documentação do Windows.  
  
> [!NOTE]  
>  Se uma publicação for cancelada, a replicação tentará remover a pasta de instantâneo no contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Caso esta conta não tenha privilégios suficientes, faça logon com uma conta que possua privilégios suficientes e remova a pasta manualmente. A remoção de uma pasta exige o privilégio **Modificar** se a pasta estiver em um caminho local ou o privilégio **Controle Total** se a pasta estiver em um caminho de rede.  
  
## <a name="delivering-snapshots-through-ftp"></a>Entregando instantâneos por FTP  
 Sugerimos como prática recomendada que os instantâneos sejam armazenados em um compartilhamento UNC, porém os instantâneos podem ser armazenados em um compartilhamento FTP e então enviados a um Assinante via FTP. Ao configurar o servidor FTP, assegure que o diretório virtual expõe um compartilhamento UNC subjacente que permite o acesso de gravação pelo Agente de Instantâneo para a publicação.  
  
 Para configurar um Assinante para recuperar o Instantâneo via FTP, defina primeiro um servidor FTP com um logon e senha que permita aos Assinantes acesso de leitura (ou “obter”) para permitir que os arquivos dos instantâneos possam ser baixados.  
  
 Para entregar um instantâneo por FTP, consulte [Entregar um instantâneo por FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
 Para obter mais informações sobre a configuração e alteração de senha para acesso a instantâneos via FTP, consulte a seção "Entrega de instantâneo por FTP" neste tópico [Secure the Publisher](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Locais da pasta de instantâneos alternativos](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Inicializar uma assinatura com um instantâneo](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção &#40;Replicação&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Transferir instantâneos pelo FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)  
  
  
