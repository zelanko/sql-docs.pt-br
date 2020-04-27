---
title: A nova coluna na saída de sp_helptrigger pode afetar os aplicativos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sp_helptrigger
ms.assetid: b7c42a8f-f2e0-4fa3-b046-3cf39c854c47
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 33d47c858a03766260e8ed8c098fef79e9e4a82f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093735"
---
# <a name="new-column-in-output-of-sp_helptrigger-may-impact-applications"></a>Coluna nova no resultado do sp_helptrigger pode impactar nos aplicativos
  trigger_schemaias a última coluna no conjunto de resultados retornado pelo procedimento armazenado do sistema sp_helptrigger.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Para obter informações sobre gatilhos definidos em uma tabela particular, consulte a exibição do catálogo sys.triggers.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Revise o uso de aplicativos sp_helptrigger. Talvez seja necessário modificar seus aplicativos para acomodar a coluna adicional. Como alternativa, você pode usar a exibição do catálogo sys.triggers.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
