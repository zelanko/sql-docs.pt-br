---
description: Exportar e importar bancos de dados usando o Always Encrypted
title: Exportar e importar bancos de dados usando o Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
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
ms.openlocfilehash: 3fc54fedce772b267cf19a9396672b61cf6e6254
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127731"
---
# <a name="export-and-import-databases-using-always-encrypted"></a>Exportar e importar bancos de dados usando o Always Encrypted 
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

Este artigo descreve como exportar e importar bancos de dados que contêm colunas protegidas com o [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md).

Quando você exporta um banco de dados, todos os dados armazenados em colunas criptografadas são recuperados do banco de dados no formato criptografado (texto cifrado) e colocados no [BACPAC](../../data-tier-applications/data-tier-applications.md) resultante. O BACPAC resultante também contém os metadados de chaves Always Encrypted.

Quando você importa o BACPAC em um banco de dados, os dados criptografados dele são carregados no banco de dados e os metadados de chave Always Encrypted são recriados. 

Se você tem um aplicativo que está configurado para consultar as colunas criptografadas armazenadas no banco de dados de origem (aquele exportado), não precisa fazer nada especial para permitir que o aplicativo consulte os dados criptografados no banco de dados de destino, pois as chaves nos dois bancos de dados são iguais.

Para obter informações detalhadas sobre como exportar e importar um banco de dados, confira:
- [Exportar um aplicativo da camada de dados](../../data-tier-applications/export-a-data-tier-application.md)
- [Importar um arquivo BACPAC para criar um novo banco de dados de usuário](../../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)
- [Exportar um Banco de Dados SQL do Azure para um arquivo BACPAC](/azure/sql-database/sql-database-export)
- [Importar um arquivo BACPAC para um banco de dados no Banco de Dados SQL do Azure](/azure/sql-database/sql-database-import)
- [SqlPackage.exe](../../../tools/sqlpackage.md)

## <a name="permissions-for-migrating-databases-with-encrypted-columns"></a>Permissões para migrar bancos de dados com colunas criptografadas

Você precisa de *ALTER ANY COLUMN MASTER KEY* e *ALTER ANY COLUMN ENCRYPTION KEY* no banco de dados de origem. Você precisará de *ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION DEFINITION* no banco de dados de destino.

Você não precisa ter acesso às chaves mestras de coluna configuradas para as colunas criptografadas, pois os dados permanecem criptografados durante as operações de exportação e importação.

## <a name="next-steps"></a>Próximas etapas
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)

## <a name="see-also"></a>Consulte Também
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Fazer backup de bancos de dados e restaurá-los usando o Always Encrypted ](always-encrypted-migrate-using-backup-restore.md)
- [Migrar dados para ou de colunas usando Always Encrypted com o Assistente de Importação e Exportação do SQL Server](always-encrypted-migrate-using-import-export-wizard.md)
- [Carregar em massa dados criptografados em colunas usando o Always Encrypted](migrate-sensitive-data-protected-by-always-encrypted.md)