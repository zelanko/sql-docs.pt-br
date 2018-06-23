---
title: Funcionalidade de servidor do ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: b74c6957-3f64-4e09-aa09-d06ee93f82fa
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 622a7c51bfd6c2a8a9defba70a412967a48dee50
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010552"
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
  
-   Você chamar um procedimento armazenado em sua própria com MDX [chamar](/sql/mdx/mdx-data-manipulation-call) instrução.  
  
-   Um procedimento armazenado pode conter qualquer número de parâmetros.  
  
-   Um procedimento armazenado pode retornar um conjunto de dados, um `IDataReader` ou um resultado vazio.  
  
 O exemplo a seguir usa o procedimento armazenado fictício `FinalSalesNumbers`:  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>Consulte também  
 [Programação do servidor no ADOMD.NET](adomd-net-server-programming.md)  
  
  
