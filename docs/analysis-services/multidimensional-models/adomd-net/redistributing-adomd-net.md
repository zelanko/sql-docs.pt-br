---
title: Redistribuindo ADOMD.NET | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aef9cf75270e8fccf9572669ad0487fce96c0c61
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027293"
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
  
  
