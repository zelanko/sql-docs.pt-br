---
title: "Configurar seu data warehouse do ponto de controle do utilitário (Utilitário do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 05a436bf21810e3c05c2f745d6f0c067f61d0d35
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>Configurar o data warehouse a partir do ponto de controle do utilitário (Utilitário do SQL Server)
  Dados coletados por instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são armazenados no UMDW (data warehouse de gerenciamento do utilitário); o nome de arquivo UMDW é sysutility_mdw.  
  
 É possível configurar o período de retenção de dados do UMDW. Para obter mais informações, veja [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Os parâmetros de configuração a seguir não podem ser configurados nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Nome do UMDW: Sysutility_mdw.  
  
-   Frequência de carregamento do conjunto de coleta: a cada 15 minutos.  
  
 O diretório do UMDW é configurável: \<System drive>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\, where \<System drive> normalmente é a unidade C:\. O arquivo de log Sysutility_mdw_\<GUID>_LOG, está localizado no mesmo diretório.  
  
> [!NOTE]  
>  O local do arquivo UMDW (sysutility_mdw) pode ser alterado usando-se desanexar/anexar ou ALTER DATABASE. É recomendável usar ALTER DATABASE. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
