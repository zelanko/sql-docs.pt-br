---
title: WideWorldImportersDW - fluxo de trabalho ETL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a227848ac7f7fde500aa03a1ab206d19c11f3fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758714"
---
# <a name="wideworldimportersdw-etl-workflow"></a>Fluxo de trabalho ETL WideWorldImportersDW
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Use o *WWI_Integration* pacote ETL para migrar dados do banco de dados de WideWorldImporters para o banco de dados WideWorldImportersDW como alterações de dados. O pacote é executado periodicamente (normalmente, diariamente).

O pacote garante um alto desempenho usando o SQL Server Integration Services para coordenar operações em massa de T-SQL (em vez de transformações separadas no Integration Services).

As dimensões são carregadas primeiro e, em seguida, as tabelas de fatos são carregadas. O pacote pode ser executada sempre após uma falha.

O fluxo de trabalho tem esta aparência:

 ![Fluxo de trabalho ETL de WideWorldImporters](media/wide-world-importers/wideworldimporters-etl-workflow.png)

O fluxo de trabalho começa com uma tarefa de expressão que determina o tempo limite apropriado. O tempo limite é a hora atual menos alguns minutos. (Essa abordagem é mais robusta que solicitando dados diretamente para a hora atual). Qualquer milissegundos são truncados desde o momento.

Inicia o processamento principal, preenchendo a tabela de dimensões de data. O processamento garante que todas as datas do ano atual foram populadas na tabela.

Em seguida, uma série de tarefas de fluxo de dados carrega cada dimensão. Em seguida, ele carregam cada fato.

## <a name="prerequisites"></a>Prerequisites

- SQL Server 2016 (ou posterior), com WideWorldImporters e WideWorldImportersDW bancos de dados (na mesma ou em diferentes instâncias do SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Certifique-se de que você crie um catálogo do Integration Services. Para criar um catálogo do Integration Services, no Pesquisador de objetos do SQL Server Management Studio, clique com botão direito **Integration Services**e, em seguida, selecione **Adicionar catálogo**. Deixe as opções padrão. Você precisará habilitar o SQLCLR e forneça uma senha.


## <a name="download"></a>Download

Para obter a versão mais recente da amostra, consulte [todo o mundo-importadores versão](http://go.microsoft.com/fwlink/?LinkID=800630). Baixe o *ETL.ispac diária* arquivo de pacote do Integration Services.

Para o código-fonte recriar o banco de dados de exemplo, consulte [world-wide-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl).

## <a name="install"></a>Instalar

1. Implante o pacote do Integration Services:
   1. No Windows Explorer, abra o *ETL.ispac diária* pacote. Isso inicia o Assistente de implantação do SQL Server Integration Services.
   2. Sob **Selecionar origem**, siga os padrões para a implantação de projeto, com o caminho que aponta para o *ETL.ispac diária* pacote.
   3. Sob **Selecionar destino**, insira o nome do servidor que hospeda o catálogo do Integration Services.
   4. Selecione um caminho de catálogo do Integration Services, por exemplo, em uma nova pasta chamada *WideWorldImporters*.
   5. Selecione **Deploy** para concluir o assistente.

2. Crie um trabalho do SQL Server Agent para o processo ETL:
   1. No Management Studio, clique com botão direito **SQL Server Agent**e, em seguida, selecione **New** > **trabalho**.
   2. Insira um nome, por exemplo, *WideWorldImporters ETL*.
   3. Adicionar um **etapa de trabalho** do tipo **pacote do SQL Server Integration Services**.
   4. Selecione o servidor que tem o catálogo do Integration Services e, em seguida, selecione a *ETL diários* pacote.
   5. Sob **Configuration** > **gerenciadores de Conexão**, certifique-se de que as conexões com a origem e destino estão configuradas corretamente. O padrão é para se conectar à instância local.
   6. Selecione **Okey** para criar o trabalho.

3. Executar ou agendar o trabalho.
