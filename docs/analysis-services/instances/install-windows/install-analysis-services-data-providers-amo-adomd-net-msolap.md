---
title: Instalar provedores de dados do Analysis Services (AMO, ADOMD.NET, MSOLAP) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7aedabc-6af9-4698-a7a4-98f894001476
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd6aa812228cce132b4180a8537ba853f3ea92a2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="install-analysis-services-data-providers-amo-adomdnet-msolap"></a>Instalar provedores de dados do Analysis Services (AMO, ADOMD.NET, MSOLAP)
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] é uma atualização de versão dos provedores de dados do Analysis Services, consistindo em ADOMD.Net, AMO e MSOLAP.  
  
 Para a maioria dos cenários de acesso a dados baseado em consulta, você pode usar as versões mais antigas existentes dos provedores de dados já instalados nos sistemas cliente para acessar modelos multidimensionais e tabulares em uma instância do SQL Server 2016 Analysis Services, incluindo modelos de tabela que usam recursos exclusivos do SQL Server 2016. Como regra geral, os aplicativos cliente que geram consultas, como Excel, Reporting Services ou Tableau, não devem exigir os provedores de dados mais recentes ao acessar um modelo do Analysis Services.  
  
 Ferramentas de modelagem e administração são uma exceção à regra, pelo menos em termos de requisitos de versão para provedores de dados. Essas ferramentas devem ter os provedores de dados que foram criados especificamente para o servidor de destino, para manipular objetos no servidor. Felizmente, as ferramentas fornecidas com [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] incluem automaticamente os provedores de dados que estão em conformidade com a versão atual do servidor.  A instalação do SQL Server Data Tools para Visual Studio 2015 instala provedores de dados para o SQL Server 2016 Analysis Services. Da mesma forma, o SQL Server 2016 Management Studio, que usa o AMO e ADOMD.Net, instala os provedores de dados para [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 Um cenário que exige uma instalação manual de um provedor de dados são aplicativos personalizados ou scripts que usam o AMO (Analysis Services Management Objects). Esta versão apresenta um namespace refatorado que move os objetos principais, como o servidor e banco de dados para um novo namespace (Microsoft.AnalysisServices.Core) que faz parte do assembly Microsoft.AnalysisServices.dll. Se você tiver código personalizado ou os scripts que usam o AMO, precisará recompilar o código e atualizar manualmente o AMO em cada servidor e estação de trabalho cliente que faz uma conexão direta por meio de AMO a uma instância do SQL Server 2016 do Analysis Services.  
  
## <a name="provider-list"></a>Lista de provedores  
 A tabela a seguir descreve cada provedor.  
  
||||  
|-|-|-|  
|Provedor|Filename|Versão|  
|Objetos de Gerenciamento do Analysis Services (AMO)|Microsoft.AnalysisServices.dll|13.0.0.0|  
|Analysis Services Core|Microsoft.AnalysisServices.Core.dll|13.0.0.0|  
|Analysis Services (ADOMD.NET)|Microsoft.AnalysisServices.AdomdClient.dll|13.0.0.0|  
|Provedor OLE DB do para Analysis Services (MSOLAP)|MSOLAP130.dll|13.0.0.0|  
  
## <a name="download-and-install-data-provider"></a>Baixar e instalar o provedor de dados  
  
1.  Vá para a [página de download do Feature Pack para SQL Server 2016](http://go.microsoft.com/fwlink/?LinkID=398150).  
  
2.  Clique em **Baixar** para habilitar a instalação de componentes individuais.  
  
3.  Para computadores de 64 bits, selecione todos ou alguns dos seguintes (caso contrário, escolha o equivalente de x86):  
  
    -   ENU\x64\SQL_AS_ADOMD.msi  
  
    -   ENU\x64\SQL_AS_AMO.msi  
  
    -   ENU\x64\SQL_AS_OLEDB.msi  
  
4.  Clique em **Avançar** para baixar os arquivos.  
  
5.  Execute cada programa para instalar o provedor. Os assemblies ADO.MD e AMO são instalados no C:\Windows\assembly\GAC_MSIL. O provedor OLE DB do Analysis Services é instalado no C:\Program Files\Microsoft Analysis Services\AS OLEDB\130.  
  
## <a name="verify-installation"></a>Verifique a instalação  
  
1.  No Explorador de arquivos, vá para C:\Windows\Assembly.  
  
2.  Clique com o botão direito do mouse em Microsoft.AnalysisServices e selecione **Propriedades**.  
  
3.  Clique em **Versão** para confirmar que você tem o build mais recente.  
  
  

