---
title: Adicionar conhecimento a uma base de dados de conhecimento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: da148a7f-55bc-4990-a157-e61968b831d7
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c9122db448e95a6734ea3cf3c1010665b60f4650
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65481181"
---
# <a name="adding-knowledge-to-a-knowledge-base"></a>Adicionando conhecimento a uma base de dados de conhecimento
  Este tópico descreve as maneiras pelas quais você pode adicionar um conhecimento a uma base de dados de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Antes de executar operações de qualidade de dados, você tem que ter conhecimento sobre os dados. Para adquirir esse conhecimento, crie e mantenha uma base de dados de conhecimento de qualidade de dados e adicione a ela conhecimentos relacionados a um tipo específico de fonte de dados. A base de dados de conhecimento é um repositório de conhecimento sobre seus dados que permitem que você entenda seus dados e mantenha sua integridade.  
  
 A base de dados de conhecimento contém domínios de dados relacionados à fonte de dados. Para cada domínio, o DQKB armazena todos os termos identificados, erros de ortografia, regras de validação e de negócio e dados de referência que podem ser usados para executar ações de qualidade de dados na fonte de dados. O DQS usa esse conhecimento para identificar dados incorretos ou inválidos ou executar correspondência.  
  
 Você pode adicionar conhecimento a uma base de dados de conhecimento usando as formas auxiliadas por computador ou interativas a seguir.  
  
-   [Executar a descoberta da base de dados de conhecimento](#Discovery)  
  
-   [Gerenciar valores de dados em um domínio](#ManageDomain)  
  
-   [Importar conhecimento de um arquivo. DQS](#DQSFile)  
  
-   [Importar conhecimento de um arquivo do Excel](#Excel)  
  
-   [Importar conhecimento de um projeto de volta para a base de dados de conhecimento](#Project)  
  
-   [Usar a base de dados de conhecimento do DQS padrão](#Default)  
  
##  <a name="Discovery"></a>Executar descoberta da base de dados de conhecimento  
 A descoberta da base de dados de conhecimento analisa uma amostra de dados para os critérios de qualidade de dados e adiciona o conhecimento obtido à base de dados de conhecimento. Esse é um processo auxiliado por computador que identifica as inconsistências de dados e os erros de sintaxe e propõe alterações nos dados. A atividade de descoberta da base de dados de conhecimento é um assistente que inclui uma página em que você pode gerenciar interativamente valores de domínio.  
  
-   Para obter mais informações na documentação, consulte [Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md).  
  
-   Para obter um vídeo que demonstra como executar a descoberta da base de dados de conhecimento, clique em [here](https://msdn.microsoft.com/sqlserver/hh323825.aspx).  
  
##  <a name="ManageDomain"></a>Gerenciar valores de dados em um domínio  
 O DQS permite que você altere e aumente interativamente os metadados que são gerados pela atividade de descoberta da base de dados de conhecimento assistida por computador. Faça isso na atividade Gerenciamento de Domínio, onde é possível aplicar uma alteração a um valor de dados específico.  
  
-   Para obter mais informações na documentação, consulte [Change Domain Values](../../2014/data-quality-services/change-domain-values.md).  
  
-   Para obter um vídeo que demonstra como executar o gerenciamento de domínio, clique [aqui](https://msdn.microsoft.com/sqlserver/hh323825.aspx). Observe que, nesse vídeo, você pode alterar os valores de domínio na página Gerenciando Valores de Domínio do assistente de Descoberta da Base de Dados de Conhecimento. Também é possível executar essas etapas na página Valores de Domínio da atividade Gerenciamento de Domínio.  
  
##  <a name="DQSFile"></a>Importar conhecimento de um arquivo. DQS  
 Você pode importar um domínio de um arquivo de dados .dqs para uma base de dados de conhecimento existente ou pode importar uma base de dados de conhecimento completa de um .dqs para uma nova base de dados de conhecimento. Para fazer isso, primeiro você precisa exportar um domínio ou base de dados de conhecimento existente para um arquivo .dqs. Um arquivo .dqs que contém um domínio inclui todos os dados de domínio, um arquivo .dqs que contém uma base de dados de conhecimento conterá todo as informações de base de dados de conhecimento, inclusive domínios e a política de correspondência.  
  
-   Para obter mais informações na documentação, consulte [Importar um domínio de um arquivo .dqs](../../2014/data-quality-services/import-a-domain-from-a-dqs-file.md) ou [Importar uma base de dados de conhecimento de um arquivo .dqs](../../2014/data-quality-services/import-a-knowledge-base-from-a-dqs-file.md).  
  
##  <a name="Excel"></a>Importar conhecimento de um arquivo do Excel  
 Você pode importar valores de domínio de um arquivo de planilha do Excel para um domínio ou uma base de dados de conhecimento existente. Para fazer isso, primeiro você deve criar uma planilha do Excel com os valores de domínio que deseja importar e assegurar que o Excel esteja instalado no computador [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para poder importar valores usando o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Não é possível exportar valores de domínio de um domínio ou uma base de dados de conhecimento para um arquivo do Excel.  
  
-   Para obter mais informações na documentação, consulte [Importar valores de um arquivo do Excel para um domínio](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md) ou [Importar domínios de um arquivo do Excel para a descoberta de conhecimento](../../2014/data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md).  
  
##  <a name="Project"></a>Importar conhecimento de um projeto de volta para a base de dados de conhecimento  
 Depois que você criar um projeto de limpeza ou de qualidade de dados de correspondência usando uma base de dados de conhecimento, poderá importar o conhecimento criado durante a limpeza ou correspondência para essa base de dados de conhecimento. Isso permite a você manter o conhecimento gerado durante o projeto e criar continuamente o conhecimento na base de dados de conhecimento.  
  
-   Para obter mais informações na documentação, consulte [Importar valores do projeto de limpeza para um domínio](../../2014/data-quality-services/import-cleansing-project-values-into-a-domain.md).  
  
##  <a name="Default"></a>Usar a base de dados de conhecimento do DQS padrão  
 O DQS é fornecido com uma base de dados de conhecimento predefinida denominada Dados do DQS que contém domínios para empresas nos Estados Unidos e dados de endereço. Essa base de conhecimento pode ser usada para iniciar um projeto rapidamente sem criar uma nova base de conhecimento. A base de dados de conhecimento Dados do DQS é somente leitura, mas o administrador de dados pode criar uma nova base de conhecimento baseado nela.  
  
-   Para obter mais informações na documentação, consulte [Using the DQS Default Knowledge Base](../../2014/data-quality-services/using-the-dqs-default-knowledge-base.md).  
  
  
