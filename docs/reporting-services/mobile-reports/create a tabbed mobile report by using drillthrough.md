---
title: "Criar um relat&#243;rio m&#243;vel com guias usando o detalhamento | Relat&#243;rios m&#243;veis do Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Criar um relat&#243;rio m&#243;vel com guias usando o detalhamento | Relat&#243;rios m&#243;veis do Reporting Services
Saiba como criar um relatório móvel do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] com aparência e funcionamento de um relatório com guias usando detalhamento e parâmetros.

Por exemplo, neste relatório, os indicadores na parte superior funcionam como guias. Quando você clica no medidor Transporte, os dados no restante do gráfico são filtrados para exibir os dados de transporte.

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

Nos bastidores, isso é realmente um conjunto de cinco relatórios separados, cada um com um parâmetro diferente que filtra o relatório para corresponder ao medidor selecionado na parte superior do relatório. 

Neste exemplo, você cria todos os cinco relatórios primeiro e, para cada um dos cinco relatórios, você faz os outros quatro medidores em detalhamento para os outros quatro relatórios. 

Eis uma descrição de alto nível das etapas.

1. Crie um relatório chamado Vendas com cinco medidores:
     - Sales
     - Transporte
     - Combustível
     - Armazenamento
     - Despesas diversas
2. Faça quatro cópias do relatório, chamadas: 
     - Transporte
     - Combustível
     - Armazenamento
     - Despesas diversas
3.  No relatório Vendas, defina cada um dos quatro medidores (que não seja o medidor Vendas) como detalhamentos para seus respectivos relatórios.

4. Ainda no relatório Vendas, defina a propriedade Destacar do medidor Vendas para contrastar com o restante do relatório. Dessa forma, ele fica em destaque.

5.  Agora, no relatório Transporte, defina o medidor Vendas como um detalhamento para o relatório Vendas e os outros três medidores como detalhamentos para seus respectivos relatórios.

6. Novamente, ainda no relatório Transporte, defina a propriedade Destacar do medidor Transporte para contrastar com o restante do relatório.

5. Repita para os relatórios Combustível, Armazenamento e Despesas diversas. 







  
