---
title: Transações XTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96d60ae8fc176fc1fc108d907f33f01877795955
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805418"
---
# <a name="xtp-transactions"></a>Transações de XTP
  O objeto de desempenho Transações de XTP contém os contadores relacionados às transações do mecanismo de XTP no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta tabela descreve os contadores **Transações de XTP** .  
  
|Contador|Descrição|  
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
 [XTP &#40;OLTP in-memory&#41; contadores de desempenho](../../integration-services/performance/performance-counters.md)  
  
  
