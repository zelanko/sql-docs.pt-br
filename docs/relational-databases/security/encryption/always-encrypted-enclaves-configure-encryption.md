---
title: Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros | Microsoft Docs
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
ms.openlocfilehash: b4f794e66e881ddeb36c724fc583d95a42bce33d
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411424"
---
# <a name="configure-column-encryption-in-place-using-always-encrypted-with-secure-enclaves"></a>Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros 
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

O [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) dá suporte a operações de criptografia em colunas de banco de dados in-loco em um enclave seguro no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A criptografia in-loco elimina a necessidade de mover os dados dessas operações para fora do banco de dados, tornando as operações criptográficas mais rápidas e confiáveis. 

> [!NOTE]
> Apesar dos benefícios de desempenho da criptografia in-loco, as operações criptográficas em tabelas grandes podem levar muito tempo e consumir recursos substanciais, podendo afetar e degradar o desempenho e a disponibilidade de seus aplicativos.

A criptografia in-loco também possibilita disparar operações criptográficas usando a instrução [ALTER TABLE ALTER COLUMN (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md), o que não é possível sem um enclave.

## <a name="prerequisites"></a>Prerequisites
As operações criptográficas com suporte e os requisitos para as chaves de criptografia de coluna, usadas para as operações, são:
- Criptografando uma coluna de texto não criptografado. A chave de criptografia de coluna usada para criptografar a coluna precisa ser habilitada para enclave.
- Criptografar novamente uma coluna criptografada criptografia usando um novo tipo de criptografia ou/e uma nova chave de criptografia de coluna. A chave de criptografia de coluna atual e a nova chave de criptografia de coluna (se forem diferentes da chave atual) precisam estar habilitadas para enclave.
- Descriptografar uma coluna criptografada – a chave de criptografia da coluna, que protege a coluna, precisa estar habilitada para enclave.

Confira [Gerenciar chaves para Always Encrypted com enclaves seguros](always-encrypted-enclaves-manage-keys.md) para obter informações sobre como garantir que as chaves de criptografia de coluna estejam habilitadas para enclave.

A criptografia in-loco também requer uma instância do SQL Server que tenha um enclave seguro inicializado corretamente. Confira [Configurar o tipo de enclave para a Opção de Configuração de Servidor Always Encrypted](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md).

Um usuário ou um aplicativo que dispara operações criptográficas deve ter permissões para fazer alterações de esquema na tabela que contém as colunas afetadas e acessar as chaves mestras de coluna envolvidas nas operações, bem como os metadados de chave relevantes no banco de dados.

Você só pode disparar a criptografia in-loco usando [ALTER TABLE ALTER COLUMN (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) do SQL Server Management Studio ou de seu aplicativo personalizado. Confira [Configurar criptografia de coluna in-loco com Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md).

> [!NOTE]
> Atualmente, o [assistente do Always Encrypted](always-encrypted-wizard.md) e o cmdlet [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/module/sqlserver/set-sqlcolumnencryption) não dão suporte à criptografia in-loco e sempre baixam os dados para operações criptográficas, mesmo que sua configuração atenda aos requisitos acima. 

## <a name="next-steps"></a>Próximas etapas
- [Configurar criptografia de coluna in-loco com Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)
- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md)
