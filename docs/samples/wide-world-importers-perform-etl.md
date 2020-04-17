---
title: WideWorldImportersDW - Fluxo de trabalho ETL | Microsoft Docs
description: Use o pacote ETL com o SSIS (SSIS) para migrar periodicamente dados do banco de dados WideWorldImporters para o WideWorldImportersDW.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 98ce2b9aa11b2e1381da1f16455df8a2c0d3f243
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487425"
---
# <a name="wideworldimportersdw-etl-workflow"></a>Fluxo de trabalho WideWorldImportersDW ETL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Use o *pacote etl WWI_Integration* para migrar dados do banco de dados WideWorldImporters para o banco de dados WideWorldImportersDW como alterações de dados. O pacote é executado periodicamente (geralmente diariamente).

O pacote garante alto desempenho usando os Serviços de Integração do Servidor SQL para orquestrar operações T-SQL em massa (em vez de transformações separadas nos Serviços de Integração).

As dimensões são carregadas primeiro e, em seguida, as tabelas de fato são carregadas. Você pode refazer o pacote a qualquer momento após uma falha.

O fluxo de trabalho é assim:

 ![Fluxo de trabalho ETL do WideWorldImporters](media/wide-world-importers/wideworldimporters-etl-workflow.png)

O fluxo de trabalho começa com uma tarefa de expressão que determina o tempo de corte apropriado. O tempo de corte é o tempo atual menos alguns minutos. (Essa abordagem é mais robusta do que solicitar dados até o momento atual.) Qualquer milissegundos são truncados a partir do momento.

O processamento principal começa povoando a tabela de dimensões Data. O processamento garante que todas as datas do ano atual tenham sido preenchidas na tabela.

Em seguida, uma série de tarefas de fluxo de dados carrega cada dimensão. Então, eles carregam cada fato.

## <a name="prerequisites"></a>Pré-requisitos

- SQL Server 2016 (ou posterior), com os bancos de dados WideWorldImporters e WideWorldImportersDW (nas mesmas ou em diferentes instâncias do SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Certifique-se de criar um catálogo de Serviços de Integração. Para criar um catálogo de serviços de integração, no SQL Server Management Studio Object Explorer, clique com o botão direito do mouse **nos Serviços**de Integração e selecione **Adicionar catálogo**. Deixe as opções padrão. Você é solicitado a ativar o SQLCLR e fornecer uma senha.


## <a name="download"></a>Baixar

Para obter a versão mais recente da amostra, consulte [a liberação de importadores de todo](https://go.microsoft.com/fwlink/?LinkID=800630)o mundo . Baixe o arquivo de pacote *Daily ETL.ispac* Integration Services.

Para que o código-fonte recrie o banco de dados de amostras, consulte [importadores de todo o mundo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-ssis).

## <a name="install"></a>Instalar

1. Implantar o pacote serviços de integração:
   1. No Windows Explorer, abra o pacote *Daily ETL.ispac.* Isso lança o Assistente de Implantação de Serviços de Integração do Servidor SQL.
   2. Em **Select Source,** siga os padrões de implantação do projeto, com o caminho apontando para o pacote *Daily ETL.ispac.*
   3. Em **Select Destination,** digite o nome do servidor que hospeda o catálogo dos Serviços de Integração.
   4. Selecione um caminho no catálogo dos Serviços de Integração, por exemplo, em uma nova pasta chamada *WideWorldImporters*.
   5. Selecione **Implantar** para terminar o assistente.

2. Crie um trabalho de agente de servidor SQL para o processo ETL:
   1. No Management Studio, clique com o botão direito do mouse **no SQL Server Agent**e selecione **Novo** > **trabalho**.
   2. Digite um nome, por exemplo, *WideWorldImporters ETL*.
   3. Adicione uma etapa de **trabalho** do pacote de serviços de **integração do servidor SQL tipo .**
   4. Selecione o servidor que possui o catálogo de Serviços de Integração e selecione o pacote *ETL diário.*
   5. Em **Configuração** > **De Gerenciamentos de Conexão,** certifique-se de que as conexões à origem e ao destino estejam configuradas corretamente. O padrão é conectar-se à instância local.
   6. Selecione **OK** para criar o trabalho.

3. Executar ou agendar o trabalho.
