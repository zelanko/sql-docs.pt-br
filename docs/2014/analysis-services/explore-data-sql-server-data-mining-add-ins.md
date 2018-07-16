---
title: Explorar dados (SQL Server Data Mining Add-ins) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- histogram [data mining]
- data visualization
ms.assetid: 714845a9-4c27-461a-9ba3-149e1e818386
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 813da97a8128464ef105d27780f459060867f11c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177023"
---
# <a name="explore-data-sql-server-data-mining-add-ins"></a>Explorar dados (Suplementos de Mineração de Dados do SQL Server)
  ![Assistente de dados de explorar](media/dmc-explore.gif "Assistente para explorar dados")  
  
 O **explorar dados** assistente o ajudará a entender o tipo e a quantidade de dados na tabela de dados. O assistente representa graficamente a distribuição e os valores das colunas selecionadas, uma coluna por vez. Assim, você pode fazer experiências alterando a maneira como os dados são agrupados ou copiar um gráfico que mostra o conteúdo de uma pasta de trabalho do Excel para análise.  
  
 Se seus dados contiverem dados numéricos contínuos, você poderá ativar /desativar entre essas duas exibições:  
  
-   **Gráfico de linha.** Esse gráfico de linha coloca os valores de dados no eixo X e o número de casos no eixo Y.  
  
-   **Gráfico de barras.** Esse gráfico agrupa os valores pelo número de casos para cada valor.  
  
 Quando o assistente encontra grupos nos dados, ele usa a distribuição real dos valores de dados. Portanto, o gráfico de barras não mostra marcadores de eixo numérico de número inteiro típicos, como 10 ou 100. Em vez disso, os intervalos mostrados no gráfico de barras podem ser algo como 43521-55603 (para a coluna de renda).  
  
 Se você quiser agrupar os dados em outros intervalos, faça isso no Excel antes de analisar os dados. Ou, você pode rotular novamente os dados usando o [rotular novamente](relabel-sql-server-data-mining-add-ins.md) assistente.  
  
## <a name="using-the-explore-data-wizard"></a>Usando o Assistente para Explorar Dados  
  
1.  No **Data Mining** faixa de opções, clique em **explorar dados**.  
  
2.  No **Selecionar origem** caixa de diálogo, selecione a tabela ou intervalo de células que contém seus dados.  
  
3.  No **Selecionar coluna** caixa de diálogo, escolha a coluna a ser analisada, dos dados de exemplo exibidos no painel.  
  
4.  No **explorar dados** caixa de diálogo, escolha os tipos de gráfico para exibir a distribuição de dados.  
  
5.  Se desejar, adicione novas colunas aos dados, altere a segmentação dos dados ou copie o gráfico para o Excel.  
  
### <a name="requirements"></a>Requisitos  
 Para usar o **explorar dados** assistente, seus dados devem estar em uma tabela de dados do Excel.   
  
## <a name="see-also"></a>Consulte também  
 [Lista de verificação de preparação para mineração de dados](checklist-of-preparation-for-data-mining.md)  
  
  
