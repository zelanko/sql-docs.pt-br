---
title: "Op&#231;&#245;es de Atributo Fixo e de Altera&#231;&#227;o (Assistente para Dimens&#245;es de Altera&#231;&#227;o Lenta) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.loaddimwizard.attriboption.f1"
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# Op&#231;&#245;es de Atributo Fixo e de Altera&#231;&#227;o (Assistente para Dimens&#245;es de Altera&#231;&#227;o Lenta)
  Use a caixa de diálogo **Opções de Atributo Fixo e de Alteração** para especificar como responder a mudanças nos atributos fixos e de alteração.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## Opções  
 **Atributos fixos**  
 Para os atributos fixos, indique se a tarefa falhará se uma mudança for detectada em um atributo fixo.  
  
 **Atributos de alteração**  
 Para alterar atributos, indique se a tarefa alterará registros antigos ou expirados, além de registros atuais, quando uma mudança for detectada em um atributo de alteração. Um registro expirado é um registro que foi substituído por um registro mais novo por uma alteração em um atributo histórico (uma alteração Tipo 2). A seleção desta opção pode impor requisitos de processamento adicionais em um objeto multidimensional construído no data warehouse relacional.  
  
## Consulte também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  