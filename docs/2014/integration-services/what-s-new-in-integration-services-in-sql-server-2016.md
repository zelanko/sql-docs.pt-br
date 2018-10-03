---
title: O que&#39;s novos (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7427402df49625c04ab7d1c38dd6bcfe3298e0ed
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048536"
---
# <a name="what39s-new-integration-services"></a>O que&#39;s novos (Integration Services)
  O [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] está inalterado desde a versão anterior.  
  
 Para obter informações sobre outros [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] produtos e tecnologias, consulte [o que há de novo no SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).  
  
 Para obter mais informações sobre alterações relacionadas ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence, consulte [o que há de novo no Analysis Services e Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md).  
  
##  <a name="ValidateXML"></a> Saída de validação de XML avançada na Tarefa XML  
 Validar documentos XML e obtenha saída de erros completa habilitando a `ValidationDetails` propriedade da tarefa XML. Antes do `ValidationDetails` propriedade estava disponível, a validação do XML pela tarefa XML retornava apenas um resultado true ou false, sem informações sobre erros ou suas localizações. Agora, quando você define `ValidationDetails` como true, a saída do arquivo contém informações detalhadas sobre cada erro, incluindo o número de linha e a posição. Você pode usar essas informações para entender, localizar e corrigir erros em documentos XML. Para obter mais informações, consulte [Validate XML with the XML Task](control-flow/xml-task.md).  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] introduziu o `ValidationDetails` propriedade em [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 2. Essa nova propriedade não foi anunciada ou documentada naquele momento. O `ValidationDetails` propriedade também está disponível no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e no SQL Server 2016.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
