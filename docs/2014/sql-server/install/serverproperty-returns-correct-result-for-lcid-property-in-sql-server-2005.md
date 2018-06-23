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
ms.topic: article
helpviewer_keywords:
- SERVERPROPERTY function
ms.assetid: 833a2fc9-b480-4697-aa7b-9677e78ee0b4
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2b0179ebe39b56082bc51cfe944e6de28e0b4a2c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119038"
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
  
  
