---
title: Manter o valor padrão da opção de configuração de bloqueios | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: f214f05b-5f0b-4786-b2ad-b8b4b6e58d72
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a27f661fedb2df4fca70e5a0338136787f713895
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32952291"
---
# <a name="keep-the-locks-configuration-option-default-value"></a>Manutenção do valor padrão da opção configuração de bloqueios
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra verifica o valor da opção de configuração de bloqueios. Esta opção determina o número máximo de bloqueios disponíveis. Isto limita a quantidade de memória que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa para bloqueios. A configuração padrão em 0 permite que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] aloque e desaloque as estruturas de bloqueio de forma dinâmica, baseado nas alterações de requisitos de sistema.  
  
 Se os bloqueios forem diferentes de zero, os trabalhos de lote pararão e a mensagem "fora de bloqueios" de erro será gerada se o valor especificado for excedido.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Use o procedimento armazenado de sistema sp_configure para alterar o valor dos bloqueios para sua configuração padrão usando a seguinte instrução:  
  
```  
EXEC sp_configure 'locks', 0;  
```  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Configurar a opção locks de configuração de servidor](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md)  
  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
  
 [Artigo 271509 da Base de Dados de Conhecimento Microsoft](http://go.microsoft.com/fwlink/?linkid=117788)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
