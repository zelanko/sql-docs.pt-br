---
title: "Compatibilidade com versões anteriores no SMO | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2f986436-aaf2-4eaf-9809-df849d97d4fb
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d82e62d1c4ed82a4339398f60a7e8a59ac9c2d59
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="backward-compatibility-in-smo"></a>Compatibilidade com versões anteriores no SMO
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Aplicativos SMO que foram escritos em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser recompilados com o SMO no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="migrating-smo-applications"></a>Migrando aplicativos SMO  
 As referências a dlls do SMO em versões mais antigas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser removidas, e as referências às novas dlls do SMO fornecidas com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] devem ser incluídas.  
  
 No mínimo, você faria as seguintes referências:  
  
-   Microsoft.SqlServer.ConnectionInfo  
  
-   Microsoft.SqlServer.Smo  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc  
  
 Esses arquivos são necessários para classes de conexão, classes de utilitário do SMO e classes de base.  
  
> [!NOTE]  
>  O arquivo SmoEnum.dll foi removido; portanto, as referências a ele devem ser removidas do projeto [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SMO.  
  
 Os namespaces também mudaram e você poderá usar o seguinte:  
  
##### <a name="for-visual-c"></a>Para o Visual C#  
  
```  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
```  
  
##### <a name="for-visual-basic"></a>Para o Visual Basic  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
```  
  
 Se o seu código usa a funcionalidade Urn, como **Server.GetSqlSmoObject(Urn)**, você deve estabelecer um vínculo com o namespace Microsoft.SqlServer.Management.Sdk.Sfc.  
  
 Se o seu código usar o objeto Transfer diretamente, você deverá estabelecer um vínculo com o namespace Microsoft.SqlServer.Management.SmoExtended.  
  
 Ao migrar o código, talvez seja necessário modificá-lo. Isso ocorre porque vários recursos do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] foram preteridos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações sobre recursos substituídos, consulte [recursos de mecanismo de banco de dados preteridos no SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md) na [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Manuais Online.  
  
  
