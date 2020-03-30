---
title: Fazer backup de bancos de dados e restaurá-los usando o Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9176052b413293d25acd7696701e4f118adba03f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73595721"
---
# <a name="backup-and-restore-databases-using-always-encrypted"></a>Fazer backup de bancos de dados e restaurá-los usando o Always Encrypted 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Este artigo descreve como fazer backup de um banco de dados que contém colunas protegidas com o [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md), bem como restaurá-lo.

Quando você faz backup de um banco de dados, o arquivo de backup resultante contém criptografado armazenado em colunas criptografadas e todos os metadados das chaves do Always Encrypted.

Quando você restaura um banco de dados, todos os dados criptografados e todos os metadados das chaves do Always Encrypted são restaurados. 

Se você restaurou o banco de dados em um servidor diferente ou com outro nome, não precisa fazer nada especial para permitir que o aplicativo consulte os dados criptografados no banco de dados de destino, pois as chaves nos dois bancos de dados são iguais.

Para obter informações detalhadas sobre como fazer backup de um banco de dados e restaurá-lo, confira:
- [Visão geral de backup (SQL Server)](../../backup-restore/backup-overview-sql-server.md)
- [Restaurar um banco de dados em uma Instância Gerenciada](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started-restore)

## <a name="next-steps"></a>Próximas etapas
- [Consultar colunas usando o Always Encrypted com o SQL Server Management Studio](always-encrypted-query-columns-ssms.md)
- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md) 

## <a name="see-also"></a>Consulte Também
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Exportar e importar bancos de dados usando o Always Encrypted](always-encrypted-migrate-using-bacpac.md)
- [Migrar dados para ou de colunas usando Always Encrypted com o Assistente de Importação e Exportação do SQL Server](always-encrypted-migrate-using-import-export-wizard.md)
- [Carregar em massa dados criptografados em colunas usando o Always Encrypted](migrate-sensitive-data-protected-by-always-encrypted.md)
