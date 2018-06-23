---
title: Transações de XTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6b890ec229755db9c6ee9b292bf632d110e9c189
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012673"
---
# <a name="xtp-transactions"></a>Transações de XTP
  O objeto de desempenho Transações de XTP contém os contadores relacionados às transações do mecanismo de XTP no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta tabela descreve os contadores **Transações de XTP** .  
  
|Contador|Description|  
|-------------|-----------------|  
|**Anulações em cascata/s**|O número de transações que foram revertidas devido a uma reversão de dependência de confirmação (em média), por segundo.|  
|**Dependências de confirmação realizadas/s**|O número de dependências de confirmação realizadas por transações (em média), por segundo.|  
|**Transações somente leitura preparadas/s**|O número de transações somente leitura que foram preparadas para o processamento da confirmação, por segundo.|  
|**Atualizações de ponto de salvamento/s**|O número de vezes que um ponto de salvamento foi “atualizado”, (em média), por segundo. Uma atualização de ponto de salvamento é quando um ponto de salvamento existente é redefinido para o momento atual no tempo de vida da transação.|  
|**Reversões de ponto de salvamento/s**|O número de vezes que uma transação foi revertida para um ponto de salvamento (em média), por segundo.|  
|**Pontos de salvamento criados/s**|O número de pontos de salvamento criados (em média), por segundo.|  
|**Falha de validação de transação/s**|O número de transações que falharam no processamento de validação (em média), por segundo.|  
|**Transações anuladas por usuário/s**|O número de transações que foram anuladas pelo usuário (em média), por segundo.|  
|**Transações anuladas/s**|O número de transações que foram anuladas (pelo usuário e pelo sistema) em média, por segundo.|  
|**Transações criadas/s**|O número de transações criadas no sistema (em média), por segundo.<br /><br /> As transações de XTP são contadas diferentemente de transações baseadas em disco (conforme refletido em bancos de dados:transações/s). Por exemplo, transações criadas/s contam como transações somente leitura, mas isso não ocorre com bancos de dados:transações/s.|  
  
## <a name="see-also"></a>Consulte também  
 [XTP &#40;OLTP na memória&#41; contadores de desempenho](../../integration-services/performance/performance-counters.md)  
  
  