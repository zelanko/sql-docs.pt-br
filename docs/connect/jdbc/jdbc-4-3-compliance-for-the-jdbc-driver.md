---
title: JDBC 4.3 conformidade para o Driver JDBC | Microsoft Docs
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3f678f33ec8f2c844bce14daa150f6c135744ff
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2018
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 4.3 conformidade para o Driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  Versões anteriores ao Microsoft JDBC Driver 6.4 para SQL Server são compatíveis com as especificações de API do Java Database Connectivity 4.2. Esta seção não se aplica a versões anteriores a versão 6.4.  
  
 Atualmente, o Microsoft JDBC Driver 6.4 para o SQL Server é Java 9 compatível, mas não é totalmente compatível com as especificações de Java 4.3 de API de conectividade de banco de dados. Para recentemente introduzido APIs no JDBC 4.3, se não for suportado pelo driver, o driver lançará um SQLFeatureNotSupportedException.