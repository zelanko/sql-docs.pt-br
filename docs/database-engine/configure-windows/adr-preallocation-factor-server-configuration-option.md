---
title: Opção de configuração do Fator de Pré-alocação da ADR | Microsoft Docs
description: Explica a definição de configuração da instância do SQL Server para o Fator de Pré-alocação da ADR.
ms.custom: ''
ms.date: 06/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ADR Preallocation Factor
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4e53c7c9d0d128c1697a301fc013469f5ac34c00
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85698176"
---
# <a name="adr-preallocation-factor-configuration-option"></a>Opção de configuração do Fator de Pré-alocação da ADR

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Introduzida no SQL Server 2019.

Essa definição de configuração é necessária para a [Recuperação Acelerada de Banco de Dados](../../relational-databases/accelerated-database-recovery-concepts.md).

A ADR (Recuperação Acelerada de Banco de Dados) mantém versões dos dados para fins de recuperação. Essas versões são geradas como parte de várias operações de DML (linguagem de manipulação de dados). As versões são armazenadas em uma tabela interna chamada PVS (armazenamento de versão persistente). 

## <a name="remarks"></a>Comentários  

O desempenho poderá diminuir se as páginas forem alocadas para a tabela de PVS como parte das operações de DML em primeiro plano do usuário. Para resolver isso, há um thread em segundo plano que pré-aloca as páginas e as mantém prontamente disponíveis para transações de DML. O desempenho é melhor quando o thread em segundo plano pré-aloca um número suficiente de páginas e o percentual de alocações de PVS em primeiro plano é próximo de 0. O log de erros conterá inteiros com a marca `PreallocatePVS` se o percentual ficar alto e estiver afetando o desempenho.

O número de páginas pré-alocadas pelo thread em segundo plano baseia-se em várias heurísticas de carga de trabalho, mas aloca páginas, em grande medida, em partes de 512 páginas. O fator de pré-alocação da ADR é um múltiplo dessa parte. Por padrão, o fator é 4. Isso significa que ele pré-alocará 2.048 páginas simultaneamente quando necessário. 

Embora o thread em segundo plano leve os padrões de carga de trabalho em consideração, esse fator pode ser aumentado, se necessário, para aprimorar o desempenho.

> [!CAUTION]
> Se a pré-alocação do PVS for aumentada em demasia, ela disputará com outras alocações no sistema e poderá, na realidade, reduzir o desempenho geral
>
> Antes de modificar essa configuração, teste o desempenho geral do sistema.

## <a name="examples"></a>Exemplos  

O exemplo a seguir define o fator de pré-alocação como 4.

```tsql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO 
sp_configure 'ADR Preallocation Factor', 4;
RECONFIGURE;
GO
```

## <a name="see-also"></a>Consulte Também  

- [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [Recuperação acelerada de banco de dados](../../relational-databases/accelerated-database-recovery-concepts.md)
- [Gerenciar Recuperação Acelerada de Banco de Dados](../../relational-databases/accelerated-database-recovery-management.md)