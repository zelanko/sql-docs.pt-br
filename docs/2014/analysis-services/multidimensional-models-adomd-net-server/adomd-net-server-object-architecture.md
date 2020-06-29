---
title: Arquitetura de objeto de servidor ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, object model
- object model [ADOMD.NET]
ms.assetid: bdc81de9-b390-4654-b62a-cd6c0c9ca10d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 33a8f420f985c9e62c7d7f275e7de370a6988e8d
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469051"
---
# <a name="adomdnet-server-object-architecture"></a>Arquitetura de objeto de servidor do ADOMD.NET
  Os objetos de servidor ADOMD.NET são objetos auxiliares que podem ser usados para criar UDFs (funções definidas pelo usuário) ou procedimentos armazenados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
> [!NOTE]  
>  Para usar o namespace `Microsoft.AnalysisServices.AdomdServer` (e esses objetos), adicione uma referência a msmgdsrv.dll ao projeto UDF ou ao procedimento armazenado.  
  
 ![Mostra as relações de objetos no servidor ADOMD.NET](../../analysis-services/dev-guide/media/adomdnetserverobjectmodel.gif "Mostra as relações de objetos no servidor ADOMD.NET")  
Modelo de objeto do ADOMD.NET  
  
 A interação com a hierarquia de objetos do ADOMD.NET normalmente começa com um ou mais objetos da camada superior, como descrito na tabela a seguir.  
  
|Para|Use este objeto|  
|--------|---------------------|  
|Avaliar expressões MDX (Multidimensional Expressions)|[Microsoft. AnalysisServices. AdomdServer. Expression](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120))<br /> O objeto [Microsoft. AnalysisServices. AdomdServer. Expression](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120)) fornece uma maneira de executar uma expressão MDX e avaliar essa expressão em uma tupla especificada.|  
|Dar suporte à execução de funções MDX sem a criação de uma instrução MDX completa|[Microsoft. AnalysisServices. AdomdServer. MDX](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120))<br /> O objeto [Microsoft. AnalysisServices. AdomdServer. MDX](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120)) é conveniente para chamar funções MDX predefinidas sem usar o objeto [Microsoft. AnalysisServices. AdomdServer. Expression](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120)) . Funções adicionais para o objeto [Microsoft. AnalysisServices. AdomdServer. MDX](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120)) devem estar disponíveis em versões futuras.|  
|Representear o contexto de execução atual para o UDF|[Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))<br /> O objeto [Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) expõe informações como o cubo atual ou o modelo de mineração e várias coleções de metadados. Um uso importante do objeto [Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) é a propriedade [Microsoft. AnalysisServices. AdomdServer. Hierarchy. CurrentMember *](/previous-versions/sql/sql-server-2014/ms137044(v=sql.120)) do objeto [Microsoft. AnalysisServices. AdomdServer. Hierarchy](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120)) . Esse uso chave permite que o autor do UDF ou do procedimento armazenado tome decisões baseado em qual membro de certa dimensão a consulta será feita.|  
|Criar conjuntos e tuplas|[Microsoft. AnalysisServices. AdomdServer. Setbuildr](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120)), [Microsoft. AnalysisServices. AdomdServer. TupleBuilder](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120))<br /> O [Microsoft. AnalysisServices. AdomdServer. Setbuildr](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120)) fornece uma maneira de criar conjuntos imutáveis, enquanto o [Microsoft. AnalysisServices. AdomdServer. TupleBuilder](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120)) fornece uma maneira de criar tuplas imutáveis.|  
|Dar suporte à conversão implícita entre os seis tipos básicos da linguagem MDX|[Microsoft. AnalysisServices. AdomdServer. MDXValue](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120))<br /> O objeto [Microsoft. AnalysisServices. AdomdServer. MDXValue](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120)) fornece conversão implícita e projeção entre os seguintes tipos:<br /><br /> -   [Microsoft. AnalysisServices. AdomdServer. Hierarchy](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. Level](/previous-versions/sql/sql-server-2014/ms143581(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. member](/previous-versions/sql/sql-server-2014/ms143820(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. tupla](/previous-versions/sql/sql-server-2014/ms145330(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. Set](/previous-versions/sql/sql-server-2014/ms144530(v=sql.120))<br />-Tipos escalares ou de valor|  
  
## <a name="see-also"></a>Consulte Também  
 [Programando o servidor no ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
