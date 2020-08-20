---
description: Configurar criptografia de coluna in-loco com Transact-SQL
title: Configurar criptografia de coluna in-loco com Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 85729b4f194cedb1a0682387ab7047f332a2ceb8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490469"
---
# <a name="configure-column-encryption-in-place-with-transact-sql"></a>Configurar criptografia de coluna in-loco com Transact-SQL
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

Este artigo descreve como executar operações de criptografia in-loco em colunas usando o Always Encrypted com enclaves seguros com a [instrução ALTER TABLE](../../../odbc/microsoft/alter-table-statement.md)/`ALTER COLUMN`. Para obter informações básicas sobre a criptografia in-loco e pré-requisitos gerais, confira [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md).

Com a instrução `ALTER TABLE` ou `ALTER COLUMN`, você pode definir a configuração da criptografia de destino para uma coluna. Quando você executa a instrução, o enclave seguro do lado do servidor criptografa, criptografa novamente ou descriptografa os dados armazenados na coluna, dependendo da configuração de criptografia atual e de destino, especificada na definição de coluna na instrução. 
- Se a coluna não estiver criptografada no momento, ela será criptografada se você especificar a cláusula `ENCRYPTED WITH` na definição de coluna.
- Se a coluna estiver criptografada no momento, ela será descriptografada (convertida em uma coluna de texto não criptografado) se você não especificar a cláusula `ENCRYPTED WITH` na definição de coluna.
- Se a coluna estiver criptografada no momento, ela será criptografada novamente se você especificar a cláusula `ENCRYPTED WITH` e o tipo de criptografia de coluna especificada ou a chave de criptografia de coluna forem diferentes do tipo de criptografia ou da chave de criptografia de coluna usada no momento. 

> [!NOTE]
> Não é possível combinar operações criptográficas com outras alterações em uma única instrução `ALTER TABLE`/`ALTER COLUMN`, exceto para alterar a coluna para `NULL` ou `NOT NULL` ou alterar uma ordenação. Por exemplo, não é possível criptografar uma coluna E alterar um tipo de dados da coluna em uma única instrução `ALTER TABLE`/`ALTER COLUMN` do Transact-SQL. É necessário usar duas instruções separadas.

Como qualquer consulta que usa um enclave seguro no lado do servidor, uma instrução `ALTER TABLE`/`ALTER COLUMN` que dispara a criptografia in-loco deve ser enviada por uma conexão com o Always Encrypted e os cálculos de enclave habilitados. 

O restante deste artigo descreve como disparar a criptografia in-loco usando a instrução `ALTER TABLE`/`ALTER COLUMN` do SQL Server Management Studio. Como alternativa, você pode emitir `ALTER TABLE`/`ALTER COLUMN` do seu aplicativo. 

