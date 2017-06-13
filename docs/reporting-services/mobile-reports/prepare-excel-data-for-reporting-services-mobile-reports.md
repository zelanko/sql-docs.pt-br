---
title: "Preparar os dados do Excel para relatórios móveis do Reporting Services | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 02/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16698f8d-bfc7-4eca-9e97-82c99d8bc08e
caps.latest.revision: 14
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c057de4b56529de08385a1e13e1a119550632eda
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="prepare-excel-data-for-reporting-services-mobile-reports"></a>Preparar dados do Excel para relatórios móveis do Reporting Services
  
Veja alguns pontos a serem lembrados ao preparar um arquivo e planilhas do Excel para uso com um relatório móvel:  
  
## <a name="do"></a>O que fazer  
  
- Ter uma planilha por conjunto de dados.  
- Ter cabeçalhos de coluna na primeira linha.  
- Manter a consistência dos tipos de dados dentro de cada coluna.  
- Formatar células conforme os tipos adequados no Excel.  
- Colocar os dados em planilhas, não no Modelo de Dados do Excel.  
- Ao usar fórmulas, assegurar-se de que a coluna inteira seja calculada usando a mesma fórmula.  
- Usar o Excel 2007 ou posterior.  
- Salvar os arquivos do Excel com a extensão XLSX.  
          
## <a name="dont"></a>O que não fazer  
  
- Incluir imagens, gráficos, Tabelas Dinâmicas ou outros objetos inseridos em planilhas de conjunto de dados.  
- Incluir linhas calculadas ou totais.  
- Manter o arquivo aberto no Excel durante a importação.  
- Formatar números manualmente adicionando moeda ou outros símbolos.  
- Usar uma pasta de trabalho com dados armazenados no Modelo de Dados.  
  
## <a name="worksheets"></a>Planilhas  
          
Ao preparar um arquivo do Excel como um conjunto de dados para um relatório móvel, verifique se você tem apenas um conjunto de dados por planilha. Cada planilha individual é importada no [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] como uma tabela separada. As planilhas com nomes idênticos de várias fontes do Excel são renomeadas na importação com o acréscimo de números incrementais. Por exemplo, se uma pasta de trabalho tiver três planilhas intituladas "MyWorksheet", a segunda e terceira serão renomeadas como "MyWorksheet0" e "MyWorksheet1". A captura de tela abaixo ilustra as primeiras linhas de uma planilha ideal do Excel pronta para importação.  
  
![SS_MRP_ExcelDataSheet](../../reporting-services/mobile-reports/media/ss-mrp-exceldatasheet.png)  
          
## <a name="column-headers"></a>Cabeçalhos de coluna  
  
Como você pode ver no exemplo acima, a primeira linha contém o nome da métrica na coluna em questão. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] preserva esses cabeçalhos de coluna para facilitar a referência nas configurações de elemento da galeria. No entanto, os cabeçalhos de coluna não são necessários. Se ausentes, o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] vai gerar cabeçalhos usando a convenção A,B,C,...,AA,BB,... do Excel.  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]detecta automaticamente os cabeçalhos da primeira linha na importação das planilhas do Excel comparando os tipos de dados das primeiras duas células em cada coluna. Se os tipos de dados das duas primeiras células em qualquer coluna não corresponderem, a primeira linha será determinada para conter cabeçalhos de coluna. Portanto, se uma tabela tiver cabeçalhos de coluna numérica, coloque uma cadeia de caracteres antes dos nomes de cabeçalho para que eles sejam detectados como cabeçalhos no processo de importação.  
  
## <a name="cells"></a>Células  
  
Os dados de célula em cada coluna do conjunto de dados de uma planilha precisam ser consistentes. Cada coluna recebe um tipo de dados na importação. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] detecta automaticamente os tipos de dados como cadeia de caracteres, duplo (numérico), booliano (true/false) ou data/hora. Os tipos de dados misturados na mesma coluna podem fazer com que essa detecção seja imprecisa ou falhe completamente. Essa detecção considera possíveis cabeçalhos de coluna como sendo do tipo de cadeia de caracteres. As células devem ser formatadas como o tipo correto no Excel para garantir que o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] detecte os tipos desejados. No exemplo acima, as seis colunas seriam tipadas como:  
*  Uma coluna de data/hora  
*  Uma coluna de cadeia de caracteres  
*  Quatro colunas duplas  
  
Se uma planilha contiver fórmulas ou células calculadas, somente o valor de exibição resultante será importado no [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
## <a name="file-location-and-refreshing-excel-data"></a>Local do arquivo e atualização de dados do Excel  
  
Não existem restrições quanto ao local de armazenamento de arquivos do Excel que você importa no [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]. No entanto, se você mover ou renomear o arquivo após a importação, não será possível atualizar os dados por meio do comando **atualizar todos os dados** encontrado na Exibição de Dados.   
  
>**Observação**: o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] não atualiza automaticamente os dados do Excel. Você poderá atualizar os dados por meio do comando [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] **refresh** command, but only if the file hasn't moved.  
  
## <a name="dates"></a>Datas  
  
Os campos de data são essenciais para muitos relatórios móveis. Portanto, assegure-se de que as células sejam corretamente formatadas como datas no Excel. Em alguns casos, isso significa que uma conversão é necessária. Veja exemplos de fórmulas para converter células de texto em datas no Excel.  
  
    Week 24-2013=DATE(MID(A2,9,4),1,-2)-WEEKDAY(DATE(MID(A2,9,4),1,3))+MID(A2,6,2)*7  
  
    2013/03/21=DATEVALUE(A1)  
  
    2013-mar-12=DATEVALUE(RIGHT(A1,2)&"-"&MID(A1,6,3)&"-"&LEFT(A1,4))  
  
Depois de converter as células, é preciso formatá-las como datas selecionando-as ou a coluna inteira > menu **Contexto** > **Formatar Células** > **Data** na lista **Categoria**. Você também pode usar o assistente de texto para colunas do Excel para converter células de texto em datas corretamente formatadas.  
  
## <a name="unsupported"></a>Sem suporte  
  
Os dados de planilha em formatos diferentes dos descritos acima podem causar resultados imprevisíveis quando importados. É uma boa prática restringir planilhas em um arquivo do Excel somente àquelas que estão no formato correto para uso com um relatório móvel.  
  
Os objetos personalizados em planilhas do Excel, incluindo Tabelas Dinâmicas, visualizações e imagens, não são importados no [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
### <a name="see-also"></a>Consulte também  
- [Preparar dados para relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)  
- [Criar e publicar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  Exibir [relatórios móveis do SQL Server e KPIs no aplicativo de iPad](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI para iOS)  
-  Exibir [relatórios móveis do SQL Server e KPIs no aplicativo do iPhone](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI para iOS)  
  
  
  
  
  
  
  


