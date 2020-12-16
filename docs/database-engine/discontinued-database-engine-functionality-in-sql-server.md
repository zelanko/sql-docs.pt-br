---
title: Funcionalidades descontinuadas do mecanismo de banco de dados
description: Saiba quais recursos e funcionalidades do mecanismo de banco de dados foram descontinuados no SQL Server 2019 (15.x), SQL Server 2016 (13.x) e versões anteriores.
ms.custom: seo-lt-2019
ms.date: 07/22/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- SSL
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= sql-server-linux-2017  || >= sql-server-2016'
ms.openlocfilehash: 73ebe8f968cb3cf91c909ca404c5475f983e2ca6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438810"
---
# <a name="discontinued-database-engine-functionality-in-sql-server"></a>Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  Este tópico descreve os recursos do [!INCLUDE[ssDE](../includes/ssde-md.md)] que não estão mais disponíveis no [!INCLUDE[ssCurrent](../includes/ssnoversion-md.md)].  

## <a name="discontinued-features-in-sssqlv15"></a>Recursos descontinuados no [!INCLUDE[ssSQLv15](../includes/sssqlv15-md.md)]  

- As opções de configuração a seguir no escopo do banco de dados foram descontinuadas:

  - `DISABLE_BATCH_MODE_ADAPTIVE_JOIN`
  - `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK`
  - `DISABLE_INTERLEAVED_EXECUTION_TVF`

Para obter as opções de configuração atuais, confira [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

>[!NOTE]
>Nenhum recurso foi descontinuado no [!INCLUDE[ssSQLv14](../includes/sssqlv14-md.md)].

## <a name="discontinued-features-in-sssql15"></a>Recursos descontinuados no [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]

- [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] é um aplicativo de 64 bits. A instalação de 32 bits foi descontinuada, embora alguns elementos sejam executados como componentes de 32 bits.  

- O nível de compatibilidade 90 foi descontinuado. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  

- O subsistema do ActiveX foi descontinuado. Use a linha de comando ou scripts do PowerShell.

- Parâmetros de inicialização **-h** e **-g**. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](/previous-versions/sql/2014/database-engine/configure-windows/database-engine-service-startup-options?view=sql-server-2014).

- A criptografia do protocolo SSL foi descontinuada. Use o protocolo TLS em vez disso. Para obter mais informações, confira [Habilitar conexões para o Mecanismo de Banco de Dados](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).

## <a name="previous-versions"></a>Versões anteriores

- [Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2014](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014)

### <a name="see-also"></a>Confira também

- [Recursos preteridos do mecanismo de banco de dados no SQL Server 2019](deprecated-database-engine-features-in-sql-server-version-15.md)
- [Recursos preteridos do mecanismo de banco de dados no SQL Server 2017](deprecated-database-engine-features-in-sql-server-2017.md)
- [Recursos preteridos do mecanismo de banco de dados no SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)
- [Alterações da falha em recursos do mecanismo de banco de dados no SQL Server 2019](breaking-changes-to-database-engine-features-in-sql-server-version-15.md)
- [Alterações da falha em recursos do mecanismo de banco de dados no SQL Server 2017](breaking-changes-to-database-engine-features-in-sql-server-2017.md)
- [Alterações da falha em recursos do mecanismo de banco de dados no SQL Server 2016](breaking-changes-to-database-engine-features-in-sql-server-2016.md)
- [Recursos preteridos na Replicação do SQL Server](../relational-databases/replication/deprecated-features-in-sql-server-replication.md)