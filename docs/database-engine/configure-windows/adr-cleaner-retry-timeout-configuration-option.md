---
title: " Opção de configuração do tempo limite (min) de nova tentativa do limpador da ADR | Microsoft Docs"
description: Explica a definição de configuração da instância do SQL Server para o tempo limite de nova tentativa do limpador da ADR.
ms.custom: ''
ms.date: 06/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ADR cleaner retry timeout (min)
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 25d7df032b0606a324d98d14258cbbd40602bae7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85698159"
---
# <a name="adr-cleaner-retry-timeout-min-configuration-option"></a>Opção de configuração do tempo limite (min) de nova tentativa do limpador da ADR

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Introduzida no SQL Server 2019.

Essa definição de configuração é necessária para a [Recuperação Acelerada de Banco de Dados](../../relational-databases/accelerated-database-recovery-concepts.md). O limpador é o processo assíncrono que é ativado periodicamente e limpa as versões de página que não são necessárias.

Ocasionalmente, ao realizar a varredura, o limpador enfrenta problemas ao adquirir bloqueios no nível do objeto devido a conflitos com a carga de trabalho do usuário. Ela acompanha essas páginas em uma lista separada. O tempo limite de nova tentativa do limpador da ADR (com valor padrão 15) controla a quantidade de tempo que o limpador passaria exclusivamente repetindo a aquisição de bloqueios de objeto e a limpeza da página antes de abandonar a varredura. A conclusão de uma varredura com 100% de sucesso é essencial para manter o crescimento de transações anuladas no mapa de transações anuladas. Se a lista separada não puder ser limpa no tempo limite prescrito, a varredura atual será abandonada e a próxima varredura será iniciada.

## <a name="remarks"></a>Comentários  

O limpador é um thread único no SQL Server 2019 e, portanto, uma instância do SQL Server pode trabalhar em um banco de dados de cada vez. Se a instância tiver mais de um banco de dados de usuário com a ADR habilitada, não aumente o tempo limite para um valor grande, pois isso pode atrasar a limpeza em um banco de dados enquanto a nova tentativa está acontecendo em outro banco de dados.

## <a name="examples"></a>Exemplos

Os exemplos a seguir definem o tempo limite de nova tentativa do limpador.

```tsql
sp_configure 'show advanced options', 1;  
RECONFIGURE;
GO 
sp_configure 'ADR cleaner retry timeout', 15;  
RECONFIGURE;  
GO  
```  

## <a name="see-also"></a>Consulte Também  

- [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [Recuperação acelerada de banco de dados](../../relational-databases/accelerated-database-recovery-concepts.md)
- [Gerenciar Recuperação Acelerada de Banco de Dados](../../relational-databases/accelerated-database-recovery-management.md)