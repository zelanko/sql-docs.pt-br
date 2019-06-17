---
title: Funcionalidade de servidor do ADOMD.NET | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c1f37be45b702828d3c663eac0fb575a0af3bbd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63059447"
---
# <a name="adomdnet-server-functionality"></a>Funcionalidade de servidor do ADOMD.NET
  Todos os objetos de servidor do ADOMD.NET oferecem acesso somente leitura aos dados e metadados do servidor. Para recuperar dados e metadados, use o modelo de objeto de servidor do ADOMD.NET, uma vez que o modelo de objeto de servidor não dá suporte a conjuntos de linhas do esquema.  
  
 Com os objetos de servidor do ADOMD.NET, você pode criar uma função definida pelo usuário (UDF) ou um procedimento armazenado para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Estes métodos em processo são chamados por instruções de consulta criadas em linguagens como MDX (Multidimensional Expressions), DMX (Data Mining Extensions) ou SQL. Esses métodos em processo também oferecem funcionalidade agregada sem as latências associadas às comunicações de rede.  
  
> [!NOTE]  
>  O objeto <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> só dá suporte a DMX.  
  
## <a name="what-is-a-udf"></a>O que é um UDF?  
 Um *UDF* é um método que tem as seguintes características:  
  
-   Você pode chamar o UDF no contexto de uma consulta.  
  
-   O UDF pode conter qualquer número de parâmetros.  
  
-   O UDF pode retornar vários tipos de dados.  
  
 O exemplo a seguir usa o UDF fictício `FinalSalesNumber`:  
  
```  
SELECT SalesPerson.Name ON ROWS,  
       FinalSalesNumber() ON COLUMNS  
FROM SalesModel  
```  
  
## <a name="what-is-a-stored-procedure"></a>O que é um procedimento armazenado?  
 Um *procedimento armazenado* é um método que tem as seguintes características:  
  
-   Você chamar um procedimento armazenado em sua própria com o MDX [chamar](../../mdx/mdx-data-manipulation-call.md) instrução.  
  
-   Um procedimento armazenado pode conter qualquer número de parâmetros.  
  
-   Um procedimento armazenado pode retornar um conjunto de dados, uma **IDataReader**, ou um resultado vazio.  
  
 O exemplo a seguir usa o procedimento armazenado fictício `FinalSalesNumbers`:  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>Consulte também  
 [Programação do servidor no ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
