---
title: Fluxo de trabalho WideWorldImportersDW-ETL | Microsoft Docs
description: Use o pacote ETL com SQL Server Integration Services (SSIS) para migrar dados periodicamente do banco de WideWorldImporters para o WideWorldImportersDW.
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487425"
---
# <a name="wideworldimportersdw-etl-workflow"></a>Fluxo de trabalho ETL WideWorldImportersDW
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Use o pacote ETL *WWI_Integration* para migrar dados do banco de dado WideWorldImporters para o banco de dados WideWorldImportersDW conforme as alterações de dado. O pacote é executado periodicamente (normalmente diariamente).

O pacote garante alto desempenho usando SQL Server Integration Services para orquestrar operações T-SQL em massa (em vez de transformações separadas em Integration Services).

As dimensões são carregadas primeiro e, em seguida, as tabelas de fatos são carregadas. Você pode executar novamente o pacote a qualquer momento após uma falha.

O fluxo de trabalho tem esta aparência:

 ![Fluxo de trabalho ETL WideWorldImporters](media/wide-world-importers/wideworldimporters-etl-workflow.png)

O fluxo de trabalho começa com uma tarefa de expressão que determina a hora de corte apropriada. A hora de corte é a hora atual menos alguns minutos. (Essa abordagem é mais robusta do que solicitar dados diretamente para a hora atual.) Todos os milissegundos são truncados a partir do momento.

O processamento principal começa preenchendo a tabela de dimensão de data. O processamento garante que todas as datas do ano atual tenham sido preenchidas na tabela.

Em seguida, uma série de tarefas de fluxo de dados carrega cada dimensão. Em seguida, eles carregam cada fato.

## <a name="prerequisites"></a>Pré-requisitos

- SQL Server 2016 (ou posterior), com os bancos de dados WideWorldImporters e WideWorldImportersDW (no mesmo ou em instâncias diferentes do SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Certifique-se de criar um catálogo Integration Services. Para criar um catálogo Integration Services, no Pesquisador de objetos do SQL Server Management Studio, clique com o botão direito do mouse em **Integration Services**e selecione **Adicionar Catálogo**. Deixe as opções padrão. Você será solicitado a habilitar o SQLCLR e a fornecer uma senha.


## <a name="download"></a>Baixar

Para obter a versão mais recente do exemplo, consulte [Wide-World-inporters – Release](https://go.microsoft.com/fwlink/?LinkID=800630). Baixe o arquivo de pacote de Integration Services do *ETL. Ispac diário* .

Para que o código-fonte recrie o banco de dados de exemplo, consulte [Wide-World-Importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-ssis).

## <a name="install"></a>Instalar

1. Implante o pacote de Integration Services:
   1. No Windows Explorer, abra o pacote *ETL. Ispac diário* . Isso inicia o assistente de implantação SQL Server Integration Services.
   2. Em **selecionar origem**, siga os padrões para implantação de projeto, com o caminho apontando para o pacote *ETL. ispac diário* .
   3. Em **Selecionar destino**, insira o nome do servidor que hospeda o catálogo de Integration Services.
   4. Selecione um caminho no catálogo de Integration Services, por exemplo, em uma nova pasta chamada *WideWorldImporters*.
   5. Selecione **implantar** para concluir o assistente.

2. Crie um trabalho de SQL Server Agent para o processo de ETL:
   1. Em Management Studio, clique com o botão direito do mouse em **SQL Server Agent**e selecione **novo** > **trabalho**.
   2. Insira um nome, por exemplo, *WIDEWORLDIMPORTERS ETL*.
   3. Adicione uma **etapa de trabalho** do tipo **SQL Server Integration Services pacote**.
   4. Selecione o servidor que tem o catálogo Integration Services e, em seguida, selecione o pacote de *ETL diário* .
   5. Em **Configuration** > **gerenciadores de conexões**de configuração, verifique se as conexões com a origem e o destino estão configuradas corretamente. O padrão é conectar-se à instância local.
   6. Selecione **OK** para criar o trabalho.

3. Execute ou agende o trabalho.
