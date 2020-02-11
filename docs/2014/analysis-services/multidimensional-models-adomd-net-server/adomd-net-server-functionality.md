---
title: Funcionalidade do servidor ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: b74c6957-3f64-4e09-aa09-d06ee93f82fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc127a8bafc9ad2f53465caeca013d5033e5c396
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702972"
---
# <a name="adomdnet-server-functionality"></a>Funcionalidade de servidor do ADOMD.NET
  Todos os objetos de servidor do ADOMD.NET oferecem acesso somente leitura aos dados e metadados do servidor. Para recuperar dados e metadados, use o modelo de objeto de servidor do ADOMD.NET, uma vez que o modelo de objeto de servidor não dá suporte a conjuntos de linhas do esquema.  
  
 Com os objetos de servidor do ADOMD.NET, você pode criar uma UDF (função definida pelo usuário) ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]um procedimento armazenado para. Estes métodos em processo são chamados por instruções de consulta criadas em linguagens como MDX (Multidimensional Expressions), DMX (Data Mining Extensions) ou SQL. Esses métodos em processo também oferecem funcionalidade agregada sem as latências associadas às comunicações de rede.  
  
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
  
-   Você chama um procedimento armazenado por conta própria com a instrução MDX [Call](/sql/mdx/mdx-data-manipulation-call) .  
  
-   Um procedimento armazenado pode conter qualquer número de parâmetros.  
  
-   Um procedimento armazenado pode retornar um conjunto de dados, um `IDataReader` ou um resultado vazio.  
  
 O exemplo a seguir usa o procedimento armazenado fictício `FinalSalesNumbers`:  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Programando o servidor no ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
