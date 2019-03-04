---
title: Trabalhar com os dados simulados em relatórios móveis do Reporting Services | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 6baabc36-58fb-4a98-bb9c-c42bafb16d0f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e7b776893c15532efc1d2dac54d16a7bc9035991
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295896"
---
# <a name="work-with-simulated-data-in-reporting-services-mobile-reports"></a>Trabalhar com dados simulados em relatórios do Reporting Services móveis
Quando você coloca um elemento de galeria na superfície do design, [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] gera imediatamente dados simulados para esse elemento. Esses dados servem para várias finalidades úteis ao criar relatórios móveis.   
  
![SS_MRP_SimDataTreeMapProps](../../reporting-services/mobile-reports/media/ss-mrp-simdatatreemapprops.png)  
  
Dados simulados ajudam ao usar uma abordagem baseada em projeto para a criação de relatório móvel. Inicialmente, o preenchimento de elementos com dados simulados permite que você crie protótipos de relatório móveis rapidamente sem ter que lidar com requisitos específicos de dados. Esses relatórios móveis podem, então, ser avaliados quanto a estética e eficiência geral.  
  
## <a name="create-an-excel-file-with-simulated-data-as-a-template"></a>Criar um arquivo do Excel com dados simulados como modelo  
  
Dados simulados também fornecem um modelo que representa com precisão os requisitos de dados de um design de relatório móvel específico.   
  
-  Clique em **Exportar todos os dados** no canto superior direito da Exibição de Dados.   
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] gera um documento do Excel que contém os dados simulados, permitindo a rápida substituição de dados reais, prontos para importação.   
  
## <a name="how-simulated-data-behaves"></a>Como os dados simulados se comportam  
  
Os dados simulados gerados são projetados especificamente para o relatório móvel que você está criando. À medida que você coloca mais elementos na superfície do design, os dados simulados associados aumentam e mudam para fornecer a melhor experiência possível sem dados reais. Essa evolução garante que campos extras e possibilidades de filtro estejam disponíveis, caso você adicione séries extras às visualizações do gráficos ou expanda o escopo de um ou mais elementos do relatório móvel de outra maneira.  
  
Conforme mencionado anteriormente, você pode exportar dados simulados para um arquivo do Excel, criando um modelo de dados perfeito para o relatório móvel associado. Você pode trocar seus próprios dados reais no arquivo do Excel e importá-lo novamente para o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].   
  
Depois que todos os controles são associados a dados reais, as tabelas simuladas que não estão mais em uso são automaticamente removidas do relatório móvel. Não é possível remover tabelas simuladas ainda referenciadas por elementos na superfície do design.  
  
>**Observação**: os dados simulados não acrescentam à superfície geral móvel do relatório porque não são serializados com o relatório móvel, mas gerados dinamicamente em tempo de execução.  
  
### <a name="see-also"></a>Confira também  
- [Criar e publicar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  Exibir [relatórios móveis do SQL Server e KPIs no aplicativo de iPad](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI para iOS)  
-  Exibir [relatórios móveis do SQL Server e KPIs no aplicativo do iPhone](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI para iOS)  
  
  
  
  
  

