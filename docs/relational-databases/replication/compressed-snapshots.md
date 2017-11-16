---
title: "Instantâneos compactados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], compressed
- snapshot replication [SQL Server], compressed snapshots
- compressed snapshots [SQL Server replication]
ms.assetid: 979ffa7c-3a88-4e70-8cf2-b8d452fd7a7f
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 13f3bde8699bb77fd733604d81ddf65000cc55ca
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="compressed-snapshots"></a>Instantâneos compactados
  A compactação de arquivos de instantâneo é apropriada quando se está transferindo instantâneos por uma rede lenta ou salvando-os em mídia removível e um instantâneo não compactado é grande demais para a mídia. A compactação de arquivos de instantâneo é útil nessas situações, mas a compactação aumenta o tempo para gerar e aplicar o instantâneo.  
  
 Arquivos de instantâneo compactados são gravados no formato de arquivo CAB [!INCLUDE[msCoName](../../includes/msconame-md.md)] , capaz de compactar arquivos de 2 GB ou menos (se os arquivos de instantâneo forem maiores do que 2GB, eles não podem ser compactados). Para compactar arquivos, eles precisam ser gravados em uma pasta de instantâneo alternativa (arquivos gravados na pasta de instantâneo padrão não podem ser compactados). Para obter mais informações sobre pastas de instantâneo alternativos, consulte [Locais da pasta de instantâneos alternativos](../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
 Arquivos são descompactados no local onde o Distribuition Agent ou Agente de Mesclagem são executados; assinaturas pull são geralmente usadas com instantâneos compactados para que os arquivos sejam descompactados no Assinante. Quando o Assinante recebe um arquivo compactado, o arquivo é inicialmente gravado em um local temporário. Depois que o arquivo compactado é copiado para o Assinante, os arquivos de instantâneo no arquivo compactado são descompactados, em ordem, um arquivo de cada vez pelo utilitário CAB. O espaço exigido no Assinante é o tamanho do arquivo compactado mais o arquivo não comprimido maior.  
  
> [!NOTE]  
>  Os instantâneos compactados podem, em alguns casos, melhorar o desempenho da transferência de arquivos de instantâneo pela rede. No entanto, a compactação de instantâneos exige processamento adicional por parte do Snapshot Agent ao gerar os arquivos de instantâneo, e por parte do Distribution Agent ou Merge Agent ao aplicar os arquivos de instantâneo. Em alguns casos, isso pode reduzir a velocidade da geração de instantâneos e aumentar o tempo para se aplicar um instantâneo. Além disso, instantâneos compactados não podem ser retomados no caso de uma falha de rede; consequentemente, não são apropriados para redes não confiáveis. Considere essa possibilidade cuidadosamente ao usar instantâneos compactados por uma rede.  
  
 **Para compactar e entregar arquivos de instantâneo**  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Compactar arquivos de instantâneo &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   Programação [!INCLUDE[tsql](../../includes/tsql-md.md)] de replicação: [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de replicação&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Consulte também  
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Opções de instantâneo](../../relational-databases/replication/snapshot-options.md)  
  
  
