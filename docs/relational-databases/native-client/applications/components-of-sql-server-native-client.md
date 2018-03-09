---
title: Componentes do SQL Server Native Client | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3405727d9d62ccb68fa5e4b66f262f1279991338
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="components-of-sql-server-native-client"></a>Componentes do SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client contém os seguintes componentes:  
  
|Componente|Description|  
|---------------|-----------------|  
|sqlncli11.dll|O arquivo de biblioteca de vínculo dinâmico (DLL) que contém toda a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Isso inclui o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlnclir11.rll|O arquivo de recursos que acompanha a biblioteca do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|   
|sqlncli.h|O arquivo do cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que contém todas as novas definições necessárias para usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Esse arquivo de cabeçalho substitui os arquivos de cabeçalho odbcss.h e sqloledb.h.<br /><br /> Observação: Você não pode referenciar SQLNCLI. h e Odbcss no mesmo programa, mas você pode referenciar SQLNCLI. h e SQLOLEDB no mesmo programa, desde que SQLOLEDB é definido pela primeira vez.|  
|sqlncli11.lib|O arquivo de biblioteca necessário para chamar diretamente o **bcp** funções de utilitário que fazem parte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client.<br /><br /> Observação: Se você referenciar o arquivo sqlncli11.lib no código de programação, você precisa certificar-se de que o arquivo sqlncli11.dll está no caminho do sistema e no caminho do sistema dos usuários que usam o seu aplicativo.|  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
