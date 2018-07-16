---
title: Escolher um resolvedor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default conflict resolver
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: b7dec3fa-d9d9-409d-b946-f9b9a3202829
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 63bacbfaee08750811f9a0c2de4fb9c34f629c54
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172737"
---
# <a name="choose-a-resolver"></a>Escolher um resolvedor
  Ao escolher um resolvedor, considere a importância da resolução de conflito em sua aplicação e se você pode usar o resolvedor padrão baseado em prioridades ou se precisa usar um resolvedor de artigo.  
  
 Caso seus dados estejam particionados sem usuários múltiplos que gravam nas mesmas partições, e caso sua topologia de replicação seja relativamente básica (um Publicador e alguns Assinantes), os conflitos devem ser raros ou inexistentes. Nesses ambientes, você provavelmente não precisa de uma estratégia de resolução de conflito complexa. É recomendada uma estratégia que use as configurações padrão para resolução de conflito, utilizando assinaturas de cliente e uma primeira alteração na política de vitórias. Se a topologia for mais complexa (usando Assinantes de republicação, por exemplo), as assinaturas de servidor com prioridades específicas podem ser mais apropriadas.  
  
 Um resolvedor de artigo é recomendado caso as necessidades corporativas exijam uma solução mais personalizada do que a disponível com o resolvedor padrão. Se você optar por usar um resolvedor de artigo, será recomendável usar um manipulador de lógica de negócios. Para obter mais informações, consulte [Executar lógica de negócios durante a sincronizações de mesclagem](execute-business-logic-during-merge-synchronization.md).  
  
 Em última análise, escolher usar um resolvedor padrão ou um resolvedor de artigo deve ter por base os dados e as necessidades da lógica corporativa do aplicativo. Por exemplo, considere funcionários que inserem dados de classificação de clientes em um conjunto de tabelas não particionadas para diferentes Assinantes; os funcionários abrangem várias categorias de emprego (gerentes de filiais, gerentes de linha, vendedores) e a categoria emprego determina quais dados devem ter prioridade. Nesse caso, um resolvedor de artigo que utilize dados de categorias de emprego pode ser construído a partir do artigo para determinar o vencedor se ocorrer um conflito.  
  
 Se os conflitos tendem a acontecer com alguma frequência, estas são as decisões mais importantes que você deve considerar ao implementar uma estratégia de resolução de conflito.  
  
|Problema de resolução de conflito|Recomendação|  
|-------------------------------|--------------------|  
|Categorias diferentes de usuários requerem valores de prioridade diferentes.|Use o resolvedor padrão e crie assinaturas de servidor com valores de prioridade diferentes.<br /><br /> -Ou-<br /><br /> Use um resolvedor de artigo que reconheça uma coluna de valor de autoridade no artigo para ajudar a resolver um conflito.|  
|Necessária uma primeira alteração na solução de conflito de vitórias.|Use o resolvedor padrão e crie assinaturas de cliente.|  
|São aceitáveis múltiplos usuários que alteram a mesma linha de dados, desde que nenhuma alteração conflitante seja feita na mesma coluna.|Use o resolvedor padrão ou um resolvedor de artigo com controle em nível de coluna habilitado.|  
|Sinalize várias alterações para qualquer valor em uma linha como um conflito.|Use o resolvedor padrão ou um resolvedor de artigo com controle em nível de linha.|  
|Sinalize múltiplas alterações para qualquer valor em um registro lógico como um conflito.|Use o resolvedor padrão com controle em nível de registro lógico (o recurso registro lógico não oferece suporte a resolvedores de cliente ou manipuladores de lógica de negócios).|  
|Os dados de resultado de conflito precisam ser diferentes dos dados de conflito originais.|Use um resolvedor de artigo que calcule valores novos.|  
  
## <a name="see-also"></a>Consulte também  
 [Detectando e solucionando conflitos em registros lógicos](advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Republicar dados](../republish-data.md)  
  
  
