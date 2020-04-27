---
title: Construir projetos de banco de dados usando o SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], database projects
- database projects [SQL Server]
- projects [SQL Server Management Studio], about projects
- projects [SQL Server Management Studio]
ms.assetid: c2e80045-894d-44cf-b65c-e547ed738947
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 134ac290601e463063f78a59ea8fd5923d095663
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211263"
---
# <a name="build-database-projects-by-using-sql-server-management-studio"></a>Construir projetos de banco de dados usando o SQL Server Management Studio
  Um projeto de script de banco de dados é um conjunto organizado de scripts, informações de conexão e modelos que são todos associados a um banco de dados ou a uma parte de um banco de dados. O [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para administrar e criar bancos de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no contexto de um projeto de script. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] inclui os designers, editores, guias e assistentes para ajudar os usuários a desenvolver, implantar e manter bancos de dados.  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] é um pacote de ferramentas administrativas para gerenciar os componentes que pertencem ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Esse ambiente integrado permite aos usuários executar uma variedade de tarefas, como backup de dados, edição de consultas e automação de funções comuns dentro de uma única interface.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] inclui as seguintes ferramentas:  
  
-   O Editor de Códigos é um editor de script avançado para escrever e editar scripts. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] fornece quatro versões do Editor de Códigos: o Editor de Consultas [!INCLUDE[ssDE](../includes/ssde-md.md)] para scripts [!INCLUDE[tsql](../includes/tsql-md.md)] , o Editor de Consultas DMX, o Editor de Consultas MDX e o Editor de Consultas XML/A.  
  
-   O Pesquisador de Objetos para localizar, modificar, criar scripts ou executar objetos que pertençam a instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Explorador de Modelos, para localizar e gerar scripts de modelos.  
  
-   Gerenciador de Soluções, para organizar e armazenar scripts relacionados como partes de um projeto.  
  
-   Janela Propriedades, para exibir as propriedades atuais de objetos selecionados.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] dá suporte a processos de trabalho eficientes, fornecendo:  
  
-   Acesso desconectado. Você pode escrever e editar scripts sem conectar-se a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Scripts em qualquer caixa de diálogo. Você pode criar um script em qualquer caixa de diálogo, o que lhe permite ler, modificar, armazenar e reutilizar os scripts depois de criá-los.  
  
-   Caixas de diálogo não restritas. Ao acessar uma caixa de diálogo de UI, você pode consultar outros recursos do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] sem fechar a caixa de diálogo.  
  
## <a name="solutions-and-script-projects"></a>Soluções e Projetos de Script  
 O Gerenciador de Soluções é um utilitário para armazenar e reabrir soluções de banco de dados. As soluções permitem organizar projetos e arquivos de script relacionados. Os projetos de script armazenam arquivos de script, modelos SQL, informações de conexão e vários outros arquivos de informações do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Quando um script é salvo em um projeto de script, os usuários podem:  
  
-   Manter controle de versão em scripts.  
  
-   Armazenar opções de resultados com um script.  
  
-   Organizar scripts relacionados em um único projeto de script.  
  
-   Salvar informações de conexão com scripts.  
  
 O Gerenciador de Soluções é uma ferramenta para desenvolvedores que criam e reutilizam scripts relacionados ao mesmo projeto. Se uma tarefa semelhante for necessária posteriormente, você poderá usar um grupo de scripts que foram armazenados em um projeto. Caso já tenha criado aplicativos usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], verá que o Gerenciador de Soluções é bem familiar.  
  
 Uma solução consiste em um ou mais projetos de script. Um projeto consiste em um ou mais scripts ou conexões. Um projeto também pode incluir arquivos não script.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)   
 [Editores de consulta e de texto &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [Soluções &#40;SQL Server Management Studio&#41;](solution/solutions-sql-server-management-studio.md)  
  
  
