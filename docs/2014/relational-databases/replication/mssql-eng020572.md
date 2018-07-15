---
title: MSSQL_ENG020572 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020572 error
ms.assetid: 636566db-ffcf-4109-8c11-15b8c7cb9cd9
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 653aaa002ee37f7c7cdd3aeea7983486f35d1fcd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37188313"
---
# <a name="mssqleng020572"></a>MSSQL_ENG020572
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|20572|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|A assinatura do assinante '%s' para o artigo '%s' na publicação '%s' foi reiniciada após uma falha na validação.|  
  
## <a name="explanation"></a>Explicação  
 Os dados no Assinante foram validados de acordo com os dados no Publicador, e os dados não corresponderam, portanto, houve falha na validação. Quando você especificou que a validação deveria ser realizada, selecionou a opção de reinicialização da assinatura no caso de falha de validação. Reinicializar uma assinatura envolve a aplicação de um novo instantâneo no Assinante. Para obter mais informações sobre validação, consulte [Validate Replicated Data](validate-replicated-data.md).  
  
## <a name="user-action"></a>Ação do usuário  
 Dados no Publicador e no Assinante serão correspondentes após a aplicação de um novo instantâneo no Assinante.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
