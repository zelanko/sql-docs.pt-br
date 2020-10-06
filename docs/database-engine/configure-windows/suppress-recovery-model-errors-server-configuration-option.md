---
description: Suprimir erros do modelo de recuperação – opção de configuração do servidor
title: Suprimir erros do modelo de recuperação – opção de configuração do servidor | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 942dfc62bd55d1843babb78d89b95ad602f3d938
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670739"
---
# <a name="suppress-recovery-model-errors-server-configuration-option"></a>Opção de configuração de suprimir erros do modelo de recuperação do servidor

[!INCLUDE[tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md](../../includes/tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md)]

Os [modelos de recuperação](../../relational-databases/backup-restore/recovery-models-sql-server.md) do SQL Server controlam a manutenção do log de transações. O modelo de recuperação completa garante que nenhum trabalho seja perdido devido a um arquivo de dados perdido ou danificado e dá suporte à recuperação para um ponto arbitrário no tempo de acordo com a política de retenção de backups. O modelo de recuperação completa é um padrão e é o único modelo de recuperação com suporte na Instância Gerenciada de SQL. Tentativas de alterar o modelo de recuperação na Instância Gerenciada de SQL retornam uma mensagem de erro.

Use a opção de configuração avançada **suprimir erros do modelo de recuperação** para especificar se os comandos para alterar o modelo de recuperação do banco de dados, executados na Instância Gerenciada de SQL, retornarão erros ou somente avisos. Quando essa opção é definida como 1 (ATIVADO) na Instância Gerenciada de SQL, a execução do comando ALTER DATABASE SET RECOVERY não altera o modelo de recuperação do banco de dados, mas não retorna um erro, e sim uma mensagem de aviso. Quando essa opção é definida como 0 (DESATIVADO) na Instância Gerenciada de SQL, a execução do comando ALTER DATABASE SET RECOVERY retorna uma mensagem de erro.

A opção **Suprimir erros do modelo de recuperação** é útil nos casos em que aplicativos herdados ou de terceiros tentam alterar o modelo de recuperação para log Simples ou Em massa, embora esse não seja um requisito crítico ou obrigatório. Quando a alteração do modelo de recuperação é o único obstáculo para o uso da Instância Gerenciada de SQL, a ativação da opção de configuração de suprimir erros do modelo de recuperação remove esse obstáculo. Essa opção é especialmente útil quando uma solução alternativa de alteração do código do aplicativo não é viável nem acessível.

## <a name="examples"></a>Exemplos

O exemplo a seguir habilita a supressão de mensagens de erro relacionadas à alteração do modelo de recuperação de banco de dados e executa o comando para alterar o modelo de recuperação do banco de dados, retornando somente um aviso. O modelo de recuperação não é de fato alterado. Substitua *my_database* pelo nome do banco de dados real.

```sql
-- Turn advanced configuration options on:
sp_configure 'show advanced options', 1 ;  
GO
RECONFIGURE ;  
GO

-- Enable suppression of error messages for recovery model change:
sp_configure 'suppress recovery model errors', 1 ;  
GO
RECONFIGURE ;  
GO

-- Execute command for changing recovery model to Simple:
ALTER DATABASE my_database SET RECOVERY SIMPLE;
GO
```

## <a name="see-also"></a>Confira também

[Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)