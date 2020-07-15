---
title: Definir a opção de banco de dados AUTO_CLOSE como OFF | Microsoft Docs
description: Verifique se a opção AUTO_CLOSE está definida como OFF. A opção AUTO_CLOSE tem implicações para o desempenho no SQL Server.
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
ms.openlocfilehash: 0dbcc137a97af6d447dafd44c71bdb8181c69577
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774202"
---
# <a name="set-the-auto_close-database-option-to-off"></a>Definir a opção do banco de dados AUTO_CLOSE como OFF
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regra verifica se a opção AUTO_ CLOSE é definida como OFF. Quando a opção AUTO_CLOSE está definido como ON, pode causar degradação do desempenho em bancos de dados acessados com frequência, por causa do aumento da sobrecarga ao abrir e fechar o banco de dados após cada conexão. AUTO_CLOSE também libera o cache de procedimento depois de cada conexão.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Se um banco de dados for acessado frequentemente, defina sua opção de AUTO_CLOSE como OFF.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
