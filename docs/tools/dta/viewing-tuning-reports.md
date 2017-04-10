---
title: "Exibindo relat&#243;rios de ajuste | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "ajustando relatórios [SQL Server]"
ms.assetid: daee6143-269f-428b-8458-9a3e726d586c
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Exibindo relat&#243;rios de ajuste
Na prática anterior desta lição, você exibiu os scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] que criam ou cancelam objetos de banco de dados nas recomendações do Orientador de Otimização do Mecanismo de Banco de Dados que foram geradas como resultado da sessão de ajuste MySession. A sessão de ajuste MySession foi criada no [Tuning a Workload](../../tools/dta/tuning-a-workload.md).  
  
Além de ser muito útil para exibir os scripts que podem ser usados para implementar os resultados de ajuste, o Orientador de Otimização do Mecanismo de Banco de Dados fornece muitos relatórios úteis que você pode exibir. Esses relatórios fornecem informações sobre as estruturas de design físico existentes no banco de dados que você está ajustando, e sobre as estruturas recomendadas. Os relatórios de ajuste podem ser exibidos clicando na guia **Relatórios** , como descrito na prática abaixo. Esta prática usa as sessões de ajuste MySession e EvaluateMySession que você criou no [Tuning a Workload](../../tools/dta/tuning-a-workload.md) e no [Viewing Tuning Recommendations](../../tools/dta/viewing-tuning-recommendations.md).  
  
### Exibição de relatórios de ajuste  
  
1.  Inicie o Orientador de Otimização do Mecanismo de Banco de Dados. Consulte [Iniciando o Orientador de Otimização do Mecanismo de Banco de Dados](../../tools/dta/launching-database-engine-tuning-advisor.md). Verifique se você está conectado à mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usou nas práticas anteriores desta lição.  
  
    Clique duas vezes em **MySession** no painel **Monitor de Sessão**. O Orientador de Otimização do Mecanismo de Banco de Dados carrega as informações desta sessão.  
  
2.  Clique na guia **Relatórios** .  
  
3.  No painel **Resumo do Ajuste** , você pode exibir informações sobre esta sessão de otimização. Use a barra de rolagem para exibir todo o conteúdo do painel. Preste atenção no **Aperfeiçoamento de percentual esperado** e no **Espaço usado por recomendação**. É possível limitar o espaço usado pela recomendação quando você define as opções de ajuste. Na guia **Opções de Ajuste** , selecione **Opções Avançadas**. Marque **Definir espaço máximo para recomendações** e especifique, em megabytes, o espaço máximo que uma configuração de recomendada pode usar. Use o botão **Voltar** em seu navegador de ajuda para voltar a este tutorial.  
  
4.  No painel **Relatórios de Ajuste** , clique em **Relatório de custo da instrução** na lista **Selecionar relatório** . Se precisar de mais espaço para exibir o relatório, arraste a borda do painel **Monitor de Sessão** para a esquerda. Cada instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] executada em uma tabela em seu banco de dados tem um custo de desempenho associado. Esse custo de desempenho pode ser reduzido criando índices efetivos em colunas acessadas frequentemente em uma tabela. Esse relatório mostra a porcentagem estimada de aperfeiçoamento entre o custo original de executar uma instrução na carga de trabalho e o custo se a recomendação de ajuste for implementada. Note que a quantidade de informações contida no relatório é baseada no tamanho e na complexidade da carga de trabalho.  
  
5.  Clique com o botão direito do mouse no painel **Relatório de custo da instrução** na área da grade e clique em **Exportar para o Arquivo**. Salve o relatório como **MyReport**. Será anexada automaticamente uma extensão .xml ao nome do arquivo. Você pode abrir MyReport.xml em seu editor de XML favorito ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibir o conteúdo do relatório.  
  
6.  Volte à guia **Relatórios** do Orientador de Otimização do Mecanismo de Banco de Dados e clique novamente com o botão direito do mouse em **Relatório de custo da instrução**. Revise as outras opções disponíveis. Note que você pode alterar a fonte do relatório que está exibindo. Alterar a fonte aqui também altera nas outras páginas de guias.  
  
7.  Clique em outros relatórios na lista **Selecionar relatório** para se familiarizar com eles.  
  
## Resumo  
Você explorou a guia **Relatórios** da sessão de ajuste MySession na interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados. Você pode usar esses mesmos passos para explorar os relatórios que foram gerados para a sessão de ajuste EvaluateMySession. Clique duas vezes em **EvaluateMySession** no painel **Monitor de Sessão** para começar.  
  
## Próxima lição  
[Lição 3: Usando o utilitário de prompt de comando dta](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
  
  
  
