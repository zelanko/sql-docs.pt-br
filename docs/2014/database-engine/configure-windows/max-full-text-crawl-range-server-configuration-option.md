---
title: Opção de configuração de servidor max full-text crawl range | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- crawls [full-text search]
- max full-text crawl range option
ms.assetid: a49de86b-0891-4dcd-89c0-ead30aab00e0
caps.latest.revision: 23
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a5a1903dfab71b78923a7747cf7a947d83e023e3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020995"
---
# <a name="max-full-text-crawl-range-server-configuration-option"></a>Opção max full-text crawl range de configuração de servidor
  Use a opção **max full-text crawl range** para otimizar a utilização de CPU, o que melhora o desempenho durante um rastreamento completo. Usando esta opção, é possível especificar o número de partições que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve usar durante um rastreamento de índice completo. Por exemplo, se houver muitas CPUs e sua utilização não for a ideal, você pode aumentar o valor máximo dessa opção. Além dessa opção, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa vários outros fatores, como o número de linhas na tabela e o número de CPUs, para determinar o número real de partições usadas.  
  
 O valor padrão desta opção é 4; o valor mínimo é 1 e o valor máximo, 256. As alterações feitas nesta opção afetam somente os rastreamentos subsequentes. Os rastreamentos em andamento não serão afetados por alterações na configuração desta opção.  
  
 A opção **max full-text crawl range** é uma opção avançada. Se você estiver usando o procedimento armazenado do sistema **sp_configure** para alterar a configuração, só será possível alterar **max full-text crawl range** quando **show advanced options** for definido como 1. A configuração entra em vigor imediatamente sem a reinicialização do servidor.  
  
## <a name="see-also"></a>Consulte também  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
