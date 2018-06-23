---
title: Melhores práticas para tratamento de exceção do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], best practices
ms.assetid: 72fecf28-f02e-4338-b50f-0b21f520302d
caps.latest.revision: 33
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4827af143c1eca89b4873387fc4db9fd454c06c1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116071"
---
# <a name="best-practices-for-reporting-services-exception-handling"></a>Práticas recomendadas para a manipulação de exceção do Reporting Services
  Durante o desenvolvimento de aplicativos do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], existem várias metodologias que você pode usar para eliminar ou reduzir a ocorrência de exceções. Quando houver exceções, forneça mensagens de erro claras e concisas ao usuário e adicione manipulação de exceção adequada para impedir que seus aplicativos sejam encerrados de forma inesperada.  
  
 Um aplicativo que envia solicitações ao serviço Web Servidor de Relatório deve fazer o seguinte:  
  
-   Evitar as exceções impedindo quantas solicitações inválidas for possível.  
  
-   Capturar exceções e fornecer código de manipulação de erro específico sempre que possível.  
  
-   Lidar com casos de erro que não lançam exceções.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Impedir solicitações inválidas](preventing-invalid-requests.md)|Descreve técnicas para impedir que solicitações que não são válidas sejam enviadas ao servidor de relatório.|  
|[Usar blocos try e catch](using-try-and-catch-blocks.md)|Descreve como aprimorar ainda mais a confiabilidade de seu aplicativo com blocos try/catch.|  
|[Manipular avisos e casos que não causam exceções](handling-warnings-and-cases-that-do-not-cause-exceptions.md)|Explica como manipular erros que não resultam em uma exceção é lançada pelo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Usar a propriedade Detail para manipular erros específicos](using-the-detail-property-to-handle-specific-errors.md)|Explica como tratar erros específicos de forma programática usando a propriedade **Detail** do objeto **SoapException**.|  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Detail](../soapexception-class/detail-property.md)   
 [Introdução ao tratamento de exceção no Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException do Reporting Services +](../soapexception-class/reporting-services-soapexception-class.md)  
  
  