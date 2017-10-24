---
title: Redistribuindo ADOMD.NET | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3851f8dd3eea3fb2a98554bba365e723765a641d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

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
 [Programação do servidor do ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  

