---
title: "Verificar a configuração máxima de threads de trabalho | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c76c1cf549dfdba5babe5ae137f0c457a033dd5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="verify-max-worker-threads-setting"></a>Verificar a configuração máxima de threads de trabalho
  Esta regra verifica a opção do servidor de máximo de threads de trabalho para configurações potencialmente incorretas. A configuração da opção de máximo de threads de trabalho com um valor pequeno pode impedir que threads suficientes atendam às solicitações de entrada do cliente de maneira oportuna e, assim, causar uma "escassez de threads". Entretanto, a configuração da opção com um valor grande pode desperdiçar espaço de endereço, porque cada thread ativo consome até 4 KB em servidores de 64 bits.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Defina a opção max worker threads como 0. Isso permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine automaticamente o número correto de threads de trabalho ativos com base nas solicitações do usuário.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Configurar a opção max worker threads de configuração de servidor](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
