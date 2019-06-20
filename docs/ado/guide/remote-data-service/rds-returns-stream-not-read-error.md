---
title: Retorna RDS &quot;Stream não leitura&quot; erro | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 598326335c32f18b5d7f5a764d387e5b5ea536f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699430"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>Retorna RDS &quot;Stream não leitura&quot; erro
"O objeto Stream não foi possível ler porque ele está vazio ou a posição atual está no final o Stream. Para fluxos de não vazio, defina a posição atual com a propriedade Position. Para determinar se um Stream está vazio, verifique a propriedade de tamanho."  
  
 Se você vir essa mensagem de erro, você pode ter tentado usar uma consulta parametrizada de hierárquica por meio de http. RDS permite que você usar hierarquias parametrizadas remotas.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


