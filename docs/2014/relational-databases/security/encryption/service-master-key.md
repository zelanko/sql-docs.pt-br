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
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 6a802cfadfa48c7dbba7479ca169daedf70fe8b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74957130"
---
# <a name="service-master-key"></a>SMK (chave mestra de serviço)
  A chave mestra de serviço é a raiz da hierarquia de criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Ela é gerada automaticamente na primeira vez que é necessária para criptografar outra chave. Por padrão, a Chave Mestra do Serviço é criptografada com o uso da API de proteção aos dados do Windows e da chave da máquina local. A chave mestra de serviço só pode ser aberta pela conta de serviço do Windows na qual ela foi criada ou por uma entidade que tenha acesso ao nome e à senha da conta de serviço.  
  
 Gerar novamente ou restaurar a chave mestra de serviço envolve a descriptografia e uma nova criptografia da hierarquia de criptografia completa. Essa operação de uso intensivo de recursos deve ser agendada durante um período de baixa demanda, a menos que a chave mestra esteja comprometida.  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usa o algoritmo de criptografia AES para proteger a SMK (chave mestra de serviço) e a DMK (chave mestra de banco de dados). O AES é um algoritmo de criptografia mais novo que o 3DES usado em versões anteriores. Depois de atualizar uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] , o SMK e o DMK devem ser regenerados para atualizar as chave mestras para AES. Para obter mais informações sobre como regenerar a SMK, veja [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql) e [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql).  
  
## <a name="best-practice"></a>Melhor prática  
 Faça backup da chave mestra de serviço e armazene a cópia com backup em um local externo, seguro.  
  
## <a name="related-tasks"></a>Related Tasks  
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-service-master-key-transact-sql)  
  
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-service-master-key-transact-sql)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql)  
  
## <a name="see-also"></a>Consulte Também  
 [Hierarquia de criptografia](encryption-hierarchy.md)  
  
  
