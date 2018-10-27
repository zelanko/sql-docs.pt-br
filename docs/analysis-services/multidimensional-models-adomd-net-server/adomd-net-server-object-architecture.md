---
title: Arquitetura de objeto de servidor do ADOMD.NET | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9a527f9fd3a1d41b0b41190952705a4066b402ac
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144961"
---
# <a name="adomdnet-server-object-architecture"></a>Arquitetura de objeto de servidor do ADOMD.NET
  Os objetos do servidor ADOMD.NET são auxiliares que pode ser usado para criar funções definidas pelo usuário (UDFs) ou procedimentos armazenados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Para usar o **adomdserver** namespace (e esses objetos), uma referência para a msmgdsrv deve ser adicionada ao projeto UDF ou procedimento armazenado.  
  
 ![Mostra as relações de objeto no servidor do ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-server/media/adomdnetserverobjectmodel.gif "mostra as relações de objeto no servidor do ADOMD.NET")  
Modelo de objeto do ADOMD.NET  
  
 A interação com a hierarquia de objetos do ADOMD.NET normalmente começa com um ou mais objetos da camada superior, como descrito na tabela a seguir.  
  
|Para|Use este objeto|  
|--------|---------------------|  
|Avaliar expressões MDX (Multidimensional Expressions)|<xref:Microsoft.AnalysisServices.AdomdServer.Expression><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdServer.Expression> oferece um modo de executar uma expressão MDX e de avaliá-la sob uma tupla especificada.|  
|Dar suporte à execução de funções MDX sem a criação de uma instrução MDX completa|<xref:Microsoft.AnalysisServices.AdomdServer.MDX><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDX> é conveniente para chamar funções MDX predefinidas sem usar o objeto <xref:Microsoft.AnalysisServices.AdomdServer.Expression>. As funções adicionais para o objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDX> deverão estar disponíveis em futuras versões.|  
|Representear o contexto de execução atual para o UDF|<xref:Microsoft.AnalysisServices.AdomdServer.Context><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdServer.Context> exibe informações como o cubo atual ou o modelo de mineração, além de várias coleções de metadados. Um uso chave do objeto <xref:Microsoft.AnalysisServices.AdomdServer.Context> é a propriedade <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy.CurrentMember%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy>. Esse uso chave permite que o autor do UDF ou do procedimento armazenado tome decisões baseado em qual membro de certa dimensão a consulta será feita.|  
|Criar conjuntos e tuplas|<xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder>, <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder><br /> <xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder> oferece um modo de criar conjuntos imutáveis, enquanto que <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder> oferece um modo de criar tuplas imutáveis.|  
|Dar suporte à conversão implícita entre os seis tipos básicos da linguagem MDX|<xref:Microsoft.AnalysisServices.AdomdServer.MDXValue><br /> O objeto <xref:Microsoft.AnalysisServices.AdomdServer.MDXValue> oferece a conversão implícita entre os seguintes tipos:<br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Level><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Member><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Tuple><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Set><br /><br /> Escalar ou tipos de valor|  
  
## <a name="see-also"></a>Consulte também  
 [Programação do servidor no ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
