---
title: Redistribuindo ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c6253336e3f7432c7110a728a1b0aa636afc2e3f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224746"
---
# <a name="redistributing-adomdnet"></a>Redistribuindo ADOMD.NET
  Quando gravar aplicativos que usam o ADOMD.NET, você deverá redistribuir a versão apropriada do ADOMD.NET junto com seu aplicativo. Para redistribuir o ADOMD.NET, inclua o programa de instalação ADOMD.NET no programa de instalação do seu aplicativo.  
  
 O programa de instalação do ADOMD.NET, bem como a versão mais recente do ADOMD.NET, podem ser encontrados no Centro de Download da Microsoft como parte do SQL Server Feature Pack.  
  
 O programa de instalação do ADOMD.NET instala os arquivos do ADOMD.NET na \< *unidade do sistema*>: \Program Files\Microsoft.NET\ADOMD.NET\\*número de versão*.  
  
 Depois de incluir o programa de instalação do ADOMD.NET, faça com que o programa de instalação do seu aplicativo execute o programa de instalação de ADOMD.NET para instalá-lo. Além disso, dependendo de seu ambiente, talvez seja necessário garantir que os assemblies relacionados sejam confiáveis pelo SQL Server.  
  
 Para obter mais informações, consulte:  
  
 [Feature Pack para Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Do Microsoft Connect: Dependências do ADOMD.NET](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>Consulte também  
 [Programação de cliente ADOMD.NET](../../multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [Programação do servidor no ADOMD.NET](../../multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
