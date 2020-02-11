---
title: Destino do conjunto de registros | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.recordsetdest.f1
helpviewer_keywords:
- Recordset destination
- ADO recordsets [Integration Services]
- destinations [Integration Services], Recordset
- in-memory ADO recordsets [Integration Services]
ms.assetid: be973cf1-c4ff-49f8-987e-314c08ef98e4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0553b1cbbd75196fa8534cf6bf64c58c1dad206b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62770902"
---
# <a name="recordset-destination"></a>Destino do Conjunto de Registros
  O destino do conjunto de registros cria e popula um conjunto de registros ADO na memória. A forma do conjunto de registros é definida na entrada para o destino de conjunto de registros no tempo de design.  
  
## <a name="configuration-of-the-recordset-destination"></a>Configuração do destino do conjunto de registros  
 Configure o destino do conjunto de registros especificando a variável que armazena o conjunto de registros ADO.  
  
 No tempo de execução, um conjunto de registros ADO é gravado para a variável de tipo, Objeto, que é especificado na propriedade VariableName do destino do conjunto de registros. A variável torna o conjunto de registros disponível fora do fluxo de dados, onde pode ser usado por scripts e outros elementos de pacote.  
  
 Esta fonte tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas do destino do conjunto de registros](recordset-destination-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Usar um destino do conjunto de registros](recordset-destination.md)  
  
  
