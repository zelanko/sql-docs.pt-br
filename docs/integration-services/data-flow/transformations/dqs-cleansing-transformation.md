---
title: "Transformação de limpeza do DQS | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2851f1310e241dd921e0777408e000eb37836a81
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="dqs-cleansing-transformation"></a>Transformação de Limpeza DQS
  A transformação de Limpeza DQS usa o DQS (Data Quality Services) para corrigir dados de uma fonte de dados conectada com a aplicação de regras aprovadas, que foram criadas para a fonte de dados conectada ou uma fonte de dados semelhante. Para obter informações sobre regras de correção de dados, consulte [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md). Para obter mais informações sobre o DQS, consulte [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md).  
  
 Para determinar se os dados precisam ser corrigidos, a transformação de Limpeza DQS processa dados de uma coluna de entrada quando as seguintes condições são verdadeiras:  
  
-   A coluna é selecionada para correção de dados.  
  
-   O tipo de dados da coluna tem suporte da correção de dados.  
  
-   A coluna é mapeada para um domínio que tem um tipo de dados compatível.  
  
 A transformação também inclui uma saída de erro que você configura para tratar erros em nível de linha. Para configurar a saída de erro, use o **Editor de Transformação de Limpeza DQS**.  
  
 Você pode incluir [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) no fluxo de dados para identificar linhas de dados que são provavelmente duplicadas.  
  
## <a name="data-quality-projects-and-values"></a>Projetos de qualidade de dados e valores  
 Quando você processar dados com a transformação de limpeza DQS, um projeto de limpeza é criado no Data Quality Server. Você usa o Cliente Data Quality para gerenciar o projeto. Além disso, você pode usar o Cliente Data Quality para importar os valores de projeto em um domínio da base de dados de conhecimento do DQS. Você só pode importar os valores para um domínio (ou domínio vinculado) que a transformação de limpeza DQS tiver configurado para usar.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
-   [Abrir projetos do Integration Services no cliente Data Quality](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Import Cleansing Project Values into a Domain](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [Aplicar regras de qualidade de dados à fonte de dados](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Abrir, desbloquear, renomear e excluir um projeto do Data Quality](https://msdn.microsoft.com/library/hh510417.aspx)  
  
-   Artigo [Dados complexos de limpeza usando domínios compostos](http://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)em social.technet.microsoft.com.  
  
  
