---
title: Não há suporte para índices de texto completo em bancos de dados mestre, tempdb e modelo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c0982614e41097ea51830212e0548efcc42c6ba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200746"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>Não há suporte para índices de texto completo em bancos de dados mestre, tempdb e modelo
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não aceita índices de texto completo em nenhum banco de dados do sistema.  
  
## <a name="description"></a>Description  
 No [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], havia suporte para índices de texto completo em bancos de dados mestre, tempdb e modelo.  
  
 Quaisquer catálogos de texto completo no mestre, tempdb e bancos de dados de modelo serão removidos durante a atualização.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
