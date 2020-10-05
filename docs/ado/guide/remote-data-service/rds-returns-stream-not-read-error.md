---
description: O RDS retorna o &quot; erro de fluxo não lido &quot;
title: O RDS retorna o &quot; erro de fluxo não lido &quot; | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: rothja
ms.author: jroth
ms.openlocfilehash: 6acb603594acdd23f8ad8764c9b9a692acabdb9b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724897"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>O RDS retorna o &quot; erro de fluxo não lido &quot;
"Não foi possível ler o objeto de fluxo porque ele está vazio ou a posição atual está no final do fluxo. Para fluxos não vazios, defina a posição atual com a propriedade Position. Para determinar se um fluxo está vazio, verifique a propriedade Size. "  
  
 Se você vir essa mensagem de erro, você pode ter tentado usar uma consulta hierárquica parametrizada sobre http. O RDS não permite que você use hierarquias com parâmetros remotos.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](./rds-fundamentals.md)