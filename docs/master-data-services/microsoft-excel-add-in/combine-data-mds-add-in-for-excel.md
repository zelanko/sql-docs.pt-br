---
title: "Combinar dados (Suplemento do MDS para Excel) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a867dc15-5a0d-457c-8304-ac323bcf9377
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Combinar dados (Suplemento do MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], combinar dados de duas planilhas quando você deseja comparar dados antes da publicação. Nesse procedimento, você combina dados de duas planilhas em uma. Assim, você pode executar mais comparações e determinar quais dados, se houver, publicar no repositório do MDS.  
  
## Pré-requisitos  
  
-   Você deve ter uma planilha que contenha dados gerenciados no MDS. Para obter mais informações, consulte [Exportar dados para o Excel do Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md).  
  
-   Você deve ter uma planilha que contenha dados que queira combinar com os dados gerenciados no MDS. Essa planilha deve ter uma linha de cabeçalho.  
  
### Para combinar dados não gerenciados em uma planilha gerenciada no MDS  
  
1.  Na planilha que contém dados gerenciados no MDS, o **Publicar e validar** clique em **combinar dados**.  
  
2.  No **combinar dados** caixa de diálogo, em seguida o **intervalo a ser combinado com dados do MDS** texto, clique no ícone. A caixa de diálogo é recolhida.  
  
3.  Clique na planilha que contém os dados que você deseja combinar.  
  
4.  Realce todas as células na planilha que você deseja combinar, inclusive a linha de cabeçalho.  
  
5.  No **combinar dados** caixa de diálogo, clique no ícone. A caixa de diálogo é expandida.  
  
6.  Para uma coluna listada para a entidade do MDS, selecione uma coluna em **coluna correspondente**. Nem todas as colunas do MDS precisam de colunas correspondentes.  
  
7.  Clique em **combinar**. Um **fonte** coluna é exibida, indicando se os dados são do MDS ou de uma fonte externa.  
  
## Próximas etapas  
  
-   Para localizar semelhanças entre os dados gerenciados no MDS e externos, consulte [corresponder dados semelhantes e 40; Suplemento do MDS para Excel e 41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md).  
  
## Consulte também  
 [Visão geral: Exportando dados para o Excel e 40; Suplemento do MDS para Excel e 41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Correspondência de qualidade de dados no Suplemento do MDS para Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
  