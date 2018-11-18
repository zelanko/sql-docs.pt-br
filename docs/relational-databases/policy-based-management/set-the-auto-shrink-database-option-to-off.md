---
title: Definir a opção de banco de dados AUTO_SHRINK como OFF | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: c48e0671052d612a52703aa7d367e03257cf1e14
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51667335"
---
# <a name="set-the-autoshrink-database-option-to-off"></a>Definir a opção do banco de dados AUTO_SHRINK como OFF
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra verifica se a opção de banco de dados AUTO_SHRINK é definida como OFF. Reduzir e expandir um banco de dados com frequência pode causar a fragmentação física.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Defina a opção do banco de dados AUTO_SHRINK como OFF. Se você souber que o espaço que está recuperando não será necessário no futuro, poderá recuperá-lo reduzindo o banco de dados manualmente.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 Artigo da Base de Conhecimentos Microsoft [315512](https://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
