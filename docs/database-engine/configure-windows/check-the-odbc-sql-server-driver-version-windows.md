---
title: Verificar a versão do driver ODBC do SQL Server (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 11/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- driver version number [ODBC]
- ODBC drivers, version number
ms.assetid: 43451080-a562-4231-b1d4-1ba35ca0ea79
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fb6646d96991785b7c94a48ad4601fdcc6e35b60
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799545"
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
  
  
