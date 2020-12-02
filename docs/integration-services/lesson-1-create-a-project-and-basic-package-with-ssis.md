---
description: 'Lição 1: Criar um projeto e pacote básico com o SSIS'
title: 'Lição 1: Criar um projeto e pacote básico com o SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 428295430a2abb50738742db088b9573a7bf35a6
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88461982"
---
# <a name="lesson-1-create-a-project-and-basic-package-with-ssis"></a>Lição 1: Criar um projeto e pacote básico com o SSIS

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Nessa lição, você cria um pacote ETL simples que extrai dados de uma fonte única de arquivo simples, transforma os dados usando duas transformações de pesquisa e grava os dados transformados em uma cópia da tabela de fatos **FactCurrencyRate** no banco de dados de exemplo **AdventureWorksDW2012**. Como parte dessa lição, você aprende a criar novos pacotes, adicionar e configurar conexões de destino e de fonte de dados e trabalhar com novos fluxos de controle e componentes de fluxo.  
  
Antes de criar um pacote, você precisa ter um bom conhecimento da formatação usada nos dados de origem e de destino. Em seguida, você estar pronto para definir as transformações necessárias para mapear os dados de origem para o destino.  

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial se baseia no Microsoft SQL Server Data Tools, um conjunto de pacotes de exemplo e um banco de dados de exemplo.

* Para instalar SQL Server Data Tools, confira [Baixar SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md).  
  
* Para baixar todos os pacotes de lição para este tutorial:

    1.  Navegue até [Arquivos do tutorial do Integration Services](https://www.microsoft.com/download/details.aspx?id=56827).

    2.  Selecione o botão **DOWNLOAD**.

    3.  Selecione o arquivo **Creating a Simple ETL Package.zip** e, em seguida, selecione **Avançar**.

    4.  Depois que o arquivo for baixado, descompacte o conteúdo para um diretório local.  

* Para instalar e implantar o banco de dados de exemplo **AdventureWorksDW2012**, confira [Instalar e configurar o banco de dados de exemplo AdventureWorks – SQL](../samples/adventureworks-install-configure.md).
  
## <a name="look-at-the-source-data"></a>Examinar os dados de origem
Nesse tutorial, os dados de origem são um conjunto de dados de moeda corrente históricos em arquivo simples chamado **SampleCurrencyData.txt**. A fonte de dados tem as seguintes quatro colunas: a taxa média de moeda, uma chave de moeda, uma chave de data e a taxa de final do dia.  
  
Aqui está um exemplo dos dados de origem no arquivo SampleCurrencyData.txt:  
  
```
1.00070049USD9/3/05 0:001.001201442  
1.00020004USD9/4/05 0:001  
1.00020004USD9/5/05 0:001.001201442  
1.00020004USD9/6/05 0:001  
1.00020004USD9/7/05 0:001.00070049  
1.00070049USD9/8/05 0:000.99980004  
1.00070049USD9/9/05 0:001.001502253  
1.00070049USD9/10/05 0:000.99990001  
1.00020004USD9/11/05 0:001.001101211  
1.00020004USD9/12/05 0:000.99970009
```
  
Quando estiver trabalhando com os dados de origem de arquivo simples, é importante entender como o gerenciador de conexões de Arquivo Simples interpreta os dados de arquivo simples. Se a fonte do arquivo simples for Unicode, o gerenciador de conexões de Arquivo Simples definirá todas as colunas como [DT_WSTR] com uma largura padrão de coluna de 50. Se a fonte de arquivo simples for codificada por ANSI, as colunas estarão definidas como [DT_STR] com uma largura de coluna padrão de 50. Você provavelmente precisará alterar esses padrões para tornar os tipos de coluna de cadeia de caracteres mais aplicáveis para seus dados. Você precisará examinar o tipo de dados de destino e, em seguida, escolher o tipo dentro do Gerenciador de conexão de Arquivo Simples.  
  
## <a name="look-at-the-destination-data"></a>Examinar os dados de destino
O destino dos dados de origem é uma cópia da tabela de fatos **FactCurrencyRate** no **AdventureWorksDW**. A tabela de fatos **FactCurrencyRate** tem quatro colunas e tem relações com duas tabelas dimensionais, como mostrado na tabela a seguir.  
  
|Nome da coluna|Tipo de Dados|Tabela de pesquisa|coluna de pesquisa|  
|---------------|-------------|----------------|-----------------|  
|AverageRate|FLOAT|Nenhum|Nenhum|  
|CurrencyKey|int (FK)|DimCurrency|CurrencyKey (PK)|  
|DateKey|int (FK)|DimDate|DateKey (PK)|  
|EndOfDayRate|FLOAT|Nenhum|Nenhum|  
  
## <a name="map-the-source-data-to-the-destination"></a>Mapear os dados de origem para o destino  
Nossa análise dos formatos de dados de origem e destino indicam que as pesquisas são necessárias para os valores **CurrencyKey** e **DateKey**. As transformações que executam essas pesquisas obtêm esses valores usando as chaves alternativas das tabelas de dimensões **DimCurrency** e **DimDate**.  
  
|Coluna de arquivo simples|Nome da tabela|Nome da coluna|Tipo de Dados|  
|--------------------|--------------|---------------|-------------|  
|0|FactCurrencyRate|AverageRate|FLOAT|  
|1|DimCurrency|CurrencyAlternateKey|nchar (3)|  
|2|DimDate|FullDateAlternateKey|date|  
|3|FactCurrencyRate|EndOfDayRate|FLOAT|  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: criar um projeto do Integration Services](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [Etapa 2: Adicionar e configurar um gerenciador de conexões de Arquivo Simples](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [Etapa 3: Adicionar e configurar um gerenciador de conexões OLE DB](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [Etapa 4: Adicionar uma tarefa de Fluxo de Dados ao pacote](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [Etapa 5: Adicionar e configurar a fonte de arquivo simples](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [Etapa 6: Adicionar e configurar as transformações de pesquisa](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [Etapa 7: Adicionar e configurar o destino OLE DB](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [Etapa 8: Anotar e formatar o pacote da Lição 1](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [Etapa 9: Testar o pacote da Lição 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
[Etapa 1: Criar um projeto do Integration Services](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
