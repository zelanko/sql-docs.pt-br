---
title: Resolvedor Interativo de Conflitos de Replicação da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replconflictviewer.interactiveresolver.f1
ms.assetid: d3d4a480-782b-4b1d-b839-565c8cf6cb24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6c1637301eb6a6c9663f122e61447b9a8adb1623
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48213577"
---
# <a name="microsoft-replication-interactive-conflict-resolver"></a>Resolvedor Interativo de Conflitos de Replicação da Microsoft
  O Resolvedor Interativo de Conflitos de Replicação pode ser usado para assinaturas de mesclagem sincronizadas usando o Gerenciador de Sincronização do Windows. Ele permite exibir, comparar, editar e selecionar o resultado dos conflitos de dados. A replicação também inclui o Visualizador de Conflitos, que permite exibir e modificar resultados de conflitos depois de terem sido confirmados. O Resolvedor Interativo de Conflitos permite selecionar o resultado durante a sincronização.  
  
> [!NOTE]  
>  Os conflitos que envolvem registros lógicos não são exibidos no Resolvedor Interativo. Para exibir informações sobre esses conflitos, use procedimentos armazenados de replicação. Para obter mais informações, consulte [Exibir informações sobre conflitos em publicações de mesclagem &#40;Programação Transact-SQL de replicação&#41;](view-conflict-information-for-merge-publications.md).  
  
## <a name="options"></a>Opções  
 **Nome da coluna**  
 O nome de todas as colunas na tabela. Uma ou mais colunas podem ter dados conflitantes. Independentemente de quais colunas estejam em conflito, toda a linha vencedora substituirá toda a linha perdedora.  
  
 **Resolução Sugerida**  
 A resolução sugerida fornecida pelo resolvedor de conflitos para o artigo.  
  
 **Publicador**  
 O valor dos dados no Publicador.  
  
 **Assinante**  
 O valor dos dados no Assinante.  
  
 **Aceitar Sugestão**, **Aceitar Publicador**e **Aceitar Assinante**  
 Clique para aceitar a linha que será aplicada no Publicador ou no Assinante, dependendo de quem perderá o conflito. Se o Publicador perder o conflito, todos os outros Assinantes receberão a linha vencedora da próxima vez em que sincronizarem com o Publicador.  
  
 **Resolver conflitos restantes automaticamente**  
 Resolva todos os conflitos restantes usando a resolução sugerida fornecida pelo resolvedor de conflitos para o artigo.  
  
 **Registrar em log os detalhes do conflito para referência futura**  
 Registra os detalhes do conflito em tabelas do sistema.  
  
## <a name="see-also"></a>Consulte também  
 [Resolução interativa de conflitos](merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [Exibir e resolver conflitos de dados em publicações de mesclagem &#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Sincronizar uma assinatura usando o Gerenciador de Sincronização do Windows &#40;Gerenciador de Sincronização do Windows&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
