---
title: Soluções para acesso a dados remotos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 13c7179576cd29fb646b3fc62b21694452a0749b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699329"
---
# <a name="solutions-for-remote-data-access"></a>Soluções para Acesso a dados remotos
## <a name="the-issue"></a>O problema  
 ADO permite que seu aplicativo diretamente, acessar e modificar fontes de dados (às vezes chamadas de um sistema de duas camadas). Por exemplo, se sua conexão é a fonte de dados que contém seus dados, que é uma conexão direta em um sistema de duas camadas.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 No entanto, você talvez queira acessar fontes de dados indiretamente por meio de um intermediário, como o Microsoft® Internet Information Services (IIS). Essa disposição às vezes é chamada de sistema de três camadas. O IIS é um sistema cliente/servidor que fornece uma maneira eficiente para um aplicativo local ou cliente invocar um programa remoto ou servidor, entre a Internet ou intranet. O programa de servidor obtém acesso à fonte de dados e, opcionalmente, processa os dados adquiridos.  
  
 Por exemplo, sua página da Web de intranet contém um aplicativo escrito em Microsoft® Visual Basic Scripting Edition (VBScript), que se conecta ao IIS. IIS conecta-se à fonte de dados real por sua vez, recupera os dados, processa-o de alguma forma e, em seguida, retorna a informação processada para seu aplicativo.  
  
 Neste exemplo, seu aplicativo nunca conectado diretamente à fonte de dados; IIS fez. E IIS acessados os dados por meio de ADO.  
  
> [!NOTE]
>  O aplicativo cliente/servidor não precisa ser baseado na Internet ou intranet (ou seja, baseado na Web)-ele pode ser formado apenas por programas compilados em uma rede local. No entanto, o caso comum é um aplicativo baseado na Web.  
  
 Porque algum controle visual, como uma grade, caixa de seleção ou lista, pode usar as informações retornadas, as informações retornadas devem ser facilmente usadas por um controle visual.  
  
 Você deseja que uma interface de programação de aplicativo simple e eficiente que dá suporte a sistemas de três camadas e retorna informações como facilmente como se ele tivesse sido recuperado em um sistema de duas camadas. Serviço de dados remota (RDS) é esta interface.  
  
## <a name="the-solution"></a>A solução  
 RDS define um modelo de programação - a sequência de atividades necessárias para acessar e atualizar uma fonte de dados - para ter acesso a dados por meio de um intermediário, como o Internet Information Services (IIS). O modelo de programação resume toda a funcionalidade do RDS.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de programação básica do RDS](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [Cenário RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


