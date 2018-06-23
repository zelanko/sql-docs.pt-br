---
title: Mostrar conjuntos de dados ocultos para obter valores de parâmetro para dados multidimensionais (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eb01c4ca-4fd6-4629-b595-f0d2565915df
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 89df13eecdce33869199e0b5a8e82b0395679475
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009504"
---
# <a name="show-hidden-datasets-for-parameter-values-for-multidimensional-data-report-builder-and-ssrs"></a>Mostrar conjuntos de dados ocultos para obter valores de parâmetros para dados multidimensionais (Construtor de Relatórios e SSRS)
  Seu relatório pode incluir conjuntos de dados gerados automaticamente (também conhecidos como conjuntos de dados ocultos) que não aparecem por padrão no painel de dados do relatório. Esses conjuntos de dados são criados das seguintes formas:  
  
-   Em alguns designers de consulta para bancos de dados multidimensionais, você pode especificar campos a serem filtrados na área de filtro do painel de consulta e indicar se deseja criar um parâmetro de consulta para o filtro. Se você selecionar a opção de parâmetro, conjuntos de dados de relatório serão criados automaticamente para fornecer valores válidos para o parâmetro de relatório.  
  
-   Se você importar uma consulta baseada em bancos de dados multidimensionais, também poderá incluir conjuntos de dados ocultos em seu relatório.  
  
 Os conjuntos de dados ocultos não são disponibilizados a partir de um assistente.  
  
 Você pode alterar a exibição no painel de dados do relatório para exibir todos os conjuntos de dados no relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-hidden-datasets"></a>Para exibir conjuntos de dados ocultos  
  
-   No painel de dados do relatório, clique com o botão direito do mouse na pasta Conjuntos de Dados e clique em **Exibir Conjuntos de Dados Ocultos**.  
  
## <a name="see-also"></a>Consulte também  
 [Designers de Consultas &#40;Construtor de Relatórios&#41;](../query-designers-report-builder.md)   
 [Designers de Consultas do Reporting Services](../reporting-services-query-designers.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Adicionar dados a um relatório &#40;SSRS e construtor de relatórios&#41;](report-datasets-ssrs.md)  
  
  