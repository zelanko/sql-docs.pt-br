---
title: "Exibir o plano de execu&#231;&#227;o estimado | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "zoom [SQL Server]"
  - "plano de execução estimado [SQL Server]"
  - "exibindo planos de execução"
  - "exibindo planos de execução"
  - "planos de execução [SQL Server], exibindo"
  - "personalizando a exibição do plano de execução [SQL Server]"
  - "modificando a exibição do plano de execução"
  - "personalizar zoom [SQL Server]"
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 26
---
# Exibir o plano de execu&#231;&#227;o estimado
  Este tópico descreve como gerar planos de execução gráfica estimados usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Quando são gerados planos de execução estimados, as consultas ou lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] não são executadas. Ao invés disso, o plano de execução gerado exibe o plano de execução de consulta que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] teria maior probabilidade de usar se fossem executadas consultas.  
  
 Para usar esse recurso, os usuários devem ter as permissões apropriadas para executar a consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para as quais está sendo gerado um plano de execução gráfica e devem ter permissão SHOWPLAN para todos os bancos de dados incluídos na consulta.  
  
### Para exibir o plano de execução estimado para uma consulta  
  
1.  Na barra de ferramentas, clique em **Consulta do Mecanismo de Banco de Dados**. Você também pode abrir uma consulta existente e exibir o plano de execução estimado clicando no botão de barra de ferramentas **Abrir Arquivo** e localizando a consulta existente.  
  
2.  Insira a consulta para a qual você deseja exibir o plano de execução estimado.  
  
3.  No menu **Consulta**, clique em **Exibir Plano de Execução Estimado** ou clique no botão de barra de ferramentas **Exibir Plano de Execução Estimado**. O plano de execução estimado é exibido na guia **Plano de execução** no painel de resultados. Para exibir mais informações, mantenha o mouse sobre os ícones dos operadores lógicos e físicos e exiba a dica de tela com a descrição e as propriedades do operador. Você também pode exibir propriedades do operador na janela Propriedades. Se a janela Propriedades não estiver visível, clique com o botão direito do mouse em um operador e clique em **Propriedades**. Selecione um operador cujas propriedades exibir.  
  
4.  Para alterar a exibição do plano de execução, clique com o botão direito do mouse no plano de execução e selecione **Ampliar**, **Reduzir**, **Zoom Personalizado** ou **Ajustar Nível de Zoom**. **Ampliar** e **Reduzir** permitem ampliar ou reduzir o plano de execução com valores fixos. **Zoom personalizado** permite que você defina sua própria ampliação da exibição, como ampliar em 80 por cento. **Ajustar Nível de Zoom** aumenta o plano de execução para se ajustar ao painel de resultados.  
  
  