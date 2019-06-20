---
title: 'Lição 1: Criando o projeto e pacote básico | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 652cf44f70e890b3203ed27890d06f98d70b7f1d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767498"
---
# <a name="lesson-1-creating-the-project-and-basic-package"></a>Lição 1: Como criar o projeto e o pacote básico
  Nessa lição, você criará um pacote ETL simples que extrai dados de uma fonte exclusiva de arquivo simples, transforma os dados usando dois componentes de transformação pesquisa e grava esses dados na tabela de fatos **FactCurrency** no **AdventureWorksDW2012**. Como parte dessa lição, você irá aprender como criar novos pacotes, adicionar e configurar fonte de dados, e conexões de destino, e trabalhar com novos fluxos de controle e componentes de fluxo.  
  
> [!IMPORTANT]  
>  Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar **AdventureWorksDW2012**, consulte [amostras de produto do Microsoft SQL Server: Reporting Services](https://archive.codeplex.com/?p=msftrsprodsamples).  
  
## <a name="understanding-the-package-requirements"></a>Compreendendo os requisitos de pacote  
 Este tutorial requer o Microsoft SQL Server Data Tools.  
  
 Para obter mais informações sobre como instalar o SQL Server Data Tools, consulte [Download do SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017).  
  
 Antes de criar um pacote, você precisa ter um bom conhecimento da formatação usada tanto na fonte de dados quanto no destino. Depois de entender estes dois formatos de dados, você estará pronto para definir as transformações necessárias para mapear a fonte de dados ao destino.  
  
### <a name="looking-at-the-source"></a>Olhando para a Fonte  
 Nesse tutorial, os dados de origem são um conjunto de dados de moeda corrente históricos contidos no arquivo simples, SampleCurrencyData.txt. A fonte de dados tem as seguintes quatro colunas: a taxa média de moeda, uma chave de moeda, uma chave de data e a taxa de final do dia.  
  
 Aqui está um exemplo dos dados de origem contidos no arquivo SampleCurrencyData.txt:  
  
 `1.00070049USD9/3/05 0:001.001201442`  
  
 `1.00020004USD9/4/05 0:001`  
  
 `1.00020004USD9/5/05 0:001.001201442`  
  
 `1.00020004USD9/6/05 0:001`  
  
 `1.00020004USD9/7/05 0:001.00070049`  
  
 `1.00070049USD9/8/05 0:000.99980004`  
  
 `1.00070049USD9/9/05 0:001.001502253`  
  
 `1.00070049USD9/10/05 0:000.99990001`  
  
 `1.00020004USD9/11/05 0:001.001101211`  
  
 `1.00020004USD9/12/05 0:000.99970009`  
  
 Quando estiver trabalhando com dados de fonte de arquivo simples, é importante entender como o gerenciador de conexões de Arquivo Simples interpreta os dados de arquivo simples. Se a fonte do arquivo simples for Unicode, o gerenciador de conexões de Arquivo Simples definirá todas as colunas como [DT_WSTR] com uma largura padrão de coluna de 50. Se a fonte de arquivo simples for codificada por ANSI, as colunas estarão definidas como [DT_STR] com uma largura de coluna de 50. Você provavelmente terá que alterar esses padrões para tornar os tipos de coluna de cadeia de caracteres mais apropriados para seus dados. Para fazer isso, você precisará olhar o tipo de dados do destino onde os dados serão gravados, e, então, escolher o tipo correto dentro do gerenciador de conexões de Arquivo Simples.  
  
### <a name="looking-at-the-destination"></a>Olhando o destino  
 O destino final dos dados de origem é a tabela de fatos **FactCurrency** no **AdventureWorksDW**. A tabela de fatos **FactCurrency** tem quatro colunas e relacionamentos com duas tabelas de dimensões, como mostrado na tabela a seguir.  
  
|Nome da coluna|Tipo de dados|Tabela de pesquisa|Coluna de Pesquisa|  
|-----------------|---------------|------------------|-------------------|  
|AverageRate|float|None|None|  
|CurrencyKey|int (FK)|DimCurrency|CurrencyKey (PK)|  
|DateKey|int (FK)|DimDate|DateKey (PK)|  
|EndOfDayRate|float|None|None|  
  
### <a name="mapping-source-data-to-be-compatible-with-the-destination"></a>Mapeando fontes de dados compatíveis com o destino  
 Uma análise dos formatos de dados de origem e destino indicam que as pesquisas serão necessárias para os valores **CurrencyKey** e **DateKey** . As transformações que executarão essas pesquisas obterão os valores **CurrencyKey** e **DateKey** usando as chaves alternativas das tabelas de dimensões **DimCurrency** e **DimDate** .  
  
|Coluna de Arquivos Simples|Nome da tabela|Nome da coluna|Tipo de Dados|  
|----------------------|----------------|-----------------|---------------|  
|0|FactCurrency|AverageRate|float|  
|1|DimCurrency|CurrencyAlternateKey|nchar (3)|  
|2|DimDate|FullDateAlternateKey|date|  
|3|FactCurrency|EndOfDayRate|float|  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Criando um novo projeto do Integration Services](lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [Etapa 2: Adicionando e configurando um gerenciador de conexões de arquivo simples](lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [Etapa 3: Adicionando e configurando um Gerenciador de Conexão do OLE DB](lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [Etapa 4: Adicionando uma tarefa de fluxo de dados ao pacote](lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [Etapa 5: Adicionando e configurando a fonte de arquivo simples](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [Etapa 6: Adicionando e configurando a transformação pesquisa](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [Etapa 7: Adicionando e configurando o destino OLE DB](lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [Etapa 8: Tornando o pacote da lição 1 mais fácil de entender](lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [Etapa 9: Testando o pacote de Tutorial da lição 1](lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
 [Etapa 1: Criando um novo projeto do Integration Services](lesson-1-1-creating-a-new-integration-services-project.md)  
  
  
