---
title: Arquitetura de objeto de servidor do ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, object model
- object model [ADOMD.NET]
ms.assetid: bdc81de9-b390-4654-b62a-cd6c0c9ca10d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05aee754db65811d450fb06e0e433cb4b207c372
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145621"
---
# <a name="adomdnet-server-object-architecture"></a>Arquitetura de objeto de servidor do ADOMD.NET
  Os objetos do servidor ADOMD.NET são auxiliares que pode ser usado para criar funções definidas pelo usuário (UDFs) ou procedimentos armazenados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Para usar o namespace `Microsoft.AnalysisServices.AdomdServer` (e esses objetos), adicione uma referência a msmgdsrv.dll ao projeto UDF ou ao procedimento armazenado.  
  
 ![Mostra as relações de objeto no servidor do ADOMD.NET](../../../2014/analysis-services/dev-guide/media/adomdnetserverobjectmodel.gif "mostra as relações de objeto no servidor do ADOMD.NET")  
Modelo de objeto do ADOMD.NET  
  
 A interação com a hierarquia de objetos do ADOMD.NET normalmente começa com um ou mais objetos da camada superior, como descrito na tabela a seguir.  
  
|Para|Use este objeto|  
|--------|---------------------|  
|Avaliar expressões MDX (Multidimensional Expressions)|<xref:Microsoft.AnalysisServices.AdomdServer.Expression><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdServer.Expression> oferece um modo de executar uma expressão MDX e de avaliá-la sob uma tupla especificada.|  
|Dar suporte à execução de funções MDX sem a criação de uma instrução MDX completa|<xref:Microsoft.AnalysisServices.AdomdServer.MDX><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDX> é conveniente para chamar funções MDX predefinidas sem usar o objeto <xref:Microsoft.AnalysisServices.AdomdServer.Expression>. As funções adicionais para o objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDX> deverão estar disponíveis em futuras versões.|  
|Representear o contexto de execução atual para o UDF|<xref:Microsoft.AnalysisServices.AdomdServer.Context><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdServer.Context> exibe informações como o cubo atual ou o modelo de mineração, além de várias coleções de metadados. Um uso chave do objeto <xref:Microsoft.AnalysisServices.AdomdServer.Context> é a propriedade <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy.CurrentMember%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy>. Esse uso chave permite que o autor do UDF ou do procedimento armazenado tome decisões baseado em qual membro de certa dimensão a consulta será feita.|  
|Criar conjuntos e tuplas|<xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder>, <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder><br /> <xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder> oferece um modo de criar conjuntos imutáveis, enquanto que <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder> oferece um modo de criar tuplas imutáveis.|  
|Dar suporte à conversão implícita entre os seis tipos básicos da linguagem MDX|<xref:Microsoft.AnalysisServices.AdomdServer.MDXValue><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDXValue> oferece a conversão implícita entre os seguintes tipos:<br /><br /> -   <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy><br />-   <xref:Microsoft.AnalysisServices.AdomdServer.Level><br />-   <xref:Microsoft.AnalysisServices.AdomdServer.Member><br />-   <xref:Microsoft.AnalysisServices.AdomdServer.Tuple><br />-   <xref:Microsoft.AnalysisServices.AdomdServer.Set><br />-Escalares, ou tipos de valor|  
  
## <a name="see-also"></a>Consulte também  
 [Programação do servidor no ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
