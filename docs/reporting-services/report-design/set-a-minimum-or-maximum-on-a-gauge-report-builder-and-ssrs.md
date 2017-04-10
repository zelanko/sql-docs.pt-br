---
title: "Definir m&#237;nimo ou m&#225;ximo em um medidor (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
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
ms.assetid: b4c260c0-5a88-4f30-8977-eb5cc78fc146
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Definir m&#237;nimo ou m&#225;ximo em um medidor (Construtor de Relat&#243;rios e SSRS)
  Diferente de gráficos em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)], em que vários grupos são definidos, os medidores mostram apenas um valor. Como o Construtor de Relatórios e o Designer de Relatórios determinam o contexto ou a significância relativa do valor que você está tentando mostrar no medidor, defina o mínimo e o máximo da escala.   
    
  Por exemplo, se seus valores de dados tiverem classificações entre 0 e 10, você desejará definir o mínimo como 0 e o máximo como 10. Os números do intervalo são calculados automaticamente com base nos valores especificados para o mínimo e máximo. Por padrão, o mínimo e o máximo são definidos como 0 e 100, mas esse é um valor arbitrário que você deve alterar. O aplicativo não calcula seu valor como uma porcentagem.  
  
 Se o intervalo dos seus valores for grande, por exemplo, de 0 a 10.000, considere usar um multiplicador pra reduzir o número de zeros no medidor. O multiplicador só reduzirá a escala dos números do medidor, não o valor em si.  
  
 Você pode usar expressões para definir os valores das opções **Mínimo** e **Máximo**. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
## Para definir o mínimo e o máximo no medidor  
  
1.  Clique com o botão direito do mouse na escala e selecione **Propriedades da Escala**. É exibida a caixa de diálogo **Propriedades da Escala**.  
  
2.  Em **Geral**, especifique um valor para **Mínimo**. Por padrão, esse valor é 0. Se preferir, clique no botão **Expressão** (*fx*) para editar a expressão que define o valor da opção.  
  
3.  Especifique um valor para **Máximo**. Por padrão, esse valor é 100. Se preferir, clique no botão **Expressão** (*fx*) para editar a expressão que define o valor da opção.  
  
4.  (Opcional) Se os valores para mínimo e máximo forem grandes, especifique um valor para a opção **Multiplicar rótulos da escala por**. Para especificar um multiplicador que reduza sua escala, use um número decimal. Por exemplo, se você tiver uma escala de 0 a 1.000, poderá especificar um valor de multiplicador de 0,01 para reduzir a escala para ler 0 a 10.  
  
## Consulte também  
 [Formatando escalas em um medidor &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formatando ponteiros de um medidor &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  