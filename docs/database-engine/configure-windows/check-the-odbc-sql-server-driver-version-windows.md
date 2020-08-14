---
title: Verificar a versão do driver ODBC do SQL Server (Windows) | Microsoft Docs
description: Descubra como usar o Administrador de Fonte de Dados ODBC do Windows para verificar a versão dos drivers ODBC instalados no seu computador.
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d127e7400238210d96b95adcba505cb2a1572cdd
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790379"
---
# <a name="check-the-odbc-sql-server-driver-version-windows"></a>Verificar a versão do driver ODBC do SQL Server (Windows)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Seu computador pode conter uma variedade de drivers ODBC, da [!INCLUDE[msCoName](../../includes/msconame-md.md)] e de outras empresas. Este tópico descreve como usar o **Administrador de Fonte de Dados ODBC** do Windows para verificar a versão dos drivers ODBC instalados.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-check-the-odbc-sql-server-driver-version-32-bit-odbc"></a>Verificar a versão de driver ODBC SQL Server (ODBC de 32 bits)  
  
-   No **Administrador de Fonte de Dados ODBC**, clique na guia **Drivers** .  
  
     As informações de entrada do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são exibidas na coluna **Versão** .  


> [!NOTE]  
>  Para conexões com a Autenticação do Azure Active Directory para o Banco de Dados SQL, instale o driver mais recente, por exemplo, [ODBC Driver 17 for SQL Server](https://aka.ms/downloadmsodbcsql).   

  
## <a name="see-also"></a>Consulte Também  
 [Abrir o Administrador de Fonte de Dados ODBC](../../database-engine/configure-windows/open-the-odbc-data-source-administrator.md)  
  
  
