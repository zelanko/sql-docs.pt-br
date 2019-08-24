---
title: Executar uma avaliação de migração do serviço de integração SQL Server (Assistente de Migração de Dados) | Microsoft Docs
description: Saiba como usar Assistente de Migração de Dados para avaliar um serviço de integração de SQL Server local antes de migrar para o banco de dados SQL do Azure ou a instância gerenciada do banco de dados SQL do Azure
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14e53b3820e784916484cbe6a15ba82cd2ed5c8e
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70001368"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>Executar uma avaliação de migração do serviço de integração SQL Server com Assistente de Migração de Dados

As instruções passo a passo a seguir ajudam a executar sua primeira avaliação para migrar pacotes do SSIS (serviço de integração SQL Server) para o banco de dados SQL do Azure ou a instância gerenciada do banco de dados SQL do Azure, usando Assistente de Migração de Dados.

## <a name="create-an-assessment"></a>Criar uma avaliação

1. Selecione o ícone **novo** (+) e, em seguida, selecione o tipo de projeto de **avaliação** como **serviço de integração**.

1. Defina o tipo de servidor de origem e de destino.

    Selecione a origem como **SQL Server**e defina o tipo de servidor de destino como **banco de dados SQL do Azure** ou **instância gerenciada do banco de dados SQL do Azure**.

1. Clique em **Criar**.

    ![criar avaliação](media/dma-assess-ssis/dma-assess-ssis-create.png)

## <a name="add-sources-to-assess"></a>Adicionar fontes para avaliar

1. Siga a opção padrão e clique em **Avançar** em direção à **seleção de fontes**.

1. Insira o nome da instância do SQL Server, escolha o tipo de autenticação, defina as propriedades de conexão corretas.
1. Insira um caminho de pasta que contenha pacotes SSIS
1. Insira a senha de criptografia do pacote, se aplicável, e **Conecte-** se.
1. Selecione o sistema de arquivos para avaliar e, em seguida, selecione **Adicionar**.
  ![Adicionar origem](media/dma-assess-ssis/dma-assess-ssis-addsource.png)
1. Selecione **adicionar fontes** para abrir o menu de atalho de conexão, se precisar avaliar várias pastas.
1. Clique em **Iniciar avaliação**.
  ![Iniciar avaliação](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>Exibir os resultados

A categoria de problemas de compatibilidade fornece recursos com suporte parcial ou sem suporte que bloqueiam a migração de pacotes SSIS locais para Azure-SSIS Integration Runtime. Em seguida, ele fornece recomendações para ajudá-lo a resolver esses problemas.

![Exibir os resultados](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>Próximas etapas

- [Migrar pacotes SQL Server Integration Services para uma instância gerenciada do banco de dados SQL do Azure](https://docs.microsoft.com/en-us/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [Reimplantar pacotes SQL Server Integration Services no banco de dados SQL do Azure](https://docs.microsoft.com/en-us/azure/dms/how-to-migrate-ssis-packages)
