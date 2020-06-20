---
title: Definir a opção de banco de dados AUTO_CLOSE como OFF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: db6cf5a3f82c3493a8732958594743104fccc968
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066684"
---
# <a name="set-the-auto_close-database-option-to-off"></a>Definir a opção do banco de dados AUTO_CLOSE como OFF
  Esta regra verifica se a opção AUTO_ CLOSE é definida como OFF. Quando a opção AUTO_CLOSE está definido como ON, pode causar degradação do desempenho em bancos de dados acessados com frequência, por causa do aumento da sobrecarga ao abrir e fechar o banco de dados após cada conexão. AUTO_CLOSE também libera o cache de procedimento depois de cada conexão.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Se um banco de dados for acessado frequentemente, defina sua opção de AUTO_CLOSE como OFF.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
