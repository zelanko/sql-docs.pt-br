---
title: "Soluções para acesso a dados remotos | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2377f7a33f8426d7081806980618c432a56bba42
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="solutions-for-remote-data-access"></a>Soluções para acesso a dados remotos
## <a name="the-issue"></a>O problema  
 ADO permite que seu aplicativo diretamente acessar e modificar fontes de dados (às vezes chamadas de um sistema de duas camadas). Por exemplo, se sua conexão à fonte de dados que contém os dados, que é uma conexão direta em um sistema de duas camadas.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 No entanto, você talvez queira acessar fontes de dados indiretamente por meio de um intermediário, como o Microsoft® Internet Information Services (IIS). Essa organização às vezes é chamada de sistema de três camadas. O IIS é um sistema cliente/servidor que fornece uma maneira eficiente para um aplicativo local ou cliente chamar um programa remoto ou servidor, na Internet ou intranet. O programa de servidor obtém acesso à fonte de dados e, opcionalmente, processa os dados obtidos.  
  
 Por exemplo, a página da Web da intranet contém um aplicativo escrito em Microsoft® Visual Basic Scripting Edition (VBScript), que se conecta ao IIS. IIS conecta-se à fonte de dados real por sua vez, recupera os dados, processa de alguma forma e, em seguida, retorna as informações solicitadas para seu aplicativo.  
  
 Neste exemplo, seu aplicativo nunca conectado diretamente à fonte de dados; O IIS foi. E IIS acessados os dados por meio de ADO.  
  
> [!NOTE]
>  O aplicativo cliente/servidor não precisa ser com base na Internet ou intranet (ou seja, baseado na Web) — ele pode ser formado apenas por programas compilados em uma rede local. No entanto, o caso típico é um aplicativo baseado na Web.  
  
 Porque algum controle visual, como uma grade, caixa de seleção ou lista, pode usar as informações retornadas, as informações retornadas devem ser facilmente usadas por um controle de visual.  
  
 Você deseja uma interface de programação de aplicativo simple e eficiente que dá suporte a sistemas de três camadas e retorna informações como facilmente como se ele tivesse sido recuperado em um sistema de duas camadas. Remote Data Service (RDS) é esta interface.  
  
## <a name="the-solution"></a>A solução  
 RDS define um modelo de programação, a sequência de atividades necessárias para acessar e atualizar uma fonte de dados — para obter acesso aos dados por meio de um intermediário, como o Internet Information Services (IIS). O modelo de programação resume a funcionalidade total do RDS.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de programação de RDS básica](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [Cenário RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


