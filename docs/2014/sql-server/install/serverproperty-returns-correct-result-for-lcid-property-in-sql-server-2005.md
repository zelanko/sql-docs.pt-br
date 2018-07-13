---
title: SERVERPROPERTY retorna resultado correto para a propriedade LCID no SQL Server 2005 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SERVERPROPERTY function
ms.assetid: 833a2fc9-b480-4697-aa7b-9677e78ee0b4
caps.latest.revision: 17
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9a92dd33ee5693d78b5f55f3bfcbc6edb4a0d8b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157697"
---
# <a name="serverproperty-returns-correct-result-for-lcid-property-in-sql-server-2005"></a>SERVERPROPERTY retorna resultado correto para a propriedade LCID no SQL Server 2005
  Quando SERVERPROPERTY('LCID') é executado em servidores de agrupamento primário, a função retorna o LCID (identificador de localidade) do Windows que corresponde ao agrupamento do servidor.  
  
> [!NOTE]  
>  No caso de arquivos em lote ou de rastreamento que contêm referências a SERVERPROPERTY ('LCID') e que são executados em outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o Supervisor de Atualização detectará essa alteração de comportamento somente se outras instâncias tiverem o mesmo agrupamento que a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique os aplicativos para que estejam preparados para que SERVERPROPERTY ('LCID') retorne o LCDI do Windows que corresponde ao agrupamento do servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
