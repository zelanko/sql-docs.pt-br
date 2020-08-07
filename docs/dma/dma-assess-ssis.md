---
title: Criar uma avaliação de migração do SSIS com o Assistente de Migração de Dados
description: Saiba como usar Assistente de Migração de Dados para avaliar um SSIS (serviço de integração do SQL Server) local antes de migrar para o banco de dados SQL do Azure ou o SQL do Azure Instância Gerenciada
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
ms.custom: seo-lt-2019
ms.openlocfilehash: 9a7b077c3046b2f0c7e50b7ec20f68a5544e91e1
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87822191"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>Executar uma avaliação de migração do serviço de integração SQL Server com Assistente de Migração de Dados

## <a name="prerequisites"></a>Pré-requisitos

Para avaliar os pacotes do SSIS (Integration Service) SQL Server, os componentes a seguir precisam ser instalados com o Assistente de Migração de Dados:

- SQL Server Integration Service com a mesma versão que os pacotes do SSIS para avaliar.
- Azure Feature Pack ou outros componentes de terceiros se os pacotes do SSIS para avaliar tiverem esses componentes.  

O DMA precisa ser executado com acesso de **administrador** para avaliar pacotes do SSIS no repositório de pacotes.

## <a name="performance-assessments"></a>Avaliações de desempenho

As instruções passo a passo a seguir ajudam você a executar sua primeira avaliação para migrar pacotes do SSIS (serviço de integração SQL Server) para o banco de dados SQL do Azure ou o SQL Instância Gerenciada do Azure, usando Assistente de Migração de Dados.

## <a name="create-an-assessment"></a>Criar uma avaliação

1. Selecione o ícone **novo** (+) e, em seguida, selecione o tipo de projeto de **avaliação** como **serviço de integração**.

1. Defina o tipo de servidor de origem e de destino.

    Selecione a origem como **SQL Server**e defina o tipo de servidor de destino como **banco de dados SQL do Azure** ou **SQL do Azure instância gerenciada**.

1. Clique em **Criar**.

    ![criar avaliação](media/dma-assess-ssis/dma-assess-ssis-create.png)

## <a name="connect-to-a-server"></a>Conectar-se a um servidor

1. Siga a opção padrão e clique em **Avançar** em direção à **seleção de fontes**.
1. Insira o nome da instância do SQL Server, escolha o tipo de autenticação, defina as propriedades de conexão corretas.
1. Adicional Insira um caminho de pasta que contenha pacotes SSIS.
1. Adicional Insira a senha de criptografia do pacote, se aplicável.
1. Clique em **conectar-se** ao SQL Server de origem.
  ![Adicionar origem](media/dma-assess-ssis/dma-assess-ssis-addsource.png)

## <a name="add-sources-to-assess"></a>Adicionar fontes para avaliar

1. Selecione os tipos de armazenamento de pacote SSIS para avaliar e, em seguida, selecione **Adicionar**.
![Adicionar origem](media/dma-assess-ssis/dma-assess-ssis-addsource-type.png)
1. Selecione **adicionar fontes** para abrir o menu de atalho de conexão, se precisar avaliar várias pastas.
1. Clique em **Iniciar avaliação**.
  ![Iniciar avaliação](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>Exibir os resultados

A categoria de problemas de compatibilidade fornece recursos com suporte parcial ou sem suporte que bloqueiam a migração de pacotes SSIS locais para Azure-SSIS Integration Runtime. Em seguida, ele fornece recomendações para ajudá-lo a resolver esses problemas.

![Exibir os resultados](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>Próximas etapas

- [Migrar cargas de trabalho do SSIS locais para o SSIS em visão geral do ADF](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview)
- [Migrar pacotes SQL Server Integration Services para um SQL do Azure Instância Gerenciada](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [Reimplantar pacotes SQL Server Integration Services no banco de dados SQL do Azure](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages)
