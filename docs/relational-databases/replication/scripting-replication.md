---
title: Replicação de scripts | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server replication], replication objects
- merge replication scripting [SQL Server replication]
- replication [SQL Server], scripting
- snapshot replication [SQL Server], scripting
- scripts [SQL Server replication]
- transactional replication, scripting
ms.assetid: e50fac44-54c0-470c-a4ea-9c111fa4322b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 42896ae8b5c10685c14e73c07ab2dcc2441d80b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837064"
---
# <a name="scripting-replication"></a>Replicação de script
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Todos os componentes de replicação em uma topologia devem ser incluídos no script como parte de um plano de recuperação de desastre  e os scripts também podem ser usados para automatizar tarefas repetitivas. Um script contém os procedimentos armazenados do sistema Transact-SQL necessários para implementar os componentes de replicação incluídos no script, como uma publicação ou assinatura. Os scripts podem ser criados em um assistente (como o Assistente para Nova Publicação) ou no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] depois de você criar um componente. É possível exibir, modificar e executar o script por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou do **sqlcmd**. Os scripts podem ser armazenados com arquivos de backup para serem usados no caso de uma topologia de replicação precisar ser reconfigurada.  
  
 O script de um componente deve ser refeito caso alguma propriedade seja alterada. Se você usar procedimentos armazenados com replicação transacional, uma cópia de cada procedimento deve ser armazenada com os scripts; a cópia deve ser atualizada se o procedimento for alterado (os procedimentos são normalmente alterados devido a mudanças no esquema ou nos requisitos de aplicativo). Para mais informações sobre procedimentos personalizados, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 Para publicações de mesclagem que usam filtros com parâmetros, os scripts de publicação contêm as chamadas de procedimento armazenado para criar partições de dados. O script fornece uma referência para as partições criadas e um modo para recriar uma ou mais partições, caso seja necessário.  
  
## <a name="example-of-automating-a-task-with-scripts"></a>Exemplo de automatização de uma tarefa com scripts  
 Considere o [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]que implementa a replicação de mesclagem para distribuir dados a sua força de vendas remota. Um representante de vendas baixa todos os dados que pertencem aos clientes em seu território usando assinaturas pull. Ao trabalhar offline, o representante de vendas atualiza os dados e digita novos clientes e pedidos. Como o [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] tem mais de 50 representantes de vendas em territórios diferentes, a criação de diferentes assinaturas em cada Assinante com o Assistente para Nova Assinatura consumiria muito tempo. Em vez disso, o administrador de replicação pode seguir essas etapas:  
  
1.  Definir as publicações de mesclagem necessárias com partições baseadas nos representantes de vendas ou em seu território.  
  
2.  Criar uma assinatura pull para um Assinante.  
  
3.  Gerar um script baseado naquela assinatura pull.  
  
4.  Modificar o script, alterando valores como o nome do Assinante.  
  
5.  Executar o script em vários Assinantes para gerar as assinaturas pull exigidas.  
  
## <a name="script-replication-objects"></a>Executar o script de objetos de replicação  
 Script de objetos de replicação dos assistentes de replicação ou da pasta **Replicação** no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se você executar o script a partir dos assistentes, pode escolher criar objetos e então executar o script ou pode escolher somente executar o script.  
  
> [!IMPORTANT]  
>  Todas as senhas têm o script executado como NULL. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se armazenar credenciais em um arquivo de script, proteja o arquivo para evitar acesso não autorizado.  
  
 Para obter mais informações sobre como usar os assistentes de replicação, consulte:  
  
-   [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)  
  
#### <a name="to-script-an-object-from-a-replication-wizard"></a>Para executar um script de um objeto a partir de um assistente de replicação  
  
1.  Na página **Ações do Assistente** de um assistente, marque a caixa de seleção apropriada para o assistente:  
  
    -   **Gere um arquivo de script com etapas para criar uma publicação**  
  
    -   **Gere um arquivo de script com etapas criar a assinatura(s)**  
  
    -   **Gere um arquivo de script com etapas para configurar a distribuição**  
  
2.  Especifique opções na página **Propriedades do Arquivo de Script** .  
  
3.  Conclua o assistente.  
  
#### <a name="to-script-an-object-from-management-studio"></a>Para executar o script de um objeto a partir do Management Studio  
  
1.  Conecte-se ao Distribuidor, Publicador ou Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e então expanda a pasta **Publicações Locais** ou a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito do mouse em uma publicação ou assinatura e então clique em **Gerar Scripts**.  
  
4.  Especifique as opções na caixa de diálogo **Gerar Script SQL – \<ReplicationObject>**.  
  
5.  Clique em **Script para Arquivo**.  
  
6.  Insira um nome de arquivo na caixa de diálogo **Local do Arquivo de Script** e então clique em **Salvar**. Será exibida uma mensagem de status.  
  
7.  Clique em **OK**e então clique em **Fechar**.  
  
#### <a name="to-script-multiple-objects-from-management-studio"></a>Para executar script de vários objetos do Management Studio  
  
1.  Conecte-se ao Distribuidor, Publicador ou Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Clique com o botão direito do mouse na pasta **Replicação** e então clique em **Gerar Scripts**.  
  
3.  Especifique opções na caixa de diálogo **Gerar Script SQL** .  
  
4.  Clique em **Script para Arquivo**.  
  
5.  Insira um nome de arquivo na caixa de diálogo **Local do Arquivo de Script** e então clique em **Salvar**. Será exibida uma mensagem de status.  
  
6.  Clique em **OK** e então clique em **Fechar**.  
  
  
