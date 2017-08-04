---
title: "Transformação copiar coluna | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.copycolumntrans.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3039b400b136b62840c40b463bb1d8f53a43251d
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="copy-column-transformation"></a>transformação Copiar Coluna
  A transformação Copiar Coluna cria novas colunas com a cópia de colunas de entrada e a adição de novas colunas à saída da transformação. Mais tarde no fluxo de dados, transformações diferentes podem ser aplicadas às cópias da coluna. Por exemplo, você pode usar a transformação Copiar Coluna para criar uma cópia de uma coluna e, em seguida, converter os dados copiados em caracteres maiúsculos por meio da transformação Mapa de Caracteres ou aplicar agregações à coluna nova por meio da transformação Agregação.  
  
## <a name="configuration-of-the-copy-column-transformation"></a>Configuração da transformação Copiar Coluna  
 Configure a transformação Copiar Coluna especificando as colunas de entrada a serem copiadas. É possível criar várias cópias de uma coluna ou criar cópias de várias colunas em uma operação.  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Copiar Coluna** , consulte [Editor de Transformação Copiar Coluna](../../../integration-services/data-flow/transformations/copy-column-transformation-editor.md).  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
