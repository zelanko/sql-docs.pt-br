---
title: SERVERPROPERTY retorna resultado correto para a propriedade LCID no SQL Server 2005 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SERVERPROPERTY function
ms.assetid: 833a2fc9-b480-4697-aa7b-9677e78ee0b4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3b85b15ec20579cb748cf3e09c0cded8b9e43fd9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659814"
---
# <a name="serverproperty-returns-correct-result-for-lcid-property-in-sql-server-2005"></a>SERVERPROPERTY retorna resultado correto para a propriedade LCID no SQL Server 2005
  Quando SERVERPROPERTY('LCID') é executado em servidores de ordenação primária, a função retorna o LCID (identificador de localidade) do Windows que corresponde à ordenação do servidor.  
  
> [!NOTE]  
>  No caso de arquivos em lote ou de rastreamento que contêm referências a SERVERPROPERTY ('LCID') e que são executados em outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o Supervisor de Atualização detectará essa alteração de comportamento somente se outras instâncias tiverem a mesma ordenação que a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique os aplicativos para que estejam preparados para que SERVERPROPERTY ('LCID') retorne o LCDI do Windows que corresponde à ordenação do servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
