---
title: "Executar scripts antes e depois da aplicação do instantâneo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
- scripts [SQL Server replication]
ms.assetid: 9a6872c2-9bed-477f-9d2f-332d640edcf2
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c9bc1f84cf007de680f8f2da80668aebe62f7d8e
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="execute-scripts-before-and-after-the-snapshot-is-applied"></a>Executar scripts antes e depois da aplicação do instantâneo
  É possível especificar scripts a serem executados no Assinante antes ou depois que o instantâneo é aplicado. Scripts podem ser usados por várias razões, tais como a criação de logon e esquemas (proprietários de objeto) em cada Assinante.  
  
 Especifica-se um local de arquivo para cada script, e o Agente de Instantâneo copia os arquivos de script para a atual pasta de instantâneo a cada vez que ocorrer o processo de instantâneo. O Agente de Distribuição ou Agente de Mesclagem executa o script pré-instantâneo antes de qualquer script do objeto replicado, ao aplicar um instantâneo. O Agente de Distribuição ou o Agente de Mesclagem executa o script pós-instantâneo depois que todos os outros scripts de objeto e dados replicados tentam sido aplicados. Depois que a aplicação de instantâneo for concluída e os arquivos de script forem executados com êxito, os arquivos de script são removidos do diretório de trabalho no Assinante.  
  
 O script é executado lançando o utilitário **sqlcmd** . Antes de implantar um script, execute-o com **sqlcmd** para assegurar que a execução corra conforme esperado. Os conteúdos de scripts executados antes e depois que o instantâneo é aplicado devem ser repetíveis. Por exemplo, se você criar uma tabela em um script, você deve, em primeiro lugar, verificar sua existência e tomar as ações devidas caso ela exista. O script deve ser repetível, pois se você precisar reinicializar uma assinatura para a qual o script já foi aplicado, o script será aplicado novamente quando o novo instantâneo for aplicado durante a reinicialização.  
  
 Se você estiver compactando o arquivo de instantâneo (colocando-o em um formato de arquivo CAB [!INCLUDE[msCoName](../../includes/msconame-md.md)] ), os scripts também são compactados e colocados no arquivo CAB. Depois que o arquivo de instantâneo compactado for transferido para o Assinante e descompactado para um diretório de trabalho no Assinante, qualquer script indicado como script de pré-instantâneo será executado. Da mesma forma, qualquer script de pós-instantâneo é descompactado e executado no Assinante como última etapa aplicando-se o instantâneo.  
  
 **Para executar scripts antes e depois que o instantâneo é aplicado**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[Como executar scripts antes e depois que um instantâneo é aplicado \(SQL Server Management Studio\)](../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   Programação [!INCLUDE[tsql](../../includes/tsql-md.md)] de replicação: [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de replicação&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Consulte também  
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Snapshot Options](../../relational-databases/replication/snapshot-options.md)  
  
  
