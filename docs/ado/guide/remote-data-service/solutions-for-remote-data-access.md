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
ms.openlocfilehash: 40485562c8385e05ced033062563d5c5165218de
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922173"
---
# <a name="solutions-for-remote-data-access"></a>Soluções para Acesso a dados remotos
## <a name="the-issue"></a>O problema  
 O ADO permite que seu aplicativo tenha acesso direto e modifique fontes de dados (às vezes chamado de sistema de duas camadas). Por exemplo, se sua conexão for com a fonte de dados que contém seus dados, essa será uma conexão direta em um sistema de duas camadas.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 No entanto, talvez você queira acessar fontes de dados indiretamente por meio de um intermediário, como o Microsoft® Serviços de Informações da Internet (IIS). Essa organização, às vezes, é chamada de sistema de três camadas. O IIS é um sistema cliente/servidor que fornece uma maneira eficiente para um aplicativo local, ou cliente, para invocar um programa remoto ou de servidor na Internet ou em uma intranet. O programa de servidor obtém acesso à fonte de dados e, opcionalmente, processa os dados adquiridos.  
  
 Por exemplo, sua página da Web intranet contém um aplicativo escrito em Microsoft® Visual Basic Scripting Edition (VBScript), que se conecta ao IIS. O IIS, por sua vez, conecta-se à fonte de dados real, recupera os dados, processa-os de alguma forma e, em seguida, retorna as informações processadas para seu aplicativo.  
  
 Neste exemplo, seu aplicativo nunca se conectou diretamente à fonte de dados; O IIS fez. E o IIS acessou os dados por meio do ADO.  
  
> [!NOTE]
>  O aplicativo cliente/servidor não precisa ser baseado na Internet ou em uma intranet (ou seja, baseado na Web). ele pode consistir apenas em programas compilados em uma rede local. No entanto, o caso típico é um aplicativo baseado na Web.  
  
 Como um controle visual, como uma grade, uma caixa de seleção ou uma lista, pode usar as informações retornadas, as informações retornadas devem ser facilmente usadas por um controle visual.  
  
 Você quer uma interface de programação de aplicativo simples e eficiente que dê suporte a sistemas de três camadas e retorna informações tão facilmente quanto se elas tivessem sido recuperadas em um sistema de duas camadas. O RDS (serviço de dados remotos) é essa interface.  
  
## <a name="the-solution"></a>A solução  
 O RDS define um modelo de programação – a sequência de atividades necessárias para obter acesso e atualizar uma fonte de dados-para obter acesso aos dados por meio de um intermediário, como Serviços de Informações da Internet (IIS). O modelo de programação resume toda a funcionalidade do RDS.  
  
## <a name="see-also"></a>Consulte Também  
 [Modelo de programação RDS básico](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [Cenário de RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial do RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


