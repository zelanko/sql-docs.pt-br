---
title: Não há suporte para índices de texto completo em bancos de dados mestre, tempdb e modelo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fbd5e3133ed87fed9bdaf6d668df62c6471df766
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012462"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>Não há suporte para índices de texto completo em bancos de dados mestre, tempdb e modelo
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não aceita índices de texto completo em nenhum banco de dados do sistema.  
  
## <a name="description"></a>Descrição  
 No [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], havia suporte para índices de texto completo em bancos de dados mestre, tempdb e modelo.  
  
 Todos os catálogos de texto completo nos bancos de dados mestre, tempdb e modelo são removidos durante a atualização.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
