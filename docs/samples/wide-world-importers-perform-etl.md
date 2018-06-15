---
title: WideWorldImportersDW - fluxo de trabalho ETL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 36638c4cc2bda58ac277822d5c4a4ce5421ab8b4
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467682"
---
# <a name="wideworldimportersdw-etl-workflow"></a>Fluxo de trabalho WideWorldImportersDW ETL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Use o *WWI_Integration* pacote ETL para migrar dados do banco de dados de WideWorldImporters para o banco de dados WideWorldImportersDW como alterações de dados. O pacote é executado periodicamente (normalmente diariamente).

O pacote garante um alto desempenho usando o SQL Server Integration Services coordenar operações em massa T-SQL (em vez de transformações separadas no Integration Services).

Dimensões são carregadas primeiro e, em seguida, as tabelas de fatos são carregadas. O pacote pode ser executada depois de uma falha.

O fluxo de trabalho tem esta aparência:

 ![Fluxo de trabalho de WideWorldImporters ETL](media/wide-world-importers/wideworldimporters-etl-workflow.png)

O fluxo de trabalho começa com uma tarefa de expressão que determina o tempo limite apropriado. O tempo limite é a hora atual menos de alguns minutos. (Essa abordagem é mais robusta que solicitando dados diretamente para a hora atual). Qualquer milésimos de segundo são truncados da hora.

Inicia o processamento principal popular a tabela de dimensões de data. O processamento garante que todas as datas do ano atual foram populadas na tabela.

Em seguida, uma série de tarefas de fluxo de dados carrega cada dimensão. Em seguida, ele carregam cada fato.

## <a name="prerequisites"></a>Prerequisites

- SQL Server 2016 (ou posterior), com WideWorldImporters e WideWorldImportersDW bancos de dados (na mesma ou em diferentes instâncias do SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Certifique-se de que você cria um catálogo do Integration Services. Para criar um catálogo do Integration Services, no Pesquisador de objetos do SQL Server Management Studio, clique com botão direito **Integration Services**e, em seguida, selecione **Adicionar catálogo**. Deixe as opções padrão. Você precisará habilitar SQLCLR e forneça uma senha.


## <a name="download"></a>Download

Para obter a versão mais recente da amostra, consulte [wide-world importers versão](http://go.microsoft.com/fwlink/?LinkID=800630). Baixe o *ETL.ispac diário* arquivo de pacote do Integration Services.

Para o código-fonte recriar o banco de dados de exemplo, consulte [world-wide-importadores](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl).

## <a name="install"></a>Instalar

1. Implante o pacote do Integration Services:
   1. No Windows Explorer, abra o *ETL.ispac diário* pacote. Isso inicia o Assistente de implantação do SQL Server Integration Services.
   2. Em **Selecionar origem**, siga os padrões para implantação de projeto, com o caminho que aponta para o *ETL.ispac diário* pacote.
   3. Em **Selecionar destino**, digite o nome do servidor que hospeda o catálogo do Integration Services.
   4. Selecione um caminho de catálogo do Integration Services, por exemplo, em uma nova pasta chamada *WideWorldImporters*.
   5. Selecione **implantar** para concluir o assistente.

2. Crie um trabalho do SQL Server Agent para o processo ETL:
   1. No Management Studio, clique com botão direito **do SQL Server Agent**e, em seguida, selecione **novo** > **trabalho**.
   2. Insira um nome, por exemplo, *WideWorldImporters ETL*.
   3. Adicionar um **etapa de trabalho** do tipo **pacote do SQL Server Integration Services**.
   4. Selecione o servidor que tem o catálogo do Integration Services e, em seguida, selecione o *de ETL* pacote.
   5. Em **configuração** > **gerenciadores de Conexão**, certifique-se de que as conexões de origem e destino estão configuradas corretamente. O padrão é conectar-se à instância local.
   6. Selecione **Okey** para criar o trabalho.

3. Executar ou agendar o trabalho.
