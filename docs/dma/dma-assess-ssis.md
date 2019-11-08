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
ms.openlocfilehash: 84b498cbaf7a2f3d1118894157c17b8270259afa
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632875"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>Executar uma avaliação de migração do serviço de integração SQL Server com Assistente de Migração de Dados

As instruções passo a passo a seguir ajudam a executar sua primeira avaliação para migrar pacotes do SSIS (serviço de integração SQL Server) para o banco de dados SQL do Azure ou a instância gerenciada do banco de dados SQL do Azure, usando Assistente de Migração de Dados.

## <a name="create-an-assessment"></a>Criar uma avaliação

1. Selecione o ícone **novo** (+) e, em seguida, selecione o tipo de projeto de **avaliação** como **serviço de integração**.

1. Defina o tipo de servidor de origem e de destino.

    Selecione a origem como **SQL Server**e defina o tipo de servidor de destino como **banco de dados SQL do Azure** ou **instância gerenciada do banco de dados SQL do Azure**.

1. Clique em **Criar**.

    ![criar avaliação](media/dma-assess-ssis/dma-assess-ssis-create.png)

## <a name="connect-to-a-server"></a>Conectar a um servidor

1. Siga a opção padrão e clique em **Avançar** em direção à **seleção de fontes**.
1. Insira o nome da instância do SQL Server, escolha o tipo de autenticação, defina as propriedades de conexão corretas.
1. Adicional Insira um caminho de pasta que contenha pacotes SSIS.
1. Adicional Insira a senha de criptografia do pacote, se aplicável.
1. Clique em **conectar-se** ao SQL Server de origem.
  ![adicionar](media/dma-assess-ssis/dma-assess-ssis-addsource.png) de origem

## <a name="add-sources-to-assess"></a>Adicionar fontes para avaliar

1. Selecione os tipos de armazenamento de pacote SSIS para avaliar e, em seguida, selecione **Adicionar**.
![adicionar](media/dma-assess-ssis/dma-assess-ssis-addsource-type.png) de origem
1. Selecione **adicionar fontes** para abrir o menu de atalho de conexão, se precisar avaliar várias pastas.
1. Clique em **Iniciar avaliação**.
  ![iniciar a avaliação](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>Exibir os resultados

A categoria de problemas de compatibilidade fornece recursos com suporte parcial ou sem suporte que bloqueiam a migração de pacotes SSIS locais para Azure-SSIS Integration Runtime. Em seguida, ele fornece recomendações para ajudá-lo a resolver esses problemas.

![Exibir os resultados](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>Próximas etapas

- [Migrar cargas de trabalho do SSIS locais para o SSIS em visão geral do ADF](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview)
- [Migrar pacotes SQL Server Integration Services para uma instância gerenciada do banco de dados SQL do Azure](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [Reimplantar pacotes SQL Server Integration Services no banco de dados SQL do Azure](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages)
