---
title: Índices de texto completo em colunas computadas persistentes não são permitidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text indexes
ms.assetid: cba737f7-b187-47d0-8458-23dc18d18aca
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d51500dca40ed039816b973cb4698971996e2b01
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116863"
---
# <a name="full-text-indexes-on-nonpersisted-computed-columns-are-not-allowed"></a>Índices de texto completo em colunas computadas não persistentes não são permitidos
  Não é possível criar índices de texto completo em colunas computadas imprecisas e não determinísticas. Essas colunas não podem ser usadas como colunas de tipo ou colunas de chave de texto completo.  
  
## <a name="description"></a>Description  
 No [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], um índice de texto completo pode ser criado usando-se uma coluna computada imprecisa e não determinística como coluna de tipo ou coluna de chave de texto completo. Não há mais suporte para essa funcionalidade. Quando você atualiza, índices de texto completo antigos, incompatíveis e sem-suporte são desabilitados.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Para habilitar índices de texto completo, modifique as definições das colunas para que elas sejam determinísticas e precisas.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  