> [!NOTE]
> Atualmente, ferramentas diferentes do SSMS, incluindo o cmdlet [Invoke-Sqlcmd](https://docs.microsoft.com/powershell/module/sqlserver/invoke-sqlcmd) no módulo do SqlServer do PowerShell e [sqlcmd](../../../tools/sqlcmd-utility.md), não dão suporte ao uso de `ALTER TABLE`/`ALTER COLUMN` para operações criptográficas in-loco.

## <a name="perform-in-place-encryption-with-transact-sql-in-ssms"></a>Executar a criptografia in-loco com o Transact-SQL no SSMS
### <a name="pre-requisites"></a>Pré-requisitos
- Pré-requisitos descritos em [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md).
- SQL Server Management Studio 18.3 ou posterior.

### <a name="steps"></a>Etapas
1. Abra uma janela de consulta com Always Encrypted e cálculos de enclave habilitados na conexão de banco de dados. Para obter detalhes, confira [Habilitando e desabilitando Always Encrypted para uma conexão de banco de dados](always-encrypted-query-columns-ssms.md#en-dis).
2. Na janela de consulta, emita a instrução `ALTER TABLE`/`ALTER COLUMN`, especificando uma chave de criptografia de coluna habilitada para enclave na cláusula `ENCRYPTED WITH`. Se a coluna for de cadeia de caracteres (por exemplo, `char`, `varchar`, `nchar`, `nvarchar`), você também precisará alterar a ordenação para uma ordenação BIN2. 
    
    > [!NOTE]
    > Se a chave mestra de coluna estiver armazenada no Azure Key Vault, talvez seja solicitado que você entre no Azure.

3. Limpe o cache do plano para todos os lotes e procedimentos armazenados que acessam a tabela, para atualizar as informações de criptografia de parâmetros. 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > Se você não remover o plano da consulta afetada do cache, a primeira execução da consulta após a criptografia poderá falhar.

    > [!NOTE]
    > Use `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` ou `DBCC FREEPROCCACHE` para limpar o cache de planos com cuidado, pois isso pode resultar na degradação temporária do desempenho de consulta. Para minimizar o impacto negativo da limpeza do cache, você pode remover seletivamente somente os planos das consultas afetadas.

4.  Chame [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) para atualizar os metadados dos parâmetros de cada módulo (procedimento armazenado, função, exibição, gatilho) que persistiu em [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) e possa ter sido invalidado criptografando as colunas.

### <a name="examples"></a>Exemplos
#### <a name="encrypting-a-column-in-place"></a>Criptografar uma coluna in-loco
O exemplo abaixo pressupõe que:
- `CEK1` é uma chave de criptografia de coluna habilitada para enclave.
- a coluna `SSN` é de texto sem formatação e atualmente está usando a ordenação de banco de dados padrão, como uma ordenação Latin1, não BIN2 (por exemplo, `Latin1_General_CI_AI_KS_WS`).

A instrução criptografa a coluna `SSN` usando criptografia aleatória e a chave de criptografia de coluna habilitada para enclave no local. Ela também substitui a ordenação do banco de dados padrão pela ordenação BIN2 correspondente (na mesma página de código).

A operação é executada online (`ONLINE = ON`). Observe também que a chamada para `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE`, que recria os planos das consultas, é afetada pela alteração do esquema de tabela.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char] COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
WITH
(ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

#### <a name="re-encrypt-a-column-in-place-to-change-encryption-type"></a>Criptografar novamente uma coluna in-loco para alterar o tipo de criptografia
O exemplo abaixo pressupõe que:
- A coluna `SSN` foi criptografada usando criptografia determinística e uma chave de criptografia de coluna habilitada para enclave, `CEK1`.
- A ordenação atual, definida no nível da coluna, é `Latin1_General_BIN2`.

A instrução abaixo criptografa novamente a coluna usando criptografia aleatória e a mesma chave (`CEK1`)

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

#### <a name="re-encrypt-a-column-in-place-to-rotate-a-column-encryption-key"></a>Criptografar novamente uma coluna in-loco para girar uma chave de criptografia de coluna
O exemplo abaixo pressupõe que:
- A coluna `SSN` foi criptografada usando criptografia aleatória e uma chave de criptografia de coluna habilitada para enclave, `CEK1`.
- `CEK2` é uma chave de criptografia de coluna habilitada para enclave (diferente de `CEK1`).
- A ordenação atual, definida no nível da coluna, é `Latin1_General_BIN2`.

A instrução abaixo criptografa novamente a coluna com `CEK2`.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK2]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```
#### <a name="decrypt-a-column-in-place"></a>Descriptografar uma coluna no local
O exemplo abaixo pressupõe que:
- A coluna `SSN` foi criptografada usando uma chave de criptografia de coluna habilitada para enclave.
- A ordenação atual, definida no nível da coluna, é `Latin1_General_BIN2`.

A instrução abaixo descriptografa a coluna (e mantém a ordenação inalterada – como alternativa, você pode optar por alterar a ordenação, por exemplo, para uma ordenação não BIN2 na mesma instrução).

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

## <a name="next-steps"></a>Próximas etapas
- [Consultar colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-query-columns.md)
- [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)
- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>Consulte Também  
- [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md)
- [Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)
