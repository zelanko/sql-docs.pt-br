---
title: Copiar Transformação de Coluna | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.copycolumntrans.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d150aa7bcf77268cdfdbc3b037e28f358a115a97
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939653"
---
# <a name="copy-column-transformation"></a>transformação Copiar Coluna
  A transformação Copiar Coluna cria novas colunas com a cópia de colunas de entrada e a adição de novas colunas à saída da transformação. Mais tarde no fluxo de dados, transformações diferentes podem ser aplicadas às cópias da coluna. Por exemplo, você pode usar a transformação Copiar Coluna para criar uma cópia de uma coluna e, em seguida, converter os dados copiados em caracteres maiúsculos por meio da transformação Mapa de Caracteres ou aplicar agregações à coluna nova por meio da transformação Agregação.  
  
## <a name="configuration-of-the-copy-column-transformation"></a>Configuração da transformação Copiar Coluna  
 Configure a transformação Copiar Coluna especificando as colunas de entrada a serem copiadas. É possível criar várias cópias de uma coluna ou criar cópias de várias colunas em uma operação.  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Copiar Coluna** , consulte [Editor de Transformação Copiar Coluna](../../copy-column-transformation-editor.md).  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas da transformação](transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de dados](../data-flow.md)   
 [Transformações do Integration Services](integration-services-transformations.md)  
  
  
