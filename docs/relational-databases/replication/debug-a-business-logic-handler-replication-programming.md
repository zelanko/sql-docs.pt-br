---
title: "Depurar um manipulador de l&#243;gica de neg&#243;cios (Programa&#231;&#227;o de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "manipuladores de lógica de negócios de replicação de mesclagem [replicação do SQL Server]"
  - "manipuladores de lógica de negócios [replicação do SQL Server]"
  - "classe BusinessLogicModule"
ms.assetid: edd0d17a-0e9c-4c28-8395-a7d47e8ce3d6
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Depurar um manipulador de l&#243;gica de neg&#243;cios (Programa&#231;&#227;o de replica&#231;&#227;o)
  Use um manipulador de lógica de negócios para invocar a lógica de negócios personalizada quando uma assinatura de mesclagem for sincronizada. Para obter mais informações, consulte [executar lógica de negócios durante a sincronização direta](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
 O Reconciliador de replicação de mesclagem (replrec.dll) chama o assembly de código gerenciado que contém a lógica comercial. Na maior parte dos casos, o replrec.dll e a lógica comercial personalizada são executados no computador em que o Agente de Mesclagem é executado (no Assinante para a assinatura pull ou no Distribuidor da assinatura push). Com relação à sincronização da Web ou a um Assinante [!INCLUDE[ssEW](../../includes/ssew-md.md)], o reconciliador e a lógica comercial personalizada são executados no servidor Web.  
  
### Para depurar um manipulador de lógica de negócios em um computador local  
  
1.  Configure a publicação e a distribuição, crie uma publicação e crie uma assinatura para a publicação. Para obter mais informações, consulte [Configurar publicação e distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md) e [criar, modificar e excluir publicações e artigos e 40; Replicação e 41;](../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md).  
  
2.  Crie e registre um manipulador de lógica de negócios. Para obter mais informações, consulte [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
3.  Crie um projeto RMO (Replication Management Objects) no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio, que iniciará o Agente de Mesclagem em sincronia, programaticamente. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
4.  Defina um ponto de interrupção no código do manipulador de lógica de negócios, tanto no método sendo depurado como no construtor da classe. Para obter mais informações sobre os métodos que podem ser implementados em um manipulador de lógica de negócios, consulte o <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> tópico métodos.  
  
5.  Crie o manipulador de lógica de negócios no modo de depuração e implante o assembly e o arquivo de símbolo de depuração (.pdb) no local registrado na Etapa 1.  
  
    > [!NOTE]  
    >  Para simplificar a depuração, crie uma solução única de Visual Studio .NET que contenha ambos o projeto do manipulador de lógica de negócios e o projeto que sincroniza a assinatura. Nesse caso, defina o projeto de sincronização como projeto de inicialização e configure o ambiente de compilação para implantar o assembly da lógica comercial no local registrado na Etapa 1, durante a depuração.  
  
6.  Execute a inserção, atualize ou exclua comandos de acordo com a assinatura ou banco de dados de publicação. O comando e o local da execução dependem do método que é depurado.  
  
7.  Inicie o projeto na Etapa 3, em modo de depuração, para sincronizar a assinatura.  
  
8.  Supondo que nenhum outro ponto de interrupção esteja definido e que os comandos tenham sido replicados, a execução para quando alcança o ponto de interrupção do manipulador de lógica de negócios.  
  
### Para depurar um manipulador de lógica de negócios em um servidor Web usando a sincronização da Web ou para um assinante do SQL Server Compact  
  
1.  Configure a publicação e a distribuição, crie uma publicação e crie uma assinatura pull para a publicação. A publicação deve oferecer suporte à sincronização da Web ou [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes.  
  
2.  Crie e registre um manipulador de lógica de negócios. Para obter mais informações, consulte [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
3.  Defina um ponto de interrupção no código do manipulador de lógica de negócios, tanto no método sendo depurado como no construtor da classe. Para obter mais informações sobre os métodos que podem ser implementados em um manipulador de lógica de negócios, consulte o <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> tópico métodos.  
  
4.  Crie o manipulador de lógica de negócios no modo de depuração e implante o assembly e o arquivo de símbolo de depuração (.pdb) no local registrado na Etapa 1.  
  
    > [!NOTE]  
    >  Se o manipulador de lógica de negócios falhar em criar por causa do assembly que está em uso, digite o comando `iisreset` no servidor Web, no prompt de comando do servidor Web.  
  
5.  Sincronize a assinatura com sincronização da Web ativada. Durante a sincronização, o servidor Web carrega o assembly registrado.  
  
6.  Usando o depurador do Visual Studio .NET, anexe a um dos processos seguintes no servidor Web:  
  
    -   w3wp.exe - Windows Server 2003.  
  
    -   inetinfo.exe - Windows 2000 e Windows XP.  
  
7.  No **saída** janela, verifique a depuração de saída para verificar se os símbolos do assembly registrado carregadas corretamente. Se os símbolos não estiverem carregados, confirme se o arquivo .pdb correto foi copiado na Etapa 4, e repita a Etapa 5.  
  
8.  Execute a inserção, atualize ou exclua comandos de acordo com a assinatura ou banco de dados de publicação. O comando e o local da execução dependem do método que é depurado.  
  
9. Usando o depurador do Visual Studio, anexe ao processo w3wp.exe.  
  
10. Sincronize a assinatura novamente usando a sincronização da Web.  
  
11. Supondo que nenhum outro ponto de interrupção esteja definido e que os comandos tenham sido replicados, a execução para quando alcança o ponto de interrupção do manipulador de lógica de negócios.  
  
## Consulte também  
 [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  