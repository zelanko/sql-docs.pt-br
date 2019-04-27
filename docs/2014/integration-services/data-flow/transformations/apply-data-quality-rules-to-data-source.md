---
title: Aplicar regras de qualidade de dados à fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c420a52528662cecec1bae8e0e1718152279bc0e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770452"
---
# <a name="apply-data-quality-rules-to-data-source"></a>Aplicar regras de qualidade de dados à fonte de dados
  Você pode usar o DQS (Data Quality Services) para corrigir dados no fluxo de dados de pacote conectando a transformação de limpeza DQS à fonte de dados. Para obter mais informações sobre DQS, consulte [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md). Para obter mais informações sobre a transformação, consulte [DQS Cleansing Transformation](dqs-cleansing-transformation.md).  
  
 Quando você processar dados com a transformação de limpeza DQS, um projeto de qualidade de dados é criado no Data Quality Server. Você usa o Cliente Data Quality para gerenciar o projeto. Para obter mais informações, consulte [Gerenciar &#40;Abrir, desbloquear, renomear e excluir&#41; um projeto de qualidade de dados](../../../data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md).  
  
### <a name="to-correct-data-in-the-data-flow"></a>Para corrigir dados no fluxo de dados  
  
1.  Criar um pacote.  
  
2.  Adicione e configure a transformação Limpeza DQS. Para obter mais informações, consulte [DQS Cleansing Transformation Editor Dialog Box](../../dqs-cleansing-transformation-editor-dialog-box.md).  
  
3.  Conecte a transformação Limpeza DQS a uma fonte de dados.  
  
  
