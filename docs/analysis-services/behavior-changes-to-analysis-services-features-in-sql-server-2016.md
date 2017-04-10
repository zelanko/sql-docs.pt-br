---
title: "Altera&#231;&#245;es no comportamento de recursos do Analysis Services no SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# Altera&#231;&#245;es no comportamento de recursos do Analysis Services no SQL Server 2016
  Uma *alteração de comportamento* afeta a maneira como os recursos funcionam ou interagem na versão atual em comparação com as versões anteriores do SQL Server.  
  
 Revisões de valores padrão, a configuração manual necessária para concluir uma atualização ou restaurar a funcionalidade, ou então uma nova implementação de um recurso existente são exemplos de uma alteração de comportamento no produto.  
  
 Os comportamentos de recursos alterados nesta versão, mas que não interrompem um modelo ou código existente após a atualização, estão listados aqui.  
  
> [!NOTE]  
>  Em contraste com uma *alteração de comportamento*, uma *alteração significativa* é aquela que impede que um modelo de dados ou aplicativo integrado com [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seja executado após a atualização de um servidor, uma ferramenta de cliente ou um modelo. Para obter mais informações, consulte [Alterações Interruptivas em Recursos do Analysis Services no SQL Server 2016](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md).  
  
## Analysis Services no modo do SharePoint  
 Não é mais necessário executar o assistente de Configuração do Power Pivot como uma tarefa pós-instalação. Isso é verdadeiro para todas as versões com suporte do SharePoint que carregam modelos da versão [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] atual do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
## Modo DirectQuery para modelos de tabela  
 *DirectQuery* é um modo de acesso a dados para modelos de tabela, em que a execução da consulta é executada em um banco de dados relacional de back-end, recuperando um conjunto de resultados em tempo real. Ele geralmente é usado para grandes conjuntos de dados que não cabem na memória ou quando dados são voláteis e você deseja os dados mais recentes retornados em consultas a um modelo de tabela.  
  
 O DirectQuery já existe como um modo de acesso a dados em várias versões mais recentes. Em [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], a implementação foi ligeiramente revisada, supondo que o modelo de tabela está no nível de compatibilidade 1200. DirectQuery tem menos restrições do que antes. Ele também tem propriedades de banco de dados diferentes.  
  
 Se você estiver usando DirectQuery em um modelo de tabela existente, você poderá manter o modelo em seu nível de compatibilidade atual, 1100 ou 1103, e continuar a usar o DirectQuery, já que ele está implementado para esses níveis. Como alternativa, você pode atualizar para 1200 a fim de se beneficiar de aprimoramentos feitos ao DirectQuery nessa versão do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Não há nenhuma atualização in-loco de um modelo DirectQuery porque as configurações de níveis de compatibilidade mais antigos não têm contrapartes exatas no nível de compatibilidade 1200 mais recente. Se tiver um modelo tabular existente que é executado no modo DirectQuery, você deverá abrir o modelo no SQL Server Data Tools, desativar o DirectQuery, definir a propriedade **nível de compatibilidade** para 1200 e, em seguida, reconfigurar as propriedades DirectQuery como definidas para modelos de tabela 1200. Consulte [Modo DirectQuery &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md) para obter detalhes.  
  
## Consulte também  
 [Compatibilidade com versões anteriores_excluída](../Topic/Backward%20Compatibility_deleted.md)   
 [Alterações Interruptivas em Recursos do Analysis Services no SQL Server 2016](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md)   
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Baixar o SQL Server Data Tools](https://msdn.microsoft.com/en-us/library/mt204009.aspx)  
  
  