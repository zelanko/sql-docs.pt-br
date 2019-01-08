---
title: MSSQL_ENG021075 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021075 error
ms.assetid: c8c29543-d1f6-49d5-b6c8-e8c3aa373090
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b97942c7fae84a43b30ce848af593a96ea0f4714
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52778218"
---
# <a name="mssqleng021075"></a>MSSQL_ENG021075
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21075|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O instantâneo inicial da publicação '%s' ainda não está disponível.|  
  
## <a name="explanation"></a>Explicação  
 O erro MSSQL_ENG021075 pode ser gerado se o Distribution Agent ou o Merge Agent for iniciado antes do Snapshot Agent terminar de gerar o instantâneo.  
  
## <a name="user-action"></a>Ação do usuário  
 Se o Snapshot Agent da publicação não for iniciado até que a assinatura seja criada, ou se não tiver sido iniciado desde que você optou por reiniciar a assinatura, inicie o Snapshot Agent e aguarde o início do Distribution Agent ou do Merge Agent. Para obter mais informações, consulte [Create and Apply the Snapshot](create-and-apply-the-snapshot.md) (Criar e aplicar o instantâneo).  
  
 Se o Agente de Instantâneo não for concluído, verifique o histórico do Agente de Instantâneo em relação a erros e faça o diagnóstico. Para obter informações sobre como exibir o status do agente e detalhes de erro no Replication Monitor, consulte [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
 Se o erro continuar ocorrendo, aumente o log do agente e especifique um arquivo de saída para o log. Dependendo do contexto do erro, isso poderá fornecer as etapas que levaram ao erro e/ou as mensagens de erros adicionais.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
