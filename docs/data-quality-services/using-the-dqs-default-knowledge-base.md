---
title: "Usando a base de dados de conhecimento padr&#227;o do DQS | Microsoft Docs"
ms.custom: ""
ms.date: "07/31/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# Usando a base de dados de conhecimento padr&#227;o do DQS
  Este tópico descreve a base de dados de Conhecimento padrão, **dados do DQS**, que é instalada com [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Esta é uma base de conhecimento padrão pré-criada que contém os seguintes domínios:  
  
-   **País/região**: contém convencionais longos (nome oficial conforme designado pelo país/região) e nomes curtos (nome comum usado em listas, mapas, etc.), abreviação de duas letras, abreviação de três letras e código de três dígitos para cada local.  O valor principal é definido como o nome longo do país.  
  
-   **País/região (prefixo de três letras)**: contém convencionais longos (nome oficial conforme designado pelo país/região) e nomes curtos (nome comum usado em listas, mapas e assim por diante), abreviação de duas letras, abreviação de três letras e código de três dígitos para cada local.  Os valores principais são definidos como uma abreviação de três letras do Município.  
  
-   **País/região (prefixo de duas letras)**: contém convencionais longos (nome oficial conforme designado pelo país/região) e nomes curtos (nome comum usado em listas, mapas, etc.), abreviação de duas letras, abreviação de três letras e código de três dígitos para cada local.  O valor principal é definido como uma abreviação de duas letras do País.  
  
-   **EUA - municípios**: contém uma lista de regiões dos EUA.  
  
-   **EUA - Sobrenome**: contém uma lista de sobrenomes (sobrenomes) que ocorrem 100 ou mais vezes no censo 2000.  
  
-   **EUA - locais**: contém uma lista de locais para os 50 estados, o Distrito de Columbia e Porto Rico extraídos do censo 2010.  
  
-   **EUA - estado**: contém o convencional longo (oficial) nome e a abreviação de duas letras para cada estado nos EUA. O valor principal é definido como o nome convencional do estado.  
  
-   **EUA-estado (título com 2 letras)**: contém o convencional longo (oficial) nome e a abreviação de duas letras para cada estado nos EUA. O valor principal é definido como um nome de estado com abreviação de duas letras.  
  
## Usando a base de dados de conhecimento padrão  
 Você pode usar a base de dados de conhecimento padrão do DQS, os Dados do DQS, das seguintes formas:  
  
-   Inicie e execute rapidamente um projeto de qualidade de dados de limpeza usando a base de dados de conhecimento padrão sem ter que primeiro criar uma nova base de dados de conhecimento em DQS.  
  
-   Execute o Gerenciamento de Domínio, a Descoberta de Conhecimento ou as atividades de Política de Correspondência na base de dados de conhecimento padrão. Para fazer isso, clique em **Abrir Base de Dados de Conhecimento** na [Data Quality Client Home Screen](../data-quality-services/data-quality-client-home-screen.md), selecione a base de dados de conhecimento **Dados do DQS** na tela **Abrir Base de Dados de Conhecimento** e, em seguida, selecione a atividade na área **Selecionar Atividade** . Clique em **Avançar** para continuar.  
  
-   Crie uma nova base de dados de conhecimento usando a base de dados de conhecimento padrão. Para criar uma base de dados de conhecimento de uma base de conhecimento existente, consulte [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md).  
  
-   Usá-lo no [componente de limpeza do DQS no Integration Services](http://go.microsoft.com/fwlink/?LinkId=238830) e [o suplemento Master Data Services para Excel](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md).  
  
## Consulte também  
 [Bases de Dados de Conhecimento DQS e domínios](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  