---
title: Opção de configuração de servidor ft notify bandwidth | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- ft notify bandwidth opion
- small memory buffers
- memory [SQL Server], buffers
ms.assetid: 9ca284c5-f3e0-4a67-a132-fff376ff0ffe
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: dc5839f699d55edf86c5e3e3f0eb001089a0a5dd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935271"
---
# <a name="ft-notify-bandwidth-server-configuration-option"></a>Opção ft notify bandwidth de configuração de servidor
  Use a opção **ft notify bandwidth** para especificar o tamanho a que pode crescer o pool de buffers de memória pequenos. Buffers de memória pequenos têm 64 KB (quilobytes). O valor do parâmetro *max* especifica o número máximo de buffers que o gerenciador de memória de texto completo deve manter em um pool de buffers pequenos. Se o `max` valor for zero, não haverá nenhum limite superior para o número de buffers que podem estar em um pool de buffers pequeno.  
  
 O valor do parâmetro **min** especifica o número mínimo de buffers de memória que deve ser mantido no pool de buffers de memória pequenos. Mediante solicitação do gerenciador de memória do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], todos os pools de buffers extras serão liberados, mas esse número mínimo de buffers será mantido. Se, contudo, o valor especificado de **min** for zero, todos os buffers de memória serão liberados.  
  
 Sob certas circunstâncias, o número de buffers alocados atualmente é menor que o valor especificado pelo parâmetro **min** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Opção de configuração de servidor ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
