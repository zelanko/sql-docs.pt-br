---
title: "Desenvolver tipos específicos de componentes de Script | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-data-flow-script-component-types
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40797e78a6229c063e634cd152daf3108f6340ed
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="developing-specific-types-of-script-components"></a>Desenvolvendo tipos específicos de componentes Script
  O componente de Script é uma ferramenta configurável que pode ser usada no fluxo de dados de um pacote para atender a quase todos os requisitos não atendidos pelas fontes, transformações e destinos incluídos no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Esta seção contém exemplos de código do componente Script que demonstram as quatro opções para configurar o componente Script:  
  
-   Como uma origem.  
  
-   Como uma transformação com saídas síncronas.  
  
-   Como uma transformação com saídas assíncronas.  
  
-   Como um destino.  
  
 Para obter exemplos adicionais do componente Script, consulte [Exemplos de componentes Script adicionais](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Criar uma origem com o componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)  
 Explica e demonstra como criar uma origem de fluxo de dados com o componente de Script.  
  
 [Criar uma transformação síncrona com o componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 Explica e demonstra como criar uma transformação de fluxo de dados com saídas síncronas usando o componente Script. Esse tipo de transformação modifica linhas de dados no local à medida que passam pelo componente.  
  
 [Criar uma transformação assíncrona com o componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 Explica e demonstra como criar uma transformação de fluxo de dados com saídas assíncronas usando o componente Script. Esse tipo de transformação tem que ler todas as linhas de dados antes de adicionar mais informações, como agregações calculadas, aos dados que passam pelo componente.  
  
 [Criar um destino com o componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 Explica e demonstra como criar um destino de fluxo de dados com o componente de Script.  
  
## <a name="see-also"></a>Consulte também  
 [Comparar soluções de script e objetos personalizados](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Desenvolvendo tipos específicos de componentes de fluxo de dados](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  
