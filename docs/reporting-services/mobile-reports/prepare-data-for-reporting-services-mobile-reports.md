---
title: "Preparar dados para relatórios móveis do Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8adce9ad-6a08-4d20-b1cf-d3c45544d8de
caps.latest.revision: "15"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: eb1b7514e8ba88f4dacf3a521f6deb0d934dfa2d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="prepare-data-for-reporting-services-mobile-reports"></a>Preparar dados para relatórios móveis do Reporting Services
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] dá suporte a operações de dados complexas, incluindo a filtragem, agregação e divisão de tempo. Este artigo oferece alguns pontos a serem lembrados ao preparar os dados. A agregação prévia dos dados pode otimizar a criação e o uso de relatórios móveis e alguns designs de relatório móvel exigem isso.   
  
## <a name="date-and-time-formats"></a>Formatos de data e hora 
Ao lidar com intervalos de data e hora para uso em um relatório móvel, particularmente com TimeNavigator, é importante formatar adequadamente a coluna data/hora para que o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] possa identificá-la como tal. Aqui estão exemplos de formatos de data/hora válidos:  
  
    05/01/2009    
    2009-05-01    
    05/01/2009 14:57:32.8    
    2009-05-01 14:57:32.8    
    2009-05-01T14:57:32.8375298-04:00    
    5/01/2008 14:57:32.80 -07:00    
    1 May 2008 2:57:32.8 PM    
    Fri, 15 May 2009 20:10:57 GMT    
  
Conjuntos de dados com base em data e hora podem, na maioria dos casos, ser descritos por um ou mais intervalos de data/hora, como por hora, diariamente, mensalmente, trimestralmente e anualmente. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] pode combinar várias tabelas de granularidades diferentes e exibi-las em um único relatório móvel. No entanto, lembre-se dos intervalos relevantes dos conjuntos de dados originais, já que eles podem ajudar a decidir quais opções de filtro de data/hora apresentar ao usuário no relatório móvel final.  

Campos da data nos modelos multidimensionais e tabulares do [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] podem perder sua formatação de data em conjuntos de dados compartilhados. Consulte [Reter a formatação de data para Analysis Services em relatórios móveis](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) para uma solução que mantém sua formatação.
  
## <a name="preparing-filter-data"></a>Preparando dados de filtro ##  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] pode filtrar dados com base em campos de data/hora e campos de chave. Embora os campos de chave possam ser numéricos, na maioria dos casos eles são uma ID ou um valor de cadeia de caracteres. Para preparar um campo de filtro para uso com um elemento de navegação como a lista de seleção, a chave de filtro deve ser uma única coluna na tabela de dados. Dessa forma, você pode agrupar as linhas da tabela de acordo com o valor na coluna de filtro. Ter várias colunas com chaves de filtro ou critérios de filtro diferentes permite que relatórios móveis com vários navegadores de filtro sejam usados juntos hierarquicamente ou individualmente.  
  
| Setor  | País   | Região    |  
| ------------- | ------------- | ------------- |  
| Bancos     | AFEGANISTÃO   | ÁSIA      |  
| Serviços comerciais e profissionais | AFEGANISTÃO | ÁSIA |  
| Alimentação, bebidas e tabaco | AFEGANISTÃO | ÁSIA |  
| Mídia | AFEGANISTÃO | ÁSIA |  
| Produtos farmacêuticos | AFEGANISTÃO | ÁSIA |  
| Varejo de alimentos e produtos básicos | ALBÂNIA | EUROPA |  
  
  
Filtros com base em chave também podem ser estruturados hierarquicamente para uso com uma lista de seleção em uma estrutura de árvore. Para preparar dados para uso nesse tipo de cenário, crie uma tabela de pesquisa que descreva a estrutura hierárquica. Use uma estrutura de tabela que inclui uma coluna de chave e uma coluna de chave primária para indicar onde o nó se localiza em toda a hierarquia.  
  
Nesta tabela, os itens de ParentKey primeiro são listados na coluna ItemKey, em seguida, listados na coluna ParentItemKey ao lado dos itens filho.   
  
|ItemKey    | ParentItemKey |  
| ------------- | ------------- |  
| Financeiro    |   |  
| Industriais   |   |  
| Produtos básicos do consumidor |    |  
| A critério do consumidor |  |     
| Saúde   |   |  
| Tecnologia da informação |  |  
| Bancos | Financeiro |  
| Imóveis | Financeiro |  
| Financeiro diversificado |  Financeiro |   
| Seguro |   Financeiro |  
| Serviços comerciais e profissionais |  Industriais |  
| Bens de capital |   Industriais |  
| Transporte |  Industriais |  
| Alimentação, bebidas e tabaco |    Produtos básicos do consumidor |  
| Varejo de alimentos e produtos básicos |    Produtos básicos do consumidor |  
| Produtos pessoais e do lar | Produtos básicos do consumidor |  
| Mídia | A critério do consumidor |  
| Automóveis e componentes |  A critério do consumidor |  
| Bens duráveis e vestuário do consumidor |A critério do consumidor |  
| Serviços ao consumidor |   A critério do consumidor |  
| Varejo | A critério do consumidor |  
| Produtos farmacêuticos   | Saúde |  
| Serviços e equipamentos de saúde |    Saúde |  
| Software e serviços | Tecnologia da informação |  
| Hardware e equipamentos de tecnologia   | Tecnologia da informação |  
| Serviços de telecomunicação |Tecnologia da informação |  
  
### <a name="see-also"></a>Consulte também  
- [Preparar dados do Excel para relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)  
- [Reter a formatação de data para Analysis Services em relatórios móveis](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md)
- [Criar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
  
  
  

