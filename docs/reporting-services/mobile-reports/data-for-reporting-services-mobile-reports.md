---
title: "Dados para relat&#243;rios m&#243;veis do Reporting Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 91138ef8-ddb4-4ac5-a1e4-fa4cf1c58dcc
caps.latest.revision: 15
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 15
---
# Dados para relat&#243;rios m&#243;veis do Reporting Services
O modelo de dados do [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] é simples. Os dados são importados para o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] como uma coleção de conjuntos de dados. Relacionamentos formais entre conjuntos de dados não são necessários. As pesquisas de um conjunto de dados para outro funcionam desde que seus valores de chave correspondam. Agregações de data/hora são manipuladas pelo tempo de execução do relatório móvel e corresponderão entre diferente conjuntos de dados, mesmo que a granularidade de dados de data/hora seja diferente entre os conjuntos de dados.   
  
Você pode importar dados de dois tipos de fontes:   
  
* **Arquivos do Excel locais**: selecione um documento do Excel e escolha as planilhas a serem importadas. Após a importação, os dados são armazenados na definição de relatório móvel. Para atualizar os dados do arquivo original do Excel, use o comando **Atualizar Dados** no canto superior direito da guia **Dados** do [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]. Leia mais sobre como [preparar dados do Excel para relatórios SSRS móveis](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md).  
  
* **Conjuntos de dados compartilhados do [!INCLUDE[PRODUCT_NAME](../../includes/server-product-name.md)]**: navegue pela lista de conjuntos de dados publicados no servidor e selecione as opções para adicionar ao relatório móvel. Relatórios móveis baseados em dados de servidor sempre permanecem conectados aos conjuntos de dados do servidor original e refletem o estado mais recente dos dados no servidor. Veja uma [lista de fontes de dados com suporte](https://msdn.microsoft.com/library/ms159219.aspx).   
  
  Leia mais sobre [obter dados de conjuntos de dados no compartilhados no Publicador de Relatórios Móveis](../../reporting-services/mobile-reports/get-data-from-shared-datasets-in-reporting-services-mobile-reports.md).  
  
Depois de importar os dados para o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)], o restante da experiência de criação e design de relatório móvel é a mesma, independentemente de onde vêm os dados.   
  
## Conectar elementos de relatório móvel a dados ##  
  
Cada elemento [!INCLUDE[PRODUCT_NAME](../../includes/short-product-name.md)] contém uma ou mais configurações de dados. Por exemplo, o elemento Medidor Radial contém duas configurações de dados: valor principal e o valor de comparação. Cada uma dessas configurações aponta para exatamente um campo (coluna) em um conjunto de dados específico.   
  
O tempo de execução do relatório móvel fornece valores agregados para o medidor, com base nas seleções do usuário. Observe que o valor de comparação da mesma instância do Medidor Radial pode ser associado a um campo de um conjunto de dados diferente.   
  
### Consulte também  
-  [Preparar dados para relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
- [Criar e publicar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
- [Obter dados de conjuntos de dados compartilhados](../../reporting-services/mobile-reports/get-data-from-shared-datasets-in-reporting-services-mobile-reports.md)
- [Reter a formatação de data para dados do Analysis Services em relatórios móveis](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) 
  
  
