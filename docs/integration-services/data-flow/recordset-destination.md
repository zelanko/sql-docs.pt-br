---
title: Destino do conjunto de registros | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.recordsetdest.f1
helpviewer_keywords:
- Recordset destination
- ADO recordsets [Integration Services]
- destinations [Integration Services], Recordset
- in-memory ADO recordsets [Integration Services]
ms.assetid: be973cf1-c4ff-49f8-987e-314c08ef98e4
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4b5767204c23f5a8f98943c6f92d3c970121e2c8
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35411918"
---
# <a name="recordset-destination"></a>Destino do Conjunto de Registros
  O destino do conjunto de registros cria e popula um conjunto de registros ADO na memória. A forma do conjunto de registros é definida na entrada para o destino de conjunto de registros no tempo de design.  
  
## <a name="configuration-of-the-recordset-destination"></a>Configuração do destino do conjunto de registros  
 Configure o destino do conjunto de registros especificando a variável que armazena o conjunto de registros ADO.  
  
 No tempo de execução, um conjunto de registros ADO é gravado para a variável de tipo, Objeto, que é especificado na propriedade VariableName do destino do conjunto de registros. A variável torna o conjunto de registros disponível fora do fluxo de dados, onde pode ser usado por scripts e outros elementos de pacote.  
  
 Esta fonte tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas do destino Conjunto de Registros](../../integration-services/data-flow/recordset-destination-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Usar um destino do conjunto de registros](../../integration-services/data-flow/use-a-recordset-destination.md)  
  
  
