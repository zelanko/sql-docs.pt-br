---
title: Especifique marcar como tabela de data para uso com inteligência de tempo (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 30841d1f-0c3b-4575-8f4a-27a1492e248c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af799e8e806696022635a04d808213ffb5c0e779
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148566"
---
# <a name="specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular"></a>Especifique Marcar como Tabela de Data para uso com Inteligência de Tempo (SSAS tabular)
  Para usar funções de inteligência de tempo em fórmulas DAX, você deverá especificar uma tabela de datas e uma coluna de identificador exclusivo (datetime) do tipo de dados de data. Quando uma coluna na tabela de datas é especificada como um identificador exclusivo, você pode criar relações entre colunas na tabela de datas e qualquer tabela de fatos.  
  
 Ao usar as funções de inteligência de dados de tempo, as seguintes regras se aplicam:  
  
-   Ao usar as funções de inteligência de dados de tempo DAX, nunca especifique uma coluna de datetime de uma tabela de fatos. Sempre crie uma tabela de datas separada em seu modelo com pelo menos uma coluna de datetime de tipo de dados de data e com valores exclusivos.  
  
-   Tenha certeza de que sua tabela de datas tem um intervalo de datas contínuo.  
  
-   A coluna de datetime na tabela de datas deve ter uma granularidade de dia (sem frações de um dia).  
  
-   Você deve especificar uma tabela de data e uma coluna de identificador exclusivo usando a caixa de diálogo **Marcar como Tabela de Datas** .  
  
-   Crie relações entre tabelas de fatos e colunas de tipo de dados de data na tabela de datas.  
  
#### <a name="to-specify-a-date-table-and-unique-identifier"></a>Para especificar uma tabela de datas e um identificador exclusivo  
  
1.  No designer de modelos, clique na tabela de datas.  
  
2.  Clique no menu **Tabela** , clique em **Data**e em **Mark as Data Tabela**.  
  
3.  Na caixa de diálogo **Marcar como Tabela de Data** , na caixa de listagem **Data** , selecione uma coluna a ser usada como um identificador exclusivo. Esta coluna deve conter valores exclusivos e deve ser do tipo de dados de data. Por exemplo:  
  
    |data|  
    |----------|  
    |7/1/2010 12:00:00 AM|  
    |7/2/2010 12:00:00 AM|  
    |7/3/2010 12:00:00 AM|  
    |7/4/2010 12:00:00 AM|  
    |7/5/2010 12:00:00 AM|  
  
4.  Se necessário, crie qualquer relação entre tabelas de fatos e a tabela de datas.  
  
## <a name="see-also"></a>Consulte também  
 [Cálculos de &#40;Tabular do SSAS&#41;](calculations-ssas-tabular.md)   
 [Funções de inteligência de tempo &#40;DAX&#41;](https://msdn.microsoft.com/library/ee634763.aspx)  
  
  
