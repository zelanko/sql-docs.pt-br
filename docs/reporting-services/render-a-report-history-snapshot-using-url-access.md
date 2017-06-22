---
title: "Renderizar um instantâneo de histórico de relatório com acesso à URL | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- URL access [Reporting Services], report history
- history snapshots [Reporting Services]
- historical data [Reporting Services]
- snapshots [Reporting Services], URL access
- snapshots [Reporting Services], rendering report history
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 38237ef30d403dab78f8fedd00caa97ebdaf0b29
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="render-a-report-history-snapshot-using-url-access"></a>Renderizar instantâneo de histórico de relatório com o acesso à URL
  Você pode renderizar um relatório com base em um instantâneo de histórico de relatório fornecendo o parâmetro *rs:Snapshot* e definindo seu valor como uma ID de instantâneo válida. O valor do parâmetro está no formato AAAA-MM-DDTHH:MM:SS, com base no padrão ISO (Organização Internacional de Padronização) 8601.  
  
 Se você omitir esse parâmetro, o relatório será renderizado de acordo com a execução do relatório e das configurações da opção de gerenciamento de cache do servidor de relatório. Para obter mais informações sobre a execução do relatório, consulte [Definir as propriedades do processamento de relatórios](../reporting-services/report-server/set-report-processing-properties.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma URL que recupera um instantâneo de histórico de relatório:  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## <a name="see-also"></a>Consulte também  
 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md)  
  
  
