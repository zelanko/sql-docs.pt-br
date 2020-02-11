---
title: Salvar e carregar avaliações com Assistente de Migração de Dados
description: Saiba como usar Assistente de Migração de Dados para salvar e carregar avaliações.
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 995b6b131d9e65ca7a91ce9053583a036fd80fbb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75840515"
---
# <a name="save-and-load-assessments-with-data-migration-assistant"></a>Salvar e carregar avaliações com Assistente de Migração de Dados

As instruções passo a passo a seguir ajudam a usar o Assistente de Migração de Dados v 5.0 ou posterior para salvar uma avaliação de banco de dados em um arquivo e, em seguida, carregar uma avaliação de um arquivo.

> [!NOTE]
> Além de carregar avaliações salvas usando a versão mais recente do DMA, os usuários também podem aproveitar esse recurso para carregar avaliações exportadas como arquivos. JSON de versões anteriores do Assistente de Migração de Dados para exibir os resultados em v 5.0 e posterior.

## <a name="saving-an-assessment-to-a-file"></a>Salvando uma avaliação em um arquivo

1. Depois de executar uma avaliação usando Assistente de Migração de Dados, selecione **Salvar avaliação**.

   ![Abrindo a caixa de diálogo Salvar avaliação](../dma/media/dma-save-load-assessments/dma-open-save-dialog.png)

   O padrão **salvar...** a caixa de diálogo é exibida.

   > [!NOTE]
   > Para obter mais informações sobre como executar uma avaliação no Assistente de Migração de Dados, consulte o artigo [executar uma avaliação de migração de SQL Server com o assistente de migração de dados](../dma/dma-assesssqlonprem.md).

2. Especifique um nome para o arquivo e, em seguida, selecione **salvar**.

   ![Nomeando e salvando um arquivo de avaliação](../dma/media/dma-save-load-assessments/dma-name-save-assessment.png)

## <a name="loading-an-assessment-saved-to-a-file"></a>Carregando uma avaliação salva em um arquivo

1. Para carregar uma avaliação que você salvou anteriormente em um arquivo, inicie Assistente de Migração de Dados e, em seguida, na guia **todas as avaliações** , selecione **avaliação de carga**.

   ![Abrindo a caixa de diálogo avaliação de carga](../dma/media/dma-save-load-assessments/dma-open-load-dialog.png)

2. Navegue até o arquivo de avaliação salvo que você deseja carregar, selecione o arquivo e, em seguida, selecione **abrir**.

   ![Abrindo um arquivo de avaliação](../dma/media/dma-save-load-assessments/dma-open-assessment.png)

   Uma entrada para a avaliação que você carregou aparece na guia **todas as avaliações** .

   ![Exibindo a entrada da avaliação](../dma/media/dma-save-load-assessments/dma-display-assessment-entry.png)

3. Selecione a entrada avaliação e, em seguida, selecione **abrir avaliação**.

   ![Abrindo os detalhes da avaliação](../dma/media/dma-save-load-assessments/dma-open-assessment-detail.png)

   Agora Assistente de Migração de Dados exibe detalhes da avaliação que você executou anteriormente.

   ![Exibindo detalhes da avaliação](../dma/media/dma-save-load-assessments/dma-display-assessment-detail.png)
