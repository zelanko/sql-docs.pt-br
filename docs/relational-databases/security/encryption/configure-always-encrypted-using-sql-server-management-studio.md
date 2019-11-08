---
title: Configurar o Always Encrypted usando o SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
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
ms.openlocfilehash: 6ff7ef354fdf3118f68c22bf2ad927070bf8e4b6
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594429"
---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>Configurar o Always Encrypted usando o SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Este artigo descreve as tarefas para configurar o Always Encrypted e gerenciar bancos de dados que usam o Always Encrypted como [SSMS (SQL Server Management Studio)](../../../ssms/download-sql-server-management-studio-ssms.md).

## <a name="security-considerations-when-using-ssms-to-configure-always-encrypted"></a>Considerações de segurança ao usar o SSMS para configurar o Always Encrypted

Quando você usa o SSMS para configurar o Always Encrypted, o SSMS lida com dados sensíveis e chaves do Always Encrypted, por isso, as chaves e os dados aparecem em texto não criptografado dentro do processo do SSMS. Portanto, é importante que você execute o SSMS em um computador seguro. Se seu banco de dados estiver hospedado no SQL Server, certifique-se de que o SSMS seja executado em um computador diferente do computador que hospeda a instância do SQL Server. Como o objetivo principal do Always Encrypted é garantir que os dados confidenciais criptografados estejam seguros mesmo se o sistema do banco de dados for comprometido, a execução de um script do PowerShell que processa chaves ou dados confidenciais no computador do SQL Server pode reduzir ou anular os benefícios do recurso. Para obter recomendações adicionais, consulte [Security Considerations for Key Management](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)(Considerações de segurança para o Gerenciamento de Chaves).

O SSMS não dá suporte à separação de funções entre aquelas que gerenciam o banco de dados (DBAs) e aquelas que gerenciam os segredos de criptografia e têm acesso aos dados de texto não criptografado (Administradores de Segurança e/ou Administradores de Aplicativos). Se sua organização impõe a separação de funções, você deve usar o PowerShell para configurar o Always Encrypted. Para saber mais, confira [Visão geral do gerenciamento de chaves do Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) e [Configurar o Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md). 

## <a name="always-encrypted-tasks-using-ssms"></a>Tarefas do Always Encrypted usando o SSMS

- [Provisionar chaves Always Encrypted usando o SQL Server Management Studio](configure-always-encrypted-keys-using-ssms.md)
- [Girar chaves do Always Encrypted usando o SQL Server Management Studio](rotate-always-encrypted-keys-using-ssms.md)
- [Configurar a criptografia de coluna usando o Assistente do Always Encrypted](always-encrypted-wizard.md)
- [Configurar a criptografia de coluna usando o Always Encrypted com um pacote de DAC](configure-always-encrypted-using-dacpac.md)
- [Consultar colunas usando o Always Encrypted com o SQL Server Management Studio](always-encrypted-query-columns-ssms.md)
- [Exportar e importar bancos de dados usando o Always Encrypted](always-encrypted-migrate-using-bacpac.md)
- [Fazer backup de bancos de dados e restaurá-los usando o Always Encrypted](always-encrypted-migrate-using-backup-restore.md)
- [Migrar dados para ou de colunas usando Always Encrypted com o Assistente de Importação e Exportação do SQL Server](always-encrypted-migrate-using-import-export-wizard.md)

## <a name="see-also"></a>Consulte Também
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Visão geral do gerenciamento de chaves do Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)
