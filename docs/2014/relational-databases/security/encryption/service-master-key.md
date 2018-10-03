---
title: Chave mestra de serviço | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server]
- service master key [SQL Server], about service master key
ms.assetid: 85f2095d-2590-4f59-8a29-7e100edd02bb
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 6ea074466c8075b7fb1746b7d3eb8741425b44c5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147326"
---
# <a name="service-master-key"></a>SMK (chave mestra de serviço)
  A chave mestra de serviço é a raiz da hierarquia de criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Ela é gerada automaticamente na primeira vez que é necessária para criptografar outra chave. Por padrão, a Chave Mestra do Serviço é criptografada com o uso da API de proteção aos dados do Windows e da chave da máquina local. A chave mestra de serviço só pode ser aberta pela conta de serviço do Windows na qual ela foi criada ou por uma entidade que tenha acesso ao nome e à senha da conta de serviço.  
  
 Gerar novamente ou restaurar a chave mestra de serviço envolve a descriptografia e uma nova criptografia da hierarquia de criptografia completa. Essa operação de uso intensivo de recursos deve ser agendada durante um período de baixa demanda, a menos que a chave mestra esteja comprometida.  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usa o algoritmo de criptografia AES para proteger a SMK (chave mestra de serviço) e a DMK (chave mestra de banco de dados). O AES é um algoritmo de criptografia mais novo que o 3DES usado em versões anteriores. Depois de atualizar uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] , o SMK e o DMK devem ser regenerados para atualizar as chave mestras para AES. Para obter mais informações sobre como regenerar a SMK, veja [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql) e [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql).  
  
## <a name="best-practice"></a>Prática recomendada  
 Faça backup da chave mestra de serviço e armazene a cópia com backup em um local externo, seguro.  
  
## <a name="related-tasks"></a>Related Tasks  
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-service-master-key-transact-sql)  
  
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-service-master-key-transact-sql)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql)  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquia de criptografia](encryption-hierarchy.md)  
  
  
