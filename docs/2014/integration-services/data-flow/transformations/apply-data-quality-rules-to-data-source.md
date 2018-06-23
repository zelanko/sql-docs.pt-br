---
title: Aplicar regras de qualidade de dados à fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 48ed6d35bb9955579041ce6e4b1f1c4d35617ace
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010705"
---
# <a name="apply-data-quality-rules-to-data-source"></a>Aplicar regras de qualidade de dados à fonte de dados
  Você pode usar o DQS (Data Quality Services) para corrigir dados no fluxo de dados de pacote conectando a transformação de limpeza DQS à fonte de dados. Para obter mais informações sobre DQS, consulte [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md). Para obter mais informações sobre a transformação, consulte [DQS Cleansing Transformation](dqs-cleansing-transformation.md).  
  
 Quando você processar dados com a transformação de limpeza DQS, um projeto de qualidade de dados é criado no Data Quality Server. Você usa o Cliente Data Quality para gerenciar o projeto. Para obter mais informações, consulte [Gerenciar &#40;Abrir, desbloquear, renomear e excluir&#41; um projeto de qualidade de dados](../../../data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md).  
  
### <a name="to-correct-data-in-the-data-flow"></a>Para corrigir dados no fluxo de dados  
  
1.  Criar um pacote.  
  
2.  Adicione e configure a transformação Limpeza DQS. Para obter mais informações, consulte [DQS Cleansing Transformation Editor Dialog Box](../../dqs-cleansing-transformation-editor-dialog-box.md).  
  
3.  Conecte a transformação Limpeza DQS a uma fonte de dados.  
  
  