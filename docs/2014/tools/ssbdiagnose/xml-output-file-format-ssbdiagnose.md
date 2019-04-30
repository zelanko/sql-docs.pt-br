---
title: Formato de arquivo de saída XML (ssbdiagnose) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose]
- ssbdiagnose
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 127e0b807e832272dc98270d811af310cc075bdd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63285674"
---
# <a name="xml-output-file-format-ssbdiagnose"></a>Formato de arquivo de saída XML (ssbdiagnose)
  O utilitário **ssbdiagnose** entrega sua saída como um arquivo XML quando você o executa com a opção **-XML** . O arquivo de saída XML lista informações de cabeçalho e erros encontrados na configuração ou conversa do [!INCLUDE[ssSB](../../includes/sssb-md.md)] analisadas. Você pode escrever um aplicativo para analisar ou reportar os erros listados no arquivo. Ou pode exibir o arquivo de XML em um editor de XML geral, como o Bloco de Notas XML.  
  
 Um arquivo de saída do **ssbdiangose** contém um elemento raiz DiagnosticInformation com dois tipos de filho:  
  
-   Um elemento Banner com informações de cabeçalho.  
  
-   Um elemento Issue para cada problema reportado por **ssbdiagnose**.  
  
## <a name="diagnosticinformation-root-element"></a>Elemento raiz DiagnosticInformation  
  
-   [Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](diagnosticinformation-element-ssbdiagnose.md)  
  
## <a name="banner-element"></a>Elemento Banner  
  
-   [Elemento Banner &#40;ssbdiagnose&#41;](banner-element-ssbdiagnose.md)  
  
## <a name="issue-element"></a>Elemento Issue  
  
-   [Elemento Issue &#40;ssbdiagnose&#41;](issue-element-ssbdiagnose.md)  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário ssbdiagnose &#40;Service Broker&#41;](ssbdiagnose-utility-service-broker.md)  
  
  
