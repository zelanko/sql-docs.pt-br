---
title: Definir a opção de banco de dados AUTO_SHRINK como OFF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c81885e5a3aaec197b8963c2e868b6f65a0b0544
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691517"
---
# <a name="set-the-autoshrink-database-option-to-off"></a>Definir a opção do banco de dados AUTO_SHRINK como OFF
  Esta regra verifica se a opção de banco de dados AUTO_SHRINK é definida como OFF. Reduzir e expandir um banco de dados com frequência pode causar a fragmentação física.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Defina a opção do banco de dados AUTO_SHRINK como OFF. Se você souber que o espaço que está recuperando não será necessário no futuro, poderá recuperá-lo reduzindo o banco de dados manualmente.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 Artigo da Base de Conhecimentos Microsoft [315512](https://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
