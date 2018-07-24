---
title: Otimizar o desempenho da replicação de mesclagem com o controle de exclusão condicional | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- conditional delete tracking [SQL Server replication]
- merge replication [SQL Server replication], conditional delete tracking
- articles [SQL Server replication], conditional delete tracking
ms.assetid: 58f120a3-ea3a-4e97-93f0-0eb4e580ecf2
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c90fa044fb810de8e269d875643c7eb415c1de2a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37987458"
---
# <a name="optimize-merge-replication-performance-with-conditional-delete-tracking"></a>Otimizar o desempenho da replicação de mesclagem com o controle de exclusão condicional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Com a replicação de mesclagem você pode especificar que as exclusões para um ou mais artigos não devem ser controladas pelos gatilhos de replicação e pelas tabelas do sistema. Se especificar essa opção para um artigo, as exclusões não serão controladas nem replicadas do Publicador ou de qualquer Assinante. Essa opção está disponível para dar suporte a vários cenários de aplicativos e para oferecer uma otimização de desempenho para os casos nos quais a replicação de exclusões não é necessária ou desejada. O desempenho é melhorado de três maneiras: os metadados para exclusões não são armazenados, as exclusões não são enumeradas durante a sincronização e as exclusões não são replicadas para nem aplicadas ao Assinante.  
  
> [!NOTE]  
>  Para usar artigos de somente download, o nível de compatibilidade da publicação deve ser pelo menos 90RTM.  
  
 A opção pode ser especificada na criação de uma publicação ou pode ser alternada para ativada e desativada se um aplicativo necessitar que algumas exclusões sejam replicadas e outras não, como as exclusões de lotes. Os exemplos a seguir ilustram os modos nos quais essa opção poderá ser usada em um aplicativo:  
  
-   O aplicativo para uma força de vendas móvel tem normalmente tabelas como **SalesOrderHeader**, **SalesOrderDetail** e **Produto**. Os pedidos são inseridos no Assinante e replicados para o Publicador, que, muitas vezes, fornece dados a um sistema de efetivação de pedidos. Vários trabalhadores externos usam dispositivos portáteis que têm um armazenamento limitado: após o pedido ser recebido no Publicador, ele pode ser excluído do Assinante. A exclusão não é propagada ao Publicador, pois o pedido continua ativo no sistema.  
  
     Nesse cenário, as exclusões não serão controladas para as tabelas **SalesOrderHeader** e **SalesOrderDetail** . As exclusões serão controladas na tabela **Produto** , pois se um produto for excluído no Publicador, a exclusão deverá ser enviada ao Assinante para manter a lista de produtos atualizada.  
  
-   Um aplicativo armazena os dados históricos em uma tabela como a **TransactionHistory**, que é limpa periodicamente para remover registros antigos com mais de um ano. A tabela pode ser filtrada de modo que os Assinantes recebam dados sobre transações dentro do mês atual. Exclusões mensais de lotes no Publicador que remove dados mais antigos não são relevantes para os Assinantes, mas poderão ser controladas e enumeradas por padrão.  
  
     Nesse cenário, antes de o processamento do lote ocorrer, a atividade pode ser interrompida no sistema e o aplicativo irá desabilitar o controle das exclusões. Após a conclusão do processamento, o controle poderá ser habilitado novamente.  
  
> [!IMPORTANT]  
>  Se uma outra atividade continuar no Publicador, você deverá garantir que as exclusões que deveriam ser propagadas para o Assinante não ocorram enquanto o controle das exclusões estiver desabilitado.  
  
 **Para especificar que as exclusões não devem ser controladas**  
  
-   Programação [!INCLUDE[tsql](../../../includes/tsql-md.md)] de replicação: [Especificar que as exclusões não devem ser controladas para artigos de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de artigos para a replicação de mesclagem](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Otimizar o desempenho da replicação de mesclagem com artigos de somente download](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)  
  
  
