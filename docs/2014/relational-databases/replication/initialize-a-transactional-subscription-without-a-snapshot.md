---
title: Inicializar uma assinatura transacional sem um instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, initializing
- replication [SQL Server], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 75c8c1f8-60bc-44a8-944b-d18d1f6bda11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0cef8a7e8a64935cca6b378e14c00eb0d80f6b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721147"
---
# <a name="initialize-a-transactional-subscription-without-a-snapshot"></a>Inicializar uma assinatura transacional sem um instantâneo
  Por padrão, uma assinatura a uma publicação transacional é inicializada com um instantâneo, que é gerado pelo Agente de Instantâneo e aplicado pelo Agente de Distribuição. Em alguns cenários, como os que envolvem grandes conjuntos de dados iniciais, é preferível inicializar uma assinatura usando outro método. Outros métodos de inicializar um Assinante incluem:  
  
-   Especificando um backup. Restaure o backup no Assinante e, então, o Agente de Distribuição copia os metadados de replicação e procedimentos do sistema necessários. Inicializando com um backup é a forma mais fácil de entregar os dados ao Assinante e é conveniente, porque qualquer backup recente pode ser usado se for feito após a publicação ter sido habilitada para inicialização com um backup.  
  
-   Copiando um conjunto de dados inicial ao Assinante por outro mecanismo, como anexando um banco de dados. Você deve assegurar-se de que os dados e o esquema corretos estão no Assinante e, então, o Agente de Distribuição copia os metadados e procedimentos do sistema necessários.  
  
## <a name="initializing-a-subscription-with-a-backup"></a>Inicializando uma assinatura com um backup  
 Um backup contém um banco de dados inteiro; portanto, cada banco de dados de assinatura conterá uma cópia completa do banco de dados de publicação quando este for inicializado:  
  
-   O backup inclui tabelas que não são especificadas como artigos para a publicação.  
  
-   O backup inclui todos os dados, até mesmo se filtros de linha ou de coluna forem especificados em uma tabela.  
  
 É da responsabilidade do administrador ou aplicativo remover quaisquer objetos ou dados não desejados depois que o backup tiver sido restaurado. Em sincronizações subsequentes, as alterações de dados só serão replicadas se elas se aplicarem às tabelas que são especificadas como artigos e satisfizerem os critérios de filtragem que você especificou.  
  
> [!NOTE]  
>  Ao restaurar um backup, você deve garantir que o backup é proveniente de um Publicador se desejar que o Assinante sincronize automaticamente. Os valores LSN (número de sequência de log) no backup (usados para definir o ponto para iniciar a sincronização) são específicos ao Publicador.  
  
 **Para inicializar uma assinatura com um backup**  
  
 Para inicializar uma assinatura com um backup, você deve primeiro habilitar a opção ao criar a publicação e, então, especificar valores para um número de opções quando criar a assinatura. As publicações podem ser habilitadas pelo Assistente para Nova Publicação ou programaticamente. Porém, os valores requeridos para as opções de assinatura só podem ser especificados programaticamente.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Habilitar a inicialização com um backup para publicações transacionais &#40;SQL Server Management Studio&#41;](enable-initialization-with-backup-for-transactional-publications.md)  
  
-   Programação Transact-SQL de replicação: [Inicializar uma assinatura transacional de um backup &#40;programação Transact-SQL de replicação&#41;](initialize-a-transactional-subscription-from-a-backup.md)  
  
> [!NOTE]  
>  Se uma assinatura for inicializada sem usar um instantâneo, a em que o serviço do SQL Server será executado no Publicador deverá ter permissões para gravação na pasta do instantâneo no Distribuidor. Para obter mais informações sobre permissões, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
### <a name="ensuring-the-suitability-of-a-backup"></a>Assegurando que um backup é adequado  
 Um backup será adequado para inicializar um Assinante se todas as transações que ocorreram, feitas após o backup, estiverem armazenadas no Distribuidor. A replicação exibirá uma mensagem de erro se o backup não for adequado.  
  
 Para ajudar assegurar que um backup é adequado para uso, siga estas diretrizes:  
  
-   Use o último backup disponível, e se esse for mais antigo que o período máximo de retenção máximo da distribuição, crie um novo backup antes de tentar inicializar a assinatura com um backup. Para obter mais informações sobre período de retenção, consulte [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
-   Por padrão, o trabalho de limpeza de distribuição desmarca transações com mais de 72 horas do banco de dados de distribuição. A limpeza é baseada no conjunto de período de retenção para a publicação. Ao sincronizar com backups mais antigos, considere desabilitar temporariamente o trabalho antes de fazer o backup que gostaria de restaurar e habilite novamente após a assinatura ter sido criada com êxito. Isto previne a remoção de transações do banco de dados de distribuição que poderiam ser necessárias para sincronizar do backup com êxito. Para mais informações sobre execução de trabalhos de limpeza, consulte [Executar trabalhos de manutenção de replicação &#40;SQL Server Management Studio&#41;](administration/run-replication-maintenance-jobs-sql-server-management-studio.md).  
  
 Em alguns casos você deverá fazer as personalizações manualmente no banco de dados restaurado no Assinante após definir que as assinaturas serão inicializadas com um backup. Em geral, modificações manuais no banco de dados restaurado do Assinante são requeridas se a publicação for definida de tal forma que se espere que o conteúdo do banco de dados do Assinante seja diferente do conteúdo do banco de dados Publicador.  
  
-   Exibições indexadas ao banco de dados restaurado terão de ser convertidas a tabelas se elas forem publicadas como artigos de exibição indexada para tabela baseados em log  
  
-   Colunas de carimbo de hora assinadas no banco de dados restaurado devem ser convertidas a colunas **binárias(8)** : copie o conteúdo das tabelas contendo colunas de carimbo de hora para as novas tabelas com esquemas correspondentes a menos que existam colunas **binárias (8)** no lugar de colunas de carimbo de hora, descarte as tabelas originais e renomeie as novas tabelas com os mesmos nomes das tabelas originais.  
  
## <a name="initializing-a-subscription-with-an-alternative-method"></a>Inicializando uma assinatura com um método alternativo  
 É possível inicializar uma assinatura usando qualquer método que permita copiar o esquema do banco de dados de publicação e dados ao Assinante, como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Quando você usar um método alternativo para inicializar o Assinante, objetos de suporte de replicação são copiados ao Assinante.  
  
 Diferente de inicializar com um backup, você ou seu aplicativo devem assegurar que os dados e o esquema estão sincronizados corretamente na hora que você adicionar a assinatura. Por exemplo, se houver atividade no Publicador, durante o tempo em que os dados e o esquema são copiados no Assinante e a Assinatura é adicionada, as alterações resultantes dessa atividade poderão não ser replicadas no Assinante.  
  
 Para inicializar uma assinatura com um método alternativo, consulte [Initialize a Subscription Manually](initialize-a-subscription-manually.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Inicializar uma Assinatura](initialize-a-subscription.md)  
  
  
