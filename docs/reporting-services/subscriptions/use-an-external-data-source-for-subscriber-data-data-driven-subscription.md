---
title: "Usar uma fonte de dados externa para obter dados de assinante (assinatura controlada por dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "fontes de dados do assinante [Reporting Services]"
  - "assinaturas [Reporting Services], fontes de dados externas"
  - "assinatura com base em consultas [Reporting Services]"
  - "fontes de dados externas [Reporting Services]"
  - "assinaturas controladas por dados"
  - "fontes de dados [Reporting Services], assinaturas"
ms.assetid: 1cade8ec-729c-4df8-a428-e75c9ad86369
caps.latest.revision: 43
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 43
---
# Usar uma fonte de dados externa para obter dados de assinante (assinatura controlada por dados)
  Em uma assinatura controlada por dados, os dados de assinatura dinâmicos são fornecidos por uma consulta ou um comando que recupera dados de uma fonte de dados externa. Os dados de assinatura podem ser recuperados de qualquer fonte de dados com suporte que satisfaça os requisitos para o processamento de assinaturas controladas por dados. A sintaxe da consulta ou do comando deve ser válida para uma extensão de processamento de dados instalada com seu servidor de relatório.  
  
## Requisitos de processamento de dados  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa extensões de processamento de dados para recuperar dados de assinatura. Os tipos de fonte de dados recomendados incluem o seguinte:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados relacionais  
  
-   Bancos de dados Oracle  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fontes de dados multidimensionais e de mineração de dados  
  
-   Fontes de dados XML  
  
     Ao usar a extensão de processamento de dados XML para os dados de assinante, aumente as configurações de tempo limite de consulta na assinatura. A extensão de processamento de dados XML usa milissegundos em vez de segundos para os valores de tempo limite de consulta. Se você não aumentar o valor de tempo limite, a assinatura poderá falhar devido a um tempo de processamento insuficiente.  
  
     Evite usar a opção **Não são necessárias credenciais** ao configurar a conexão com a fonte de dados de assinante. As credenciais armazenadas são recomendadas ao usar a extensão de processamento de dados XML para recuperar dados de assinatura em tempo de execução.  
  
 Outros tipos de fontes de dados com suporte podem ser usados, embora não haja garantia de que funcionem. Por exemplo, os tipos de fonte de dados a seguir não podem ser usados para obter dados de assinante:  
  
-   Bancos de dados SAP Netweaver BI  
  
-   modelos de relatório  
  
 Se você tiver uma extensão de processamento de dados personalizada que deseja usar nas assinaturas controladas por dados, implemente as interfaces <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> e <xref:Microsoft.ReportingServices.DataProcessing.IDataReader>. A extensão de processamento de dados deve oferecer suporte para execuções de consulta somente de esquema. Essa consulta é usada para recuperar metadados de coluna em tempo de design, para que os usuários possam mapear colunas para opções de entrega e parâmetros de relatório na definição de assinatura. A execução de consulta somente de esquema ocorre em uma fase inicial, quando o usuário está definindo a assinatura.  
  
## Requisitos de consulta  
 Ao criar uma consulta que recupera dados de assinatura, considere o seguinte:  
  
-   Você pode criar só uma consulta para a assinatura.  
  
-   A consulta deve retornar todos os valores que você deseja usar para opções de entrega e para especificar parâmetros de relatório.  
  
-   O servidor de relatório criará uma entrega de relatório para cada linha do conjunto de resultados. Se o conjunto de resultados for composto por trezentas linhas, o servidor de relatório tentará enviar trezentos relatórios.  
  
## Definindo opções de entrega com dados variáveis de um banco de dados de assinantes  
 Você pode usar dados no banco de dados de assinantes para personalizar opções de entrega para cada destinatário. O tipo de extensão de entrega usado determina quais opções estão disponíveis. Se você estiver usando a extensão de entrega de emails do servidor de relatórios, a consulta deve conter um alias de email para cada assinante. Se a entrega de compartilhamento de arquivos estiver sendo usada, os dados do assinante devem incluir valores que podem ser usados para criar arquivos de relatório específicos do assinante ou para fornecer um destino para a entrega. Para obter mais informações, consulte [Entrega de email no Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
## Transmitindo valores de parâmetro do banco de dados de assinantes para o relatório  
 Se estiver criando uma assinatura controlada por dados para um relatório parametrizado, use valores de parâmetro variáveis para personalizar a saída de cada relatório. Por exemplo, o banco de dados de assinantes pode conter números de identificação de funcionários, datas de contratação, cargos e informações sobre a localização de escritórios que podem ser usados para filtrar dados de relatório. Se o relatório aceitar os parâmetros baseados nesses dados ou em outros dados de coluna disponíveis, você pode mapear o parâmetro para a coluna adequada.  
  
 Ao mapear campos de assinante para parâmetros de relatório, verifique se os tipos de dados e os comprimentos de coluna são compatíveis. Se houver uma desigualdade de tipo de dados, um erro ocorrerá durante o processamento da assinatura. Para saber mais sobre como usar dados de assinante em um relatório com parâmetros, consulte [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md).  
  
## Modificando a fonte de dados de assinante  
 As modificações a seguir feitas na fonte de dados de assinante podem impedir a execução da assinatura:  
  
-   Remoção de colunas mencionadas na assinatura.  
  
-   Modificação da estrutura de tabela da fonte de dados.  
  
-   Alteração do tipo de dados e de outras propriedades de coluna.  
  
 Se fizer alguma dessas alterações, você deverá atualizar a assinatura.  
  
## Consulte também  
 [Criar, modificar e excluir assinaturas controladas por dados](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [Assinaturas controladas por dados](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
  