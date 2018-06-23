---
title: Correspondência de qualidade de dados no Suplemento MDS para Excel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: be78d051-0d56-46d3-bb89-327e218dadd6
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 08040fafaa66570d3c0f2023bc1a66d0f82c1d4d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008454"
---
# <a name="data-quality-matching-in-the-mds-add-in-for-excel"></a>Correspondência de qualidade de dados no Suplemento do MDS para Excel
  Com o tempo, você desejará adicionar mais dados ao repositório do MDS. Antes de adicionar dados, talvez seja útil comparar os novos dados aos dados que já são gerenciados no MDS, para assegurar que você não está adicionando dados duplicados ou inexatos.  
  
 O [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] MDS usa o recurso DQS (Data Quality Services) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para associar a dados semelhantes. Quando você usar a funcionalidade correspondente no suplemento, serão agrupados registros semelhantes e uma pontuação que representa a exatidão do resultado exibido. Para obter mais informações sobre a funcionalidade de correspondência fornecida pelo DQS, consulte [Correspondência de dados](../../data-quality-services/data-matching.md).  
  
## <a name="workflow-for-data-quality-matching"></a>Fluxo de trabalho para correspondência de qualidade de dados  
 Ao usar o DQS com o MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], use o fluxo de trabalho seguinte:  
  
1.  Recupere uma lista de dados gerenciados no MDS e combine-a com uma lista não gerenciada no MDS. Para obter mais informações, consulte [Combine Data &#40;MDS Add-in for Excel&#41;](combine-data-mds-add-in-for-excel.md).  
  
2.  Use o conhecimento do DQS para comparar os dados na lista combinada. Para obter mais informações, consulte [Match Similar Data &#40;MDS Add-in for Excel&#41;](match-similar-data-mds-add-in-for-excel.md).  
  
3.  Para exibir mais detalhes sobre as semelhanças encontradas pelo DQS, mostre as colunas de detalhe.  
  
4.  Analise os resultados e determine quais dados devem ser adicionados ao repositório do MDS e quais dados são duplicados.  
  
5.  Publique os dados novos e/ou atualizados no repositório do MDS.  
  
## <a name="knowledge-bases"></a>Bases de dados de conhecimento  
 Os resultados correspondentes fornecidos no suplemento se baseiam em uma base de dados de conhecimento do DQS.  
  
-   A base de dados de conhecimento padrão (Dados do DQS) é criada quando o DQS é instalado. Se você escolher usar a base de conhecimento padrão (sem adicionar uma política de correspondência à base de conhecimento padrão no Cliente Data Quality), você deverá mapear colunas na planilha para domínios na base de dados de conhecimento e, em seguida, atribuir um valor de peso aos domínios que você escolher.  
  
-   Você pode usar o Cliente Data Quality para criar uma nova base de dados de conhecimento com uma política de correspondência ou adicionar uma política de correspondência à base de dados de conhecimento padrão. Nesse caso, os valores de peso são determinados pela política correspondente que você já criou e só é necessário mapear as colunas para os domínios. Para obter mais informações, consulte [Create a Matching Policy](../../data-quality-services/create-a-matching-policy.md).  
  
 Para obter mais informações sobre bases de dados de conhecimento, consulte [Bases de Dados de Conhecimento DQS e domínios](../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Combine dados externos com dados gerenciados no MDS na preparação para compará-los.|[Combinar dados &#40;suplemento do MDS para Excel&#41;](combine-data-mds-add-in-for-excel.md)|  
|Use o conhecimento do DQS para localizar semelhanças em seus dados.|[Corresponder dados semelhantes &#40;Suplemento MDS para Excel&#41;](match-similar-data-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Publicando dados &#40;suplemento do MDS para Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Correspondência de dados](../../data-quality-services/data-matching.md)  
  
  