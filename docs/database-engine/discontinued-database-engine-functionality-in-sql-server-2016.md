---
title: Funcionalidade descontinuada do Mecanismo de Banco de Dados no SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
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
ms.openlocfilehash: c93aa484caf1ae6a2b7582c00f8fd6223fcf35e5
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874188"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2016"></a>Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve os recursos do [!INCLUDE[ssDE](../includes/ssde-md.md)] que não estão mais disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-includesssql15includessssql15-mdmd"></a>Recursos descontinuados no [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
- [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] é um aplicativo de 64 bits. A instalação de 32 bits foi descontinuada, embora alguns elementos sejam executados como componentes de 32 bits.  
  
- O nível de compatibilidade 90 foi descontinuado. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  

- O subsistema do ActiveX foi descontinuado. Use a linha de comando ou scripts do PowerShell.

- Parâmetros de inicialização **-h** e **-g**. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](https://docs.microsoft.com/sql/database-engine/configure-windows/database-engine-service-startup-options?view=sql-server-2014).

- A criptografia do protocolo SSL foi descontinuada. Use o protocolo TLS em vez disso. Para obter mais informações, confira [Habilitar conexões para o Mecanismo de Banco de Dados](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).
  
## <a name="previous-versions"></a>Versões anteriores  
  
- [Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2014](https://docs.microsoft.com/sql/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014)

## <a name="see-also"></a>Consulte Também  
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Recursos preteridos na Replicação do SQL Server](../relational-databases/replication/deprecated-features-in-sql-server-replication.md)  
  
 
