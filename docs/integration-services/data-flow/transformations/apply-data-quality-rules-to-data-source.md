---
description: Aplicar regras de qualidade de dados à fonte de dados
title: Aplicar regras de qualidade de dados à fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: afccf7296d27331d7b76ba5e4978faca2126060f
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194638"
---
# <a name="apply-data-quality-rules-to-data-source"></a>Aplicar regras de qualidade de dados à fonte de dados

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Você pode usar o DQS (Data Quality Services) para corrigir dados no fluxo de dados de pacote conectando a transformação de limpeza DQS à fonte de dados. Para obter mais informações sobre DQS, consulte [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md). Para obter mais informações sobre a transformação, consulte [DQS Cleansing Transformation](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md).  
  
 Quando você processar dados com a transformação de limpeza DQS, um projeto de qualidade de dados é criado no Data Quality Server. Você usa o Cliente Data Quality para gerenciar o projeto. Para obter mais informações, consulte [Abrir, desbloquear, renomear e excluir um projeto de qualidade de dados](../../../data-quality-services/open-unlock-rename-and-delete-a-data-quality-project.md).  
  
### <a name="to-correct-data-in-the-data-flow"></a>Para corrigir dados no fluxo de dados  
  
1.  Criar um pacote.  
  
2.  Adicione e configure a transformação Limpeza DQS. Para obter mais informações, consulte [DQS Cleansing Transformation Editor Dialog Box](./dqs-cleansing-transformation.md).  
  
3.  Conecte a transformação Limpeza DQS a uma fonte de dados.  
  
