---
title: "Sincronizar uma assinatura usando o Gerenciador de Sincroniza&#231;&#227;o do Windows (Gerenciador de Sincroniza&#231;&#227;o do Windows) | Microsoft Docs"
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
  - "sincronização [replicação do SQL Server], Gerenciador de Sincronização do Windows"
  - "Gerenciador de Sincronização do Windows"
ms.assetid: 80f15dd6-e84d-4f96-9866-5b34ea531f1e
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Sincronizar uma assinatura usando o Gerenciador de Sincroniza&#231;&#227;o do Windows (Gerenciador de Sincroniza&#231;&#227;o do Windows)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] O Gerenciador de sincronização do Windows só pode ser usado para sincronizar assinaturas Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicações se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução no mesmo computador como o Gerenciador de sincronização (ele também pode ser usado para sincronizar arquivos offline e páginas da Web). Para usar o Gerenciador de Sincronização:  
  
1.  Habilitar a sincronização de assinaturas pull com o Gerenciador de sincronização no **Propriedades de assinatura - \< assinante>: \< Banco_de_dados_de_assinatura>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar propriedades de assinatura Pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
2.  Gerenciador de sincronização de acesso por meio de **Iniciar** menu no Windows.  
  
 O Gerenciador de Sincronização permite usar o Resolvedor Interativo para mesclar assinaturas. Normalmente, os conflitos detectados durante a sincronização são resolvidos automaticamente, mas se a resolução interativa estiver habilitada, os conflitos poderão ser resolvidos pelo usuário durante a sincronização. Se a sincronização a ser executada for a do Gerenciador de Sincronização do Windows (como uma sincronização agendada ou sob demanda no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no Replication Monitor) os conflitos serão resolvidos automaticamente sem a intervenção do usuário, de acordo com o resolvedor especificado para o artigo.  
  
> [!NOTE]  
>  A partir do [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] e [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)], as versões de 64 bits do Gerenciador de Sincronização do Windows não podem detectar assinaturas de 32 bits.  
  
### Para habilitar a sincronização de assinaturas pull com o Gerenciador de Sincronização do Windows  
  
1.  Na **geral** página do **Propriedades de assinatura - \< assinante>: \< Banco_de_dados_de_assinatura>** caixa de diálogo, selecione um valor de **Habilitar** para o **Gerenciador de sincronização do Windows Use** opção.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### Para sincronizar uma assinatura pull com o Gerenciador de Sincronização  
  
1.  Inicie o Gerenciador de Sincronização usando um dos seguintes métodos:  
  
    -   No Internet Explorer, clique em **ferramentas**, e, em seguida, clique em **sincronizar**.  
  
    -   Clique em **Iniciar**, aponte para **programas** ou **todos os programas**, aponte para **Acessórios**, e, em seguida, clique em **sincronizar**.  
  
    -   Clique em **Iniciar**, e, em seguida, clique em **Executar.** No **executar** caixa de diálogo, digite **mobsync.exe** no **Abrir** campo e, em seguida, clique em **OK**.  
  
2.  No **itens a serem sincronizados** caixa de diálogo, selecione as assinaturas para sincronizar. As assinaturas são listadas sob as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no computador.  
  
3.  Clique em **sincronizar**.  
  
### Para reinicializar uma assinatura pull com o Gerenciador de Sincronização  
  
1.  No **itens a serem sincronizados** caixa de diálogo, selecione uma assinatura e, em seguida, clique em **propriedades**.  
  
2.  No **Propriedades de assinatura do SQL Server** caixa de diálogo, clique em **reinicializar assinatura**.  
  
3.  Clique em **Sim**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Por padrão, na próxima vez que a assinatura é sincronizada, um novo instantâneo é aplicado ao banco de dados de assinatura. Para obter mais informações, consulte [reinicializar assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
> [!NOTE]  
>  A replicação de mesclagem permite que qualquer alteração pendente seja carregada no Publicador antes do instantâneo ser aplicado, mas essa opção não está disponível no Gerenciador de Sincronização. Para carregar alterações, sincronize a assinatura antes de reiniciá-la.  
  
### Para definir propriedades de uma assinatura pull no Gerenciador de Sincronização  
  
1.  No **itens a serem sincronizados** caixa de diálogo, selecione uma assinatura e, em seguida, clique em **propriedades**.  
  
2.  Exiba e modifique propriedades nas seguintes guias:  
  
    -   **Identificação**  
  
    -   **Logon do assinante**, **logon do distribuidor**, e **logon do publicador** (para replicação de mesclagem somente)  
  
    -   **Informações do servidor Web** (para assinaturas de mesclagem em assinantes que executam o SQL Server 2005 ou posterior)  
  
    -   **Outro**  
  
     É recomendável usar a Autenticação do Windows para todas as conexões. Para obter informações sobre as permissões exigidas pelo Distribution Agent e o agente de mesclagem, consulte [modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### Para remover uma assinatura pull do Gerenciador de Sincronização  
  
1.  No **itens a serem sincronizados** caixa de diálogo, selecione uma assinatura e, em seguida, clique em **propriedades**.  
  
2.  No **Propriedades de assinatura do SQL Server** caixa de diálogo, clique em **Remover assinatura**.  
  
3.  Selecione uma opção de **Remover assinatura** caixa de diálogo.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### Para usar o Resolvedor Interativo  
  
1.  Habilite o artigo e assinatura a usarem a resolução interativa. Para obter mais informações, consulte [especificar resolução interativa de conflitos para artigos de mesclagem](../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md).  
  
2.  Após o início da sincronização da assinatura no Gerenciador de Sincronização, o Resolvedor Interativo será iniciado automaticamente se a resolução interativa de conflitos estiver habilitada e se houver conflitos em um ou mais artigos. O Resolvedor Interativo exibe um conflito de cada vez, com uma sugestão de resolução para cada conflito (com base no resolvedor especificado quando a publicação e a assinatura foram criadas).  
  
3.  Opcionalmente, edite qualquer uma das colunas exibidas no Resolvedor Interativo e clique em um dos seguintes botões para resolver o conflito:  
  
    -   **Aceitar Sugestão**  
  
    -   **Aceitar Publicador**  
  
    -   **Aceitar Assinante**  
  
    -   **Resolver automaticamente todos os** (todos os conflitos atuais são resolvidos sem entrada adicional)  
  
     Em seguida, a linha selecionada é aplicada ao Publicador e/ou Assinante. Ela é propagada para outros nós na topologia durante sincronizações subsequentes.  
  
> [!NOTE]  
>  As edições serão aplicadas apenas se fizerem parte da linha escolhida para resolução. Por exemplo, se você fizer edições no **Publisher**, e, em seguida, clique em **Aceitar assinante**, as edições serão descartadas.  
  
## Consulte também  
 [Resolução de conflito interativo](../../relational-databases/replication/merge/interactive-conflict-resolution.md)  
  
  