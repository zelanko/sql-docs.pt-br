---
title: "Opção de configuração de servidor ft crawl bandwidth | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- large memory buffers
- memory [SQL Server], buffers
- ft crawl bandwidth option
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bbd5b1bb9be83e917adc6d0e2a392601dd57b7ab
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="ft-crawl-bandwidth-server-configuration-option"></a>Opção de configuração de servidor ft crawl bandwidth
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Use a opção **ft crawl bandwidth** para especificar o tamanho até o qual o pool de buffers de memória grandes pode se expandir. Buffers de memória grandes têm o tamanho de 4 MB (megabytes). O valor do parâmetro **max** especifica o número máximo de buffers que o gerenciador de memória de texto completo deve manter em um pool de buffers grandes. Se o valor de **max** for zero, não haverá limite máximo ao número de buffers no pool de buffers grandes.  
  
 O valor do parâmetro **min** especifica o número mínimo de buffers de memória que deve ser mantido no pool de buffers de memória grandes. Mediante solicitação do gerenciador de memória do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , todos os pools de buffers extra serão liberados, mas esse número mínimo de buffers será mantido. Se, contudo, o valor especificado de **min** for zero, todos os buffers de memória serão liberados.  
  
 Em algumas circunstâncias, o número de buffers alocados atualmente é menor que o valor especificado pelo parâmetro **min** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Opção de configuração de servidor ft notify bandwidth](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
