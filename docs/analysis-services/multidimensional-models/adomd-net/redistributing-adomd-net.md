---
title: Redistribuindo ADOMD.NET | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8d14c89b7263833c25d8a0335a005dfdc8d90151
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="redistributing-adomdnet"></a>Redistribuindo ADOMD.NET
  Quando gravar aplicativos que usam o ADOMD.NET, você deverá redistribuir a versão apropriada do ADOMD.NET junto com seu aplicativo. Para redistribuir o ADOMD.NET, inclua o programa de instalação ADOMD.NET no programa de instalação do seu aplicativo.  
  
 O programa de instalação do ADOMD.NET, bem como a versão mais recente do ADOMD.NET, podem ser encontrados no Centro de Download da Microsoft como parte do SQL Server Feature Pack.  
  
 O programa de instalação do ADOMD.NET instala os arquivos do ADOMD.NET em \< *unidade do sistema*>: \Program Files\Microsoft.NET\ADOMD.NET\\*o número de versão*.  
  
 Depois de incluir o programa de instalação do ADOMD.NET, faça com que o programa de instalação do seu aplicativo execute o programa de instalação de ADOMD.NET para instalá-lo. Além disso, dependendo de seu ambiente, talvez seja necessário garantir que os assemblies relacionados sejam confiáveis pelo SQL Server.  
  
 Para obter mais informações, consulte:  
  
 [Feature Pack para Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Microsoft Connect: Dependências do ADOMD.NET](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>Consulte também  
 [Programação de cliente ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [Programação do servidor no ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
