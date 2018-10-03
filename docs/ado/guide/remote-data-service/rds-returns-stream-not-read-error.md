---
title: Retorna RDS &quot;Stream não leitura&quot; erro | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc2944e213e2a6a8ba3f9dc51a9a23b496f4e31a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613914"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>Retorna RDS &quot;Stream não leitura&quot; erro
"O objeto Stream não foi possível ler porque ele está vazio ou a posição atual está no final o Stream. Para fluxos de não vazio, defina a posição atual com a propriedade Position. Para determinar se um Stream está vazio, verifique a propriedade de tamanho."  
  
 Se você vir essa mensagem de erro, você pode ter tentado usar uma consulta parametrizada de hierárquica por meio de http. RDS permite que você usar hierarquias parametrizadas remotas.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


