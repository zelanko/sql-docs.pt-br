---
title: "Adicionar um HTML a um relat&#243;rio (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Adicionar um HTML a um relat&#243;rio (Construtor de Relat&#243;rios e SSRS)
  Usando um espaço reservado, você pode importar HTML de um campo em seu conjunto de dados para usar no relatório. Por padrão, um espaço reservado representa texto sem-formatação, portanto você precisará alterar o tipo de marcação do espaço reservado para HTML. Para obter mais informações, consulte [Importando HTML para um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para adicionar HTML de um campo em seu conjunto de dados a uma caixa de texto  
  
1.  Na guia **Inserir**, clique em **Lista**. Clique na superfície de design e arraste-a para criar uma caixa com o tamanho desejado.  
  
     A caixa de diálogo **Propriedades do Conjunto de Dados** é aberta. Você pode usar um conjunto de dados compartilhado ou um conjunto de dados inserido em seu relatório. Para obter mais informações, clique em [Caixa de diálogo Propriedades do Conjunto de Dados, Consulta &#40;Construtor de Relatórios&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) ou [Caixa de diálogo Propriedades do Conjunto de Dados, Consulta](../Topic/Dataset%20Properties%20Dialog%20Box,%20Query.md).  
  
2.  Na guia **Inserir** , clique em **Caixa de Texto**. Clique na lista e arraste-a para criar uma caixa com o tamanho desejado.  
  
3.  Arraste um campo HTML do conjunto de dados para a caixa de texto. Será criado um espaço reservado para seu campo.  
  
4.  Clique com o botão direito do mouse no espaço reservado e depois em **Propriedades do Espaço Reservado**.  
  
5.  Na guia **Geral**, verifique se a caixa **Valor** contém uma expressão que avalie para o campo descartado na etapa 3.  
  
6.  Clique em **HTML – Interpretar marcas HTML como estilos**. Isso faz com que o campo seja avaliado como HTML.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Consulte também  
 [Formatando números e datas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Formatando linhas, cores e imagens &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Espaço Reservado, Geral &#40;Construtor de Relatórios e SSRS&#41;](../Topic/Placeholder%20Properties%20Dialog%20Box,%20General%20\(Report%20Builder%20and%20SSRS\).md)  
  
  