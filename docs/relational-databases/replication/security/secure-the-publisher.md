---
title: "Proteger o Publicador | Microsoft Docs"
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
  - "logons [replicação do SQL Server], lista de acesso da publicação"
  - "publicações [replicação do SQL Server], listas de acesso da publicação"
  - "lista de acesso à publicação (PAL)"
  - "PAL (lista de acesso à publicação)"
  - "Publicadores [replicação do SQL Server], segurança"
  - "publicações [replicação do SQL Server], segurança"
ms.assetid: 4513a18d-dd6e-407a-b009-49dc9432ec7e
caps.latest.revision: 48
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 48
---
# Proteger o Publicador
  Os seguintes agentes de replicação se conectam ao Publicador:  
  
-   Agente de Leitor de Log  
  
-   Snapshot Agent  
  
-   Queue Reader Agent  
  
-   Agente de Mesclagem  
  
 Recomendamos que você forneça um logon adequado para esses agentes, siga o princípio de conceder o mínimo possível de direitos necessários e de proteger o armazenamento de todas as senhas. Para obter mais informações sobre permissões requeridas para cada agente, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Além de gerenciar adequadamente logons e senhas, você deve entender a função da lista de acesso à publicação (PAL). A PAL é usada para habilitar logons para acessar os dados da publicação enquanto restringem o acesso ad hoc ao banco de dados no Publicador.  
  
## Lista de acesso à publicação  
 A PAL é o mecanismo principal para proteger publicações no Publicador. A PAL funciona de modo semelhante à lista de controle de acesso do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Quando você cria uma publicação, a replicação cria uma PAL para a publicação. A PAL pode ser configurada para conter uma lista de logons e grupos com acesso concedido à publicação. Quando um agente se conecta ao Publicador ou ao Distribuidor e solicita acesso à publicação, as informações de autenticação na PAL são comparadas com o logon no Publicador fornecido por aquele agente. Esse processo fornece segurança adicional ao Publicador, impedindo que o logon do Publicador e do Distribuidor seja usado por uma ferramenta cliente para executar modificações diretamente no Publicador.  
  
> [!NOTE]  
>  A replicação cria uma função no Publicador para cada publicação impor a associação à PAL. A função tem um nome no formato **msmerge _***\< Id_da_publicação>* para replicação de mesclagem e **msreplpal _***\< Id_do_banco_de_dados_de_publicação>***_***\< Id_da_publicação>* para replicação transacional e de instantâneo.  
  
 Por padrão, os seguintes logons são incluídos na PAL: os membros da função de servidor fixa **sysadmin** no momento em que a publicação é criada e o logon usado para criar a publicação. Por padrão, todos os logons que são membros do **sysadmin** função de servidor fixa ou o **db_owner** função de banco de dados fixa no banco de dados de publicação pode assinar uma publicação sem serem adicionados explicitamente à PAL.  
  
 Quando você estiver usando a PAL, considere as seguintes diretrizes:  
  
-   É preciso associar o logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com um usuário de banco de dados no banco de dados de publicação antes de adicionar o logon à PAL.  
  
-   Siga o princípio de menos privilégios permitindo logons na PAL somente as permissões cujos logons precisem executar tarefas de replicação. Não adicione os logons a quaisquer funções de banco de dados fixas ou funções de servidor que não são necessários para replicação. Para obter mais informações sobre as permissões exigidas, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) e [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
-   Se for usado um Distribuidor remoto, as contas da PAL precisarão estar disponíveis tanto no Publicador quanto no Distribuidor. A conta ou deve ser uma conta de domínio ou uma conta local que é definida em ambos os servidores. As senhas associadas com ambos os logons devem ser as mesmas.  
  
-   Se a PAL contiver contas do Windows e o domínio usa o Active Directory, a conta em que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] executa deverá ter permissões de leitura do Active Directory. Se você tiver problemas com contas do Windows, verifique se a conta que executa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possui permissões adequadas. Para obter mais informações, consulte a documentação do Windows.  
  
 Para gerenciar a PAL, consulte [Gerenciar logons na lista de acesso da publicação](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md).  
  
## Snapshot Agent  
 Há um Agente de Instantâneo para cada publicação. Para obter mais informações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
## Entrega de instantâneo por FTP  
 Se especificar que os instantâneos devem ser disponibilizados através de um compartilhamento FTP ao invés de um compartilhamento UNC, você deverá especificar um logon e uma senha quando for configurar o acesso ao FTP. Para obter mais informações, consulte [entregar um instantâneo por meio de FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
## Agente de Leitor de Log  
 Há um Agente de Leitor de Log para cada banco de dados publicado para replicação transacional. Para obter mais informações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
## Queue Reader Agent  
 Há um Agente de Leitor de Fila para todos os Publicadores e publicações (que permite assinaturas de atualização em fila) associado a um determinado Distribuidor. Para obter mais informações, consulte [Habilitar assinaturas de atualização para publicações transacionais](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).  
  
## Consulte também  
 [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção e 40; Replicação e 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  