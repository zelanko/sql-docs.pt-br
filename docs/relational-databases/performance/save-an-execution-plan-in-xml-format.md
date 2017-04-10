---
title: "Salvar um plano de execu&#231;&#227;o em formato XML | Microsoft Docs"
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
  - "planos de consulta XML [SQL Server]"
  - "abrindo planos de execução"
  - "Planos de execução XML [SQL Server]"
  - "planos de execução [SQL Server], salvando"
  - "salvando planos de execução"
ms.assetid: c439e53b-56f3-4442-97c6-dabd48a203d8
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Salvar um plano de execu&#231;&#227;o em formato XML
  Use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para salvar planos de execução como um arquivo XML e abri-los para exibição.  
  
 Para usar o recurso plano de execução em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ou usar as opções SET Showplan XML, os usuários devem ter as permissões apropriadas para executar a consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para qual um plano de execução está sendo gerado, e deve ser concedida a permissão SHOWPLAN para todos os bancos de dados referenciados pela consulta.  
  
### Para salvar um plano de consulta usando as opções SET Showplan XML  
  
1.  Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] abra um editor de consulta e conecte a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Ative o SHOWPLAN_XML com a instrução seguinte:  
  
    ```  
    SET SHOWPLAN_XML ON;  
    GO  
    ```  
  
     Para ativar o STATISTICS XML, use a instrução seguinte:  
  
    ```  
    SET STATISTICS XML ON;  
    GO  
    ```  
  
     O SHOWPLAN_XML gera informações de plano de execução de consulta de tempo de compilação para uma consulta, mas não executa a consulta. O STATISTICS XML gera informações de plano de execução de consulta em tempo de execução para uma consulta e executa a consulta.  
  
3.  Execute uma consulta. Exemplo:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SET SHOWPLAN_XML ON;  
    GO  
    -- Execute a query.  
    SELECT BusinessEntityID   
    FROM HumanResources.Employee  
    WHERE NationalIDNumber = '509647174';  
    GO  
    SET SHOWPLAN_XML OFF;  
    ```  
  
4.  No painel **Resultados**, clique com o botão direito do mouse em **Plano de execução XML do Microsoft SQL Server** que contém o plano de consulta e clique em **Salvar Resultados Como**.  
  
5.  Na caixa de diálogo **Salvar** \<Grid or Text> **Resultados**, na caixa **Salvar como tipo**, clique em **Todos os arquivos (\*.\*)**.  
  
6.  Na caixa **Nome do arquivo**, forneça um nome no formato \<name**>.sqlplan** e clique em **Salvar**.  
  
### Para salvar um plano de execução usando opções do SQL Server Management Studio  
  
1.  Gere um plano de execução estimado ou um plano de execução atual usando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obter mais informações, veja [Exibir o plano de execução estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md) ou [Exibir um plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md).  
  
2.  Na guia **Plano de execução** do painel de resultados, clique com o botão direito do mouse no plano de execução gráfico e escolha **Salvar Plano de Execução Como**.  
  
     Como alternativa, você também pode escolher **Salvar Plano de Execução Como** no menu **Arquivo** .  
  
3.  Na caixa de diálogo **Salvar Como**, verifique se a opção **Salvar como tipo** está definida como **Arquivos de Plano de Execução (\*.sqlplan)**.  
  
4.  Na caixa **Nome do arquivo**, forneça um nome no formato \<name**>.sqlplan** e clique em **Salvar**.  
  
### Para abrir um plano de consulta XML salvo em SQL Server Management Studio  
  
1.  Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Arquivo** , escolha **Abrir**e então clique em **Arquivo**.  
  
2.  Na caixa de diálogo **Abrir Arquivo**, defina **Arquivos de tipo** para **Arquivos de Plano de Execução (\*.sqlplan)** para gerar uma lista filtrada dos arquivos de plano de consulta XML salvos.  
  
3.  Selecione o arquivo plano consulta XML que você quer exibir e clique em **Abrir**.  
  
     Como alternativa, no Windows Explorer, clique duas vezes em um arquivo com a extensão **.sqlplan**. O plano abre em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## Consulte também  
 [SET SHOWPLAN_XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)   
 [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md)  
  
  