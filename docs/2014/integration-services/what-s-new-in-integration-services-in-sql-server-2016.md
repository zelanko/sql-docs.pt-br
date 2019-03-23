---
title: O que&#39;s novos (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6eda4eb4f01819bd569a472df01a276c5f270f31
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58383099"
---
# <a name="what39s-new-integration-services"></a>O que&#39;s novos (Integration Services)
  O [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] está inalterado desde a versão anterior.  
  
 Para obter informações sobre outros [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] produtos e tecnologias, consulte [o que há de novo no SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).  
  
 Para obter mais informações sobre alterações relacionadas ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence, consulte [o que há de novo no Analysis Services e Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md).  
  
##  <a name="ValidateXML"></a> Saída de validação de XML avançada na Tarefa XML  
 Valide documentos XML e obtenha saída de erros completa habilitando a propriedade `ValidationDetails` da tarefa XML. Antes da disponibilidade da propriedade `ValidationDetails`, a validação do XML pela tarefa XML retornava apenas um resultado true ou false, sem informações sobre erros ou suas localizações. Agora, quando você define `ValidationDetails` como true, o arquivo de saída contém informações detalhadas sobre cada erro, incluindo o número de linha e a posição. Você pode usar essas informações para entender, localizar e corrigir erros em documentos XML. Para obter mais informações, consulte [Validate XML with the XML Task](control-flow/xml-task.md).  
  
 O [!INCLUDE[ssIS](../includes/ssis-md.md)] introduziu a propriedade `ValidationDetails` no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 2. Essa nova propriedade não foi anunciada ou documentada naquele momento. A propriedade `ValidationDetails` também está disponível no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e no SQL Server 2016.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
