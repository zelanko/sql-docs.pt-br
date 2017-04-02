---
title: "Altera&#231;&#245;es Interruptivas em Recursos do Analysis Services no SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "alterações recentes [Analysis Services]"
  - "atualizando o Analysis Services"
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
caps.latest.revision: 55
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 53
---
# Altera&#231;&#245;es Interruptivas em Recursos do Analysis Services no SQL Server 2016
  Um *alteração interruptiva* faz com que um modelo de dados, código do aplicativo ou script não funcionem depois de atualizar o modelo ou o servidor.  
  
> [!NOTE]  
>  Por outro lado, uma *alteração de comportamento* é caracterizada como uma alteração de código que não interrompe um modelo ou aplicativo, mas apresenta um comportamento diferente de uma versão anterior.  Exemplos de alterações de comportamento podem incluir a alteração de um valor padrão ou a desabilitação de uma configuração de opções ou propriedades que anteriormente era permitida. Para saber mais sobre as alterações de comportamento nesta versão, confira [Behavior Changes to Analysis Services Features in SQL Server 2016](../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md).  
  
## Atualização de Versão do .NET 4.0  
 Bibliotecas de cliente de AMO (Analysis Services Management Objects), ADOMD.NET e o TOM (Tabular Object Model) em [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] agora são voltadas para o tempo de execução do .NET 4.0. Isso pode ser uma alteração interruptiva para aplicativos destinados ao .NET 3.5. Aplicativos que usam versões mais recentes desses assemblies agora devem ser voltados para o .NET 4.0 ou posterior.  
  
## Atualização de Versão do AMO  
 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] é uma atualização de versão para [Objetos de Gerenciamento do Analysis Services &#40;AMO&#41;](../Topic/Analysis%20Services%20Management%20Objects%20\(AMO\).md) e é uma alteração interruptiva em determinadas circunstâncias.  O código e os scripts existentes que chamam o AMO continuarão a ser executados como antes se você efetuar a atualização a partir de uma versão anterior. No entanto, se você precisar *recompilar* seu aplicativo e tiver como alvo uma instância [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] , é necessário adicionar o namespace a seguir para tornar o seu código ou script operacional:  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 O namespace [Microsoft.AnalysisServices.Core](../Topic/Microsoft.AnalysisServices.Core.md) agora é necessário sempre que a referenciar o assembly Microsoft. AnalysisServices em seu código. Objetos que estiveram anteriormente apenas no namespace do **Microsoft.AnalysisServices** são movidos para o namespace principal nesta versão, se o objeto for usado em cenários de tabela e cenários multidimensionais da mesma maneira.  Por exemplo, as APIs de servidor são realocadas para o namespace principal.  
  
 Apesar de agora haver vários namespaces, eles existem no mesmo assembly (Microsoft.AnalysisServices.dll).  
  
## Alterações de XEvent DISCOVER  
 Para dar um melhor suporte ao streaming de XEvent DISCOVER no SSMS para [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], `DISCOVER_XEVENT_TRACE_DEFINITION` é substituído pelos seguintes rastreamentos XEvent:  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  
  
## Consulte também  
 [Analysis Services Backward Compatibility](../analysis-services/analysis-services-backward-compatibility.md)  
  
  