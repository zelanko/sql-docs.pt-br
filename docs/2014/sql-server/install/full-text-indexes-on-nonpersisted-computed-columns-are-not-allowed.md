---
title: Índices de texto completo em colunas computadas persistentes não são permitidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: cba737f7-b187-47d0-8458-23dc18d18aca
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 417ca3c2e5e477960c4c905543f3a712a5ec7453
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095166"
---
# <a name="full-text-indexes-on-nonpersisted-computed-columns-are-not-allowed"></a>Índices de texto completo em colunas computadas não persistentes não são permitidos
  Não é possível criar índices de texto completo em colunas computadas imprecisas e não determinísticas. Essas colunas não podem ser usadas como colunas de tipo ou colunas de chave de texto completo.  
  
## <a name="description"></a>Descrição  
 No [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], um índice de texto completo pode ser criado usando-se uma coluna computada imprecisa e não determinística como coluna de tipo ou coluna de chave de texto completo. Não há mais suporte para essa funcionalidade. Quando você atualiza, índices de texto completo antigos, incompatíveis e sem-suporte são desabilitados.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Para habilitar índices de texto completo, modifique as definições das colunas para que elas sejam determinísticas e precisas.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
