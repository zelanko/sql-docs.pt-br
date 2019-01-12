---
title: Alternar locais de pasta de instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c86e79928bdadb129ed0aa591e4bd035ffe22c1c
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54128996"
---
# <a name="alternate-snapshot-folder-locations"></a>Locais da pasta de instantâneos alternativos
  Locais de instantâneos alternativos permitem que você armazene arquivos de instantâneos em outro local ou em local diferente do padrão onde normalmente está localizado no Distribuidor. Locais alternativos podem ficar em outro servidor, em uma unidade de rede ou uma mídia removível (como um CD-ROM ou disco removível).  
  
 Locais de instantâneo alternativos são armazenados como uma propriedade da publicação. Devido ao local de instantâneo alternativo ser uma propriedade da publicação, o Agente de Distribuição e o Agente de Mesclagem podem localizar o instantâneo apropriado como parte do processo de sincronização.  
  
 Para especificar um local de pasta de instantâneo padrão ou compactar arquivos de instantâneo, crie a publicação sem criar o instantâneo inicial imediatamente, defina as propriedades da publicação para o local do instantâneo e execute o Agente de Instantâneo para aquela publicação. Se você alterar o local alternativo após criar o instantâneo inicial, o local de qualquer instantâneo gerado para a publicação não será realocado para o novo local alternativo. Nesse caso, dependendo das configurações da publicação, o Merge Agent ou Distribution Agent talvez não encontrem os arquivos de instantâneo no novo local alternativo.  
  
> [!NOTE]  
>  Não especifique nenhum local alternativo (usando a caixa de diálogo **Propriedades da Publicação** ou [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)) que seja igual ao local da pasta do instantâneo padrão.  
  
> [!CAUTION]  
>  Não use WebSync e locais de pasta de instantâneo alternativos ao mesmo tempo.  
  
 **Para especificar locais de instantâneo alternativos**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Especifique um local de pasta de instantâneo alternativa](snapshot-options.md#snapshot-folder-locations) 
  
-   Programação [!INCLUDE[tsql](../../includes/tsql-md.md)] de replicação: [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Consulte também  
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)   
 [Opções de instantâneo](snapshot-options.md)  
  
  
