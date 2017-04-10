---
title: "Correspond&#234;ncia de qualidade de dados no Suplemento do MDS para Excel | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: be78d051-0d56-46d3-bb89-327e218dadd6
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Correspond&#234;ncia de qualidade de dados no Suplemento do MDS para Excel
  Com o tempo, você desejará adicionar mais dados ao repositório do MDS. Antes de adicionar dados, talvez seja útil comparar os novos dados aos dados que já são gerenciados no MDS, para assegurar que você não está adicionando dados duplicados ou inexatos.  
  
 O [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] MDS usa o recurso DQS (Data Quality Services) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para associar a dados semelhantes. Quando você usar a funcionalidade correspondente no suplemento, serão agrupados registros semelhantes e uma pontuação que representa a exatidão do resultado exibido. Para obter mais informações sobre a funcionalidade de correspondência fornecida pelo DQS, consulte [Correspondência de dados](../../data-quality-services/data-matching.md).  
  
## Fluxo de trabalho para correspondência de qualidade de dados  
 Ao usar o DQS com o MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], use o fluxo de trabalho seguinte:  
  
1.  Recupere uma lista de dados gerenciados no MDS e combine-a com uma lista não gerenciada no MDS. Para obter mais informações, consulte [Combinar dados &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md).  
  
2.  Use o conhecimento do DQS para comparar os dados na lista combinada. Para obter mais informações, consulte [Corresponder dados semelhantes &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md).  
  
3.  Para exibir mais detalhes sobre as semelhanças encontradas pelo DQS, mostre as colunas de detalhe.  
  
4.  Analise os resultados e determine quais dados devem ser adicionados ao repositório do MDS e quais dados são duplicados.  
  
5.  Publique os dados novos e/ou atualizados no repositório do MDS.  
  
## Bases de dados de conhecimento  
 Os resultados correspondentes fornecidos no suplemento se baseiam em uma base de dados de conhecimento do DQS.  
  
-   A base de dados de conhecimento padrão (Dados do DQS) é criada quando o DQS é instalado. Se você escolher usar a base de conhecimento padrão (sem adicionar uma política de correspondência à base de conhecimento padrão no Cliente Data Quality), você deverá mapear colunas na planilha para domínios na base de dados de conhecimento e, em seguida, atribuir um valor de peso aos domínios que você escolher.  
  
-   Você pode usar o Cliente Data Quality para criar uma nova base de dados de conhecimento com uma política de correspondência ou adicionar uma política de correspondência à base de dados de conhecimento padrão. Nesse caso, os valores de peso são determinados pela política correspondente que você já criou e só é necessário mapear as colunas para os domínios. Para obter mais informações, consulte [Create a Matching Policy](../../data-quality-services/create-a-matching-policy.md).  
  
 Para obter mais informações sobre bases de dados de conhecimento, consulte [Bases de Dados de Conhecimento DQS e domínios](../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
## Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Combine dados externos com dados gerenciados no MDS na preparação para compará-los.|[Combinar dados &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)|  
|Use o conhecimento do DQS para localizar semelhanças em seus dados.|[Corresponder dados semelhantes &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)|  
  
## Conteúdo relacionado  
  
-   [Visão geral: Importando dados do Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Correspondência de dados](../../data-quality-services/data-matching.md)  
  
  