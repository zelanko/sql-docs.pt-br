---
title: Renderizar um instantâneo do histórico de relatórios usando o acesso à URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], report history
- history snapshots [Reporting Services]
- historical data [Reporting Services]
- snapshots [Reporting Services], URL access
- snapshots [Reporting Services], rendering report history
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: cc661c1241ce6d265fc949d7324ed4c54a5793f5
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56029497"
---
# <a name="render-a-report-history-snapshot-using-url-access"></a>Renderizar instantâneo de histórico de relatório com o acesso à URL
  Você pode renderizar um relatório com base em um instantâneo de histórico de relatório fornecendo o parâmetro *rs:Snapshot* e definindo seu valor como uma ID de instantâneo válida. O valor do parâmetro está no formato AAAA-MM-DDTHH:MM:SS, com base no padrão ISO (Organização Internacional de Padronização) 8601.  
  
 Se você omitir esse parâmetro, o relatório será renderizado de acordo com a execução do relatório e das configurações da opção de gerenciamento de cache do servidor de relatório. Para obter mais informações sobre a execução do relatório, consulte [Definir as propriedades do processamento de relatórios](report-server/set-report-processing-properties.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma URL que recupera um instantâneo de histórico de relatório:  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## <a name="see-also"></a>Consulte também  
 [Acesso à URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](url-access-parameter-reference.md)  
  
  
