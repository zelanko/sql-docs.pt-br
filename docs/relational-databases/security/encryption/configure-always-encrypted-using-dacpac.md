---
title: Configurar a criptografia de coluna usando o Always Encrypted com um pacote de DAC | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fc10c556999d843456728289acb72bddb3b0784e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765137"
---
# <a name="configure-column-encryption-using-always-encrypted-with-a-dac-package"></a>Configurar a criptografia de coluna usando o Always Encrypted com um pacote de DAC 
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

Um [pacote de DAC (aplicativo da camada de dados)](../../data-tier-applications/data-tier-applications.md), também conhecido como DACPAC, é uma unidade portátil de implantação de banco de dados do SQL Server que define todos os objetos do SQL Server, incluindo tabelas e colunas dentro das tabelas. Quando você publica um DACPAC em um banco de dados (ao atualizar um banco de dados usando um DACPAC), o esquema do banco de dados de destino é atualizado para corresponder ao esquema no DACPAC. Publique um DACPAC usando o [Assistente para Atualizar Aplicativo da Camada de Dados](../../data-tier-applications/upgrade-a-data-tier-application.md#UsingDACUpgradeWizard) no SQL Server Management Studio, no [PowerShell](../../data-tier-applications/upgrade-a-data-tier-application.md#UpgradeDACPowerShell) ou no [sqlpackage](../../../tools/sqlpackage.md#publish-parameters-properties-and-sqlcmd-variables).

Este artigo aborda considerações especiais sobre a atualização de um banco de dados quando o DACPAC e/ou o banco de dados de destino contêm colunas protegidas com o [Always Encrypted](always-encrypted-database-engine.md). Se o esquema de criptografia para uma coluna no DACPAC é diferente do esquema de criptografia para uma coluna existente no banco de dados de destino, a publicação do DACPAC resulta na criptografia, na descriptografia ou na nova criptografia dos dados armazenados na coluna. Confira a tabela a seguir para obter detalhes.

| Condição|Ação|
|:---|:---|
|A coluna está criptografada no DACPAC e não está criptografada no banco de dados.| Os dados na coluna serão criptografados.|
|A coluna não está criptografada no DACPAC e está criptografada no banco de dados.| Os dados na coluna serão descriptografados (a criptografia será removida da coluna).|
| A coluna está criptografada no DACPAC e no banco de dados, mas a coluna no DACPAC usa um tipo de criptografia diferente e/ou uma chave de criptografia de coluna diferente da coluna correspondente no banco de dados.|Os dados na coluna serão descriptografados e criptografados novamente para corresponder à configuração de criptografia no DACPAC.|

A implantação de um pacote de DAC também pode resultar na criação ou na remoção de objetos de metadados para chaves mestras de coluna ou chaves de criptografia de coluna do Always Encrypted.

## <a name="performance-considerations"></a>Considerações sobre o desempenho
Para executar operações de criptografia, uma ferramenta usada para implantar um DACPAC precisa mover os dados para fora do banco de dados. A ferramenta cria tabelas com a configuração de criptografia desejada no banco de dados, carrega todos os dados das tabelas originais, executa as operações de criptografia solicitadas, carrega os dados nas novas tabelas e, em seguida, troca as tabelas originais pelas novas tabelas. A execução de operações criptográficas pode levar muito tempo. Durante esse tempo, o banco de dados não estará disponível para gravar transações. 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> Se estiver usando [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] e sua instância do SQL Server estiver configurada com um enclave seguro, você poderá executar operações criptográficas in-loco, sem mover os dados para fora do banco de dados. Confira [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md). Observe que a criptografia in-loco não está disponível para implantações de DACPAC.

::: moniker-end

## <a name="permissions-for-publishing-a-dac-package-if-always-encrypted-is-set-up"></a>Permissões para publicar um pacote de DAC se o Always Encrypted está configurado

Para publicar um pacote de DAC se o Always Encrypted está configurado no DACPAC e/ou no banco de dados de destino, talvez você precise ter algumas ou todas as permissões abaixo, dependendo das diferenças entre o esquema no DACPAC e o esquema do banco de dados de destino.

*ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*, *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION*

Se a operação de atualização disparar uma operação de criptografia de dados, você também precisará ser capaz de acessar as chaves mestras de coluna configuradas para as colunas afetadas:

- **Repositório de Certificados – Computador local**: você precisa ter acesso de leitura ao certificado que é usado como chave mestra da coluna ou ser o administrador do computador.
- **Azure Key Vault**: você precisa das permissões *create*, *get*, *unwrapKey*, *wrapKey*, *sign* e *verify* no cofre que contém a chave mestra da coluna.
- **Provedor do Repositório de Chaves (CNG)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted). 

 
## <a name="next-steps"></a>Próximas etapas
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)
- [Consultar colunas usando o Always Encrypted com o SQL Server Management Studio](always-encrypted-query-columns-ssms.md)

## <a name="see-also"></a>Consulte Também  
 - [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
 - [Visão geral do gerenciamento de chaves do Always Encrypted](overview-of-key-management-for-always-encrypted.md) 
 - [Configurar o Always Encrypted usando o SQL Server Management Studio](configure-always-encrypted-using-sql-server-management-studio.md)
 - [Configurar a criptografia de coluna usando o Assistente do Always Encrypted](always-encrypted-wizard.md)
 - [Configurar a criptografia de coluna usando o Always Encrypted com o PowerShell](configure-column-encryption-using-powershell.md)
 
