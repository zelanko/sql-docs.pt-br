---
title: "Replica&#231;&#227;o de script | Microsoft Docs"
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
  - "scripts [replicação do SQL Server], objetos de replicação"
  - "script de replicação de mesclagem [replicação do SQL Server]"
  - "replicação [SQL Server], scripts"
  - "replicação de instantâneo [SQL Server], script"
  - "scripts [replicação do SQL Server]"
  - "replicação transacional, scripts"
ms.assetid: e50fac44-54c0-470c-a4ea-9c111fa4322b
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Replica&#231;&#227;o de script
  Todos os componentes de replicação em uma topologia devem ser incluídos no script como parte de um plano de recuperação de desastre  e os scripts também podem ser usados para automatizar tarefas repetitivas. Um script contém os procedimentos armazenados do sistema Transact-SQL necessários para implementar os componentes de replicação incluídos no script, como uma publicação ou assinatura. Scripts podem ser criados em um assistente (como o Assistente de nova publicação) ou em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] depois de criar um componente. É possível exibir, modificar e executar o script por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou do **sqlcmd**. Os scripts podem ser armazenados com arquivos de backup para serem usados no caso de uma topologia de replicação precisar ser reconfigurada.  
  
 O script de um componente deve ser refeito caso alguma propriedade seja alterada. Se você usar procedimentos armazenados com replicação transacional, uma cópia de cada procedimento deve ser armazenada com os scripts; a cópia deve ser atualizada se o procedimento for alterado (os procedimentos são normalmente alterados devido a mudanças no esquema ou nos requisitos de aplicativo). Para obter mais informações sobre procedimentos personalizados, consulte [especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
 Para publicações de mesclagem que usam filtros com parâmetros, os scripts de publicação contêm as chamadas de procedimento armazenado para criar partições de dados. O script fornece uma referência para as partições criadas e um modo para recriar uma ou mais partições, caso seja necessário.  
  
## Exemplo de automatização de uma tarefa com scripts  
 Considere o [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]que implementa a replicação de mesclagem para distribuir dados a sua força de vendas remota. Um representante de vendas baixa todos os dados que pertencem aos clientes em seu território usando assinaturas pull. Ao trabalhar offline, o representante de vendas atualiza os dados e digita novos clientes e pedidos. Como o [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] tem mais de 50 representantes de vendas em territórios diferentes, a criação de diferentes assinaturas em cada Assinante com o Assistente para Nova Assinatura consumiria muito tempo. Em vez disso, o administrador de replicação pode seguir essas etapas:  
  
1.  Definir as publicações de mesclagem necessárias com partições baseadas nos representantes de vendas ou em seu território.  
  
2.  Criar uma assinatura pull para um Assinante.  
  
3.  Gerar um script baseado naquela assinatura pull.  
  
4.  Modificar o script, alterando valores como o nome do Assinante.  
  
5.  Executar o script em vários Assinantes para gerar as assinaturas pull exigidas.  
  
## Executar o script de objetos de replicação  
 Script de objetos de replicação de assistentes de replicação ou do **replicação** pasta [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se você executar o script a partir dos assistentes, pode escolher criar objetos e então executar o script ou pode escolher somente executar o script.  
  
> [!IMPORTANT]  
>  Todas as senhas têm o script executado como NULL. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se armazenar credenciais em um arquivo de script, proteja o arquivo para evitar acesso não autorizado.  
  
 Para obter mais informações sobre como usar os assistentes de replicação, consulte:  
  
-   [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)  
  
#### Para executar um script de um objeto a partir de um assistente de replicação  
  
1.  Sobre o **Ações do assistente** página de um assistente, selecione a caixa de seleção apropriada para o Assistente:  
  
    -   **Gere um arquivo de script com etapas para criar uma publicação**  
  
    -   **Gere um arquivo de script com etapas criar a assinatura(s)**  
  
    -   **Gere um arquivo de script com etapas para configurar a distribuição**  
  
2.  Especifique opções no **Propriedades do arquivo de Script** página.  
  
3.  Conclua o assistente.  
  
#### Para executar o script de um objeto a partir do Management Studio  
  
1.  Conecte-se ao Distribuidor, Publicador ou Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e expanda o nó do servidor.  
  
2.  Expanda o **replicação** pasta e, em seguida, expanda o **publicações locais** pasta ou o **assinaturas locais** pasta.  
  
3.  Clique em uma publicação ou assinatura e, em seguida, clique em **Gerar Scripts**.  
  
4.  Especificar opções de **Gerar Script SQL - \< Objeto_de_replicação>** caixa de diálogo.  
  
5.  Clique em **Script para arquivo**.  
  
6.  Insira um nome de arquivo de **local do arquivo de Script** caixa de diálogo e clique **Salvar**. Será exibida uma mensagem de status.  
  
7.  Clique em **OK**, e, em seguida, clique em **Fechar**.  
  
#### Para executar script de vários objetos do Management Studio  
  
1.  Conecte-se ao Distribuidor, Publicador ou Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e expanda o nó do servidor.  
  
2.  Clique com botão direito do **replicação** pasta e clique **Gerar Scripts**.  
  
3.  Especificar opções de **Gerar Script SQL** caixa de diálogo.  
  
4.  Clique em **Script para arquivo**.  
  
5.  Insira um nome de arquivo de **local do arquivo de Script** caixa de diálogo e clique **Salvar**. Será exibida uma mensagem de status.  
  
6.  Clique em **OK e, em seguida,** clique **Fechar**.  
  
  