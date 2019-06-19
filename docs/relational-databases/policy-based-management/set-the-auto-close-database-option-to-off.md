---
title: Definir a opção de banco de dados AUTO_CLOSE como OFF | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 6b9fda04dd570d0077b692b86937e401bac54e42
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62930893"
---
# <a name="set-the-autoclose-database-option-to-off"></a>Definir a opção do banco de dados AUTO_CLOSE como OFF
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra verifica se a opção AUTO_ CLOSE é definida como OFF. Quando a opção AUTO_CLOSE está definido como ON, pode causar degradação do desempenho em bancos de dados acessados com frequência, por causa do aumento da sobrecarga ao abrir e fechar o banco de dados após cada conexão. AUTO_CLOSE também libera o cache de procedimento depois de cada conexão.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Se um banco de dados for acessado frequentemente, defina sua opção de AUTO_CLOSE como OFF.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
