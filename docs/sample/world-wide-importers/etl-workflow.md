---
title: Fluxo de trabalho ETL | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 06/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 679e58fe-b062-4934-a94c-9bb916b0bcb0
caps.latest.revision: 5
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 85898dfc3a12ee195910bf965f0099b35f95b239
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="wideworldimportersdw-etl-workflow"></a>Fluxo de trabalho WideWorldImportersDW ETL
O pacote ETL WWI_Integration é usado para migrar dados do banco de dados de WideWorldImporters para o banco de dados WideWorldImportersDW como as alterações de dados. O pacote é executado periodicamente (geralmente diariamente).

## <a name="overview"></a>Visão geral

O design dos usos de pacote SQL Server Integration Services (SSIS) coordenar operações em massa T-SQL (em vez de como transformações separadas no SSIS) para garantir o alto desempenho.

Dimensões são carregadas em primeiro lugar, seguidas por tabelas de fatos. O pacote pode ser executado novamente a qualquer momento após uma falha.

O fluxo de trabalho é o seguinte:

 ![Fluxo de trabalho de WideWorldImporters ETL](../../sample/world-wide-importers/media/wideworldimporters-etl-workflow.png)

Ele começa com uma tarefa de expressão funciona o tempo limite apropriado. Essa hora é a hora atual menos alguns minutos. (Isso é mais robusto que solicitando dados diretamente para a hora atual). Em seguida, truncará qualquer milissegundos desde o momento.

Inicia o processamento principal popular a tabela de dimensões de data. Isso garante que todas as datas do ano atual foram populadas na tabela.

Depois disso, uma série de tarefas de fluxo de dados carrega cada dimensão e, em seguida, cada fato.

## <a name="prerequisites"></a>Pré-requisitos

- SQL Server 2016 (ou superior) com os bancos de dados WideWorldImporters e WideWorldImportersDW. Eles podem ser em iguais ou diferentes instâncias do SQL Server.
- SQL Server Management Studio (SSMS)
- SQL Server 2016 Integration Services (SSIS).
  - Certifique-se de que ter criado um catálogo do SSIS. Se não estiver, clique com botão direito **Integration Services** no Pesquisador de objetos do SSMS e escolha **Adicionar catálogo**. Siga os padrões. Solicitará que você habilitar sqlclr e forneça uma senha.


## <a name="download"></a>Download

A versão mais recente do exemplo:

[todo-world importers versão](http://go.microsoft.com/fwlink/?LinkID=800630)

Baixe o arquivo de pacote SSIS **ETL.ispac diário**.

Código-fonte para recriar o banco de dados de exemplo está disponível no seguinte local.

[world-wide-importadores](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)

## <a name="install"></a>Instalar

1. Implante o pacote do SSIS.
   - Abra o pacote de "Diário ETL.ispac" do Windows Explorer. Isso iniciará o Assistente de implantação do Integration Services.
   - Em "Selecionar origem" seguir o padrão de implantação de projeto, com o caminho que aponta para o pacote de "Diário ETL.ispac".
   - Em "Selecionar destino" Insira o nome do servidor que hospeda o catálogo do SSIS.
   - Selecione um caminho de catálogo do SSIS, por exemplo, em uma nova pasta "WideWorldImporters".
   - Finalize o assistente, clique em implantar.

2. Crie um trabalho do SQL Server Agent para o processo ETL.
   - No SSMS, clique com botão direito "SQL Server Agent" e selecione Novo -> trabalho.
   - Selecione um nome, por exemplo "WideWorldImporters ETL".
   - Adicione uma etapa de trabalho do tipo "Pacote de serviços de integração do SQL Server".
   - Selecione o servidor com o catálogo do SSIS e selecione o pacote de "Diário ETL".
   - Em Configuração -> gerenciadores de Conexão, verifique se as conexões de origem e destino estão configuradas corretamente. O padrão é conectar-se à instância local.
   - Clique em Okey para criar o trabalho.

3. Executar ou agendar o trabalho.

