---
title: "Lição 2: Adicionando um loop com o SSIS | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 683a2db5f7af5292051b5ce5c4cec9d49d465c2e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-2-adding-looping-with-ssis"></a>Lição 2: Adicionando um loop com o SSIS
Na [Lição 1: Criar um projeto e pacote básico com o SSIS](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md), você criou um pacote que extraiu dados de uma única fonte de arquivo simples, transformou os dados usando transformações Pesquisa e, por fim, carregou os dados na tabela de fatos **FactCurrency** do banco de dados de exemplo **AdventureWorksDW2012** .  
  
Porém, é raro para um processo de extração, transformação e carregamento (ETL) usar um único arquivo simples. Um típico processo ETL extrairia dados de várias fontes de arquivo simples. Extrair dados de várias fontes requer um fluxo de controle iterativo. Um dos recursos mais aguardados do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é a capacidade de adicionar iterações ou loops aos pacotes com facilidade.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece dois tipos de contêineres para efetuar loop por meio de pacotes: Foreach Loop e Loop For. O contêiner Foreach Loop usa um enumerador para executar o loop, enquanto que o contêiner For Loop geralmente usa uma expressão de variável. Esta lição usa o contêiner Loop Foreach.  
  
O contêiner Loop Foreach habilita um pacote a repetir o fluxo de controle para cada membro de um enumerador especificado. Com o contêiner Loop Foreach, você pode enumerar:  
  
-   Linhas do conjunto de registros ADO  
  
-   Informações de esquema do ADO .Net  
  
-   Estruturas de arquivo e diretório  
  
-   Variáveis de sistema, pacote e usuário  
  
-   Objetos enumeráveis contidos em uma variável  
  
-   Itens de uma coleção  
  
-   Nós em uma expressão XML Path Language (XPath)  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SMO (Management Objects)  
  
Nesta lição, você modificará o pacote ETL simples criado na lição 1 para aproveitar o contêiner Loop Foreach. Você também ajustará as variáveis do pacote definidas pelo usuário para habilitar o pacote do tutorial a ser iterado por todos os arquivos simples na pasta. Se você não tiver completado a lição anterior, também poderá copiar o pacote da Lição 1 terminada, que está incluído no tutorial.  
  
Nesta lição, você não modificará o fluxo de dados, apenas o fluxo de controle.  
  
> [!IMPORTANT]  
> Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar o **AdventureWorksDW2012**, consulte [Amostras de produto do Reporting Services no CodePlex](http://go.microsoft.com/fwlink/p/?LinkID=526910).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiando o pacote da Lição 1](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
-   [Etapa 2: adicionando e configurando o contêiner Loop Foreach](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [Etapa 3: Modificando o Gerenciador de Conexões de Arquivo Simples](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
-   [Etapa 4: Testando o pacote de tutorial da Lição 2](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
[Etapa 1: Copiando o pacote da Lição 1](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
## <a name="see-also"></a>Consulte Também  
[Contêiner Loop For](../integration-services/control-flow/for-loop-container.md)  
  
  
  
