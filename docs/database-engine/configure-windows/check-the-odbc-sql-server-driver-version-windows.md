---
title: Verificar a versão do driver ODBC do SQL Server (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 11/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- driver version number [ODBC]
- ODBC drivers, version number
ms.assetid: 43451080-a562-4231-b1d4-1ba35ca0ea79
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1012d97082fe975a4e5eea7e0003df703ad32bc0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="check-the-odbc-sql-server-driver-version-windows"></a>Verificar a versão do driver ODBC do SQL Server (Windows)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Seu computador pode conter uma variedade de drivers ODBC, da [!INCLUDE[msCoName](../../includes/msconame-md.md)] e de outras empresas. Este tópico descreve como usar o **Administrador de Fonte de Dados ODBC** do Windows para verificar a versão dos drivers ODBC instalados.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-check-the-odbc-sql-server-driver-version-32-bit-odbc"></a>Verificar a versão de driver ODBC SQL Server (ODBC de 32 bits)  
  
-   No **Administrador de Fonte de Dados ODBC**, clique na guia **Drivers** .  
  
     As informações de entrada do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são exibidas na coluna **Versão** .  


> [!NOTE]  
>  Para conexões do Banco de Dados SQL com a Autenticação do Azure Active Directory instale o driver mais recente, por exemplo [Driver ODBC 13.1 para SQL Server](https://www.microsoft.com/download/details.aspx?id=53339).   

  
## <a name="see-also"></a>Consulte Também  
 [Abrir o Administrador de Fonte de Dados ODBC](../../database-engine/configure-windows/open-the-odbc-data-source-administrator.md)  
  
  
