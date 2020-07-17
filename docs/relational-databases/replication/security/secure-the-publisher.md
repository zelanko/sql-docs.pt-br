---
title: Proteger o publicador | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- Publishers [SQL Server replication], security
- publications [SQL Server replication], security
ms.assetid: 4513a18d-dd6e-407a-b009-49dc9432ec7e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: f6f3b56ec2a45420e56add4d3e746bcca5fb6eba
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86159494"
---
# <a name="secure-the-publisher"></a>Proteger o Publicador
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/applies-to-version/sql-asdbmi.md)]
  
Os seguintes agentes de replicação se conectam ao Publicador:  
  
-   Agentes de Leitor de Log
-   Snapshot Agent
-   Queue Reader Agent  
-   Merge Agent  
  
 Recomendamos que você forneça um logon adequado para esses agentes, siga o princípio de conceder o mínimo possível de direitos necessários e de proteger o armazenamento de todas as senhas. Para obter mais informações sobre permissões requeridas para cada agente, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Além de gerenciar adequadamente logons e senhas, você deve entender a função da lista de acesso à publicação (PAL). A PAL é usada para habilitar logons para acessar os dados da publicação enquanto restringem o acesso ad hoc ao banco de dados no Publicador.  
  
## <a name="publication-access-list"></a>Lista de acesso à publicação  
 A PAL é o mecanismo principal para proteger publicações no Publicador. A PAL funciona de modo semelhante à lista de controle de acesso do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Quando você cria uma publicação, a replicação cria uma PAL para a publicação. A PAL pode ser configurada para conter uma lista de logons e grupos com acesso concedido à publicação. Quando um agente se conecta ao Publicador ou ao Distribuidor e solicita acesso à publicação, as informações de autenticação na PAL são comparadas com o logon no Publicador fornecido por aquele agente. Esse processo fornece segurança adicional ao Publicador, impedindo que o logon do Publicador e do Distribuidor seja usado por uma ferramenta cliente para executar modificações diretamente no Publicador.  
  
> [!NOTE]  
>  A replicação cria uma função no Publicador para cada publicação impor a associação à PAL. A função tem um nome no formato **Msmerge_** _\<PublicationID>_ para replicação de mesclagem e **MSReplPAL_** _\<PublicationDatabaseID>_ **_** _\<PublicationID>_ para replicação transacional e de instantâneo.  
  
 Por padrão, os seguintes logons são incluídos na PAL: os membros da função de servidor fixa **sysadmin** no momento em que a publicação é criada e o logon usado para criar a publicação. Por padrão, todos os logons que são membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** no banco de dados de publicação podem assinar uma publicação sem serem adicionados explicitamente à PAL.  
  
 Quando você estiver usando a PAL, considere as seguintes diretrizes:  
  
-   É preciso associar o logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com um usuário de banco de dados no banco de dados de publicação antes de adicionar o logon à PAL.  
  
-   Siga o princípio de menos privilégios permitindo logons na PAL somente as permissões cujos logons precisem executar tarefas de replicação. Não adicione os logons a quaisquer funções de banco de dados fixas ou funções de servidor que não são necessários para replicação. Para obter mais informações sobre as permissões exigidas, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) e [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
-   Se for usado um Distribuidor remoto, as contas da PAL precisarão estar disponíveis tanto no Publicador quanto no Distribuidor. A conta ou deve ser uma conta de domínio ou uma conta local que é definida em ambos os servidores. As senhas associadas com ambos os logons devem ser as mesmas.  
  
-   Se a PAL contiver contas do Windows e o domínio usa o Active Directory, a conta em que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] executa deverá ter permissões de leitura do Active Directory. Se você tiver problemas com contas do Windows, verifique se a conta que executa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possui permissões adequadas. Para obter mais informações, consulte a documentação do Windows.  
  
 Para gerenciar o PAL, consulte [Gerenciar logons na Lista de Acesso à Publicação](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md).  
  
## <a name="snapshot-agent"></a>Snapshot Agent  
 Há um Agente de Instantâneo para cada publicação. Para obter mais informações, consulte [Criar uma assinatura](../../../relational-databases/replication/publish/create-a-publication.md).  
  
## <a name="ftp-snapshot-delivery"></a>Entrega de instantâneo por FTP  
 Se especificar que os instantâneos devem ser disponibilizados através de um compartilhamento FTP ao invés de um compartilhamento UNC, você deverá especificar um logon e uma senha quando for configurar o acesso ao FTP. Para obter mais informações, consulte [Deliver a Snapshot Through FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md) (Entregar um instantâneo por meio de FTP).  
  
## <a name="log-reader-agent"></a>Agente de Leitor de Log  
 Há um Agente de Leitor de Log para cada banco de dados publicado para replicação transacional. Para obter mais informações, consulte [Criar uma assinatura](../../../relational-databases/replication/publish/create-a-publication.md).  
  
## <a name="queue-reader-agent"></a>Queue Reader Agent  
 Há um Agente de Leitor de Fila para todos os Publicadores e publicações (que permite assinaturas de atualização em fila) associado a um determinado Distribuidor. Para obter mais informações, consulte [Habilitar atualização de assinaturas para publicações transacionais](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Exibir e modificar configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
