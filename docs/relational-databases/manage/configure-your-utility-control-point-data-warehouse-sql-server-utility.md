---
title: Configurar seu data warehouse do ponto de controle do utilitário (Utilitário do SQL Server) | Microsoft Docs
description: Saiba mais sobre o data warehouse de gerenciamento do utilitário, em que as instâncias do SQL Server armazenam dados. Saiba como configurar o período de retenção de dados e o diretório.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e35e6e779a138633c8ea15c79a2d1370c1b3edcf
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775993"
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>Configurar o data warehouse a partir do ponto de controle do utilitário (Utilitário do SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Dados coletados por instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são armazenados no UMDW (data warehouse de gerenciamento do utilitário); o nome de arquivo UMDW é sysutility_mdw.  
  
 É possível configurar o período de retenção de dados do UMDW. Para obter mais informações, veja [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Os parâmetros de configuração a seguir não podem ser configurados nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Nome do UMDW: Sysutility_mdw.  
  
-   Frequência de upload do conjunto de coleta: a cada 15 minutos.  
  
 O diretório do UMDW é configurável: \<System drive>:\Program Files\Microsoft SQL Server\MSSQL10_50.<Nome_do_UCP>\MSSQL\Data\\, em que \<System drive>, normalmente, é a unidade C:\. O arquivo de log Sysutility_mdw_\<GUID>_LOG está localizado no mesmo diretório.  
  
> [!NOTE]  
>  O local do arquivo UMDW (sysutility_mdw) pode ser alterado usando-se desanexar/anexar ou ALTER DATABASE. É recomendável usar ALTER DATABASE. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
