---
title: Abrir um editor (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5d654a60-d205-49d2-a831-b3d986d60024
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 561ddee283355b308e58cd5e0aa5eb66c29b1c47
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="open-an-editor-sql-server-management-studio"></a>Abrir um editor (SQL Server Management Studio)
  Este tópico descreve como abrir o editor [!INCLUDE[ssDE](../../includes/ssde-md.md)] Query, MDX, DMX ou XML/A no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Quando aberta, cada janela de editor aparece como uma guia no painel central do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="before-you-begin"></a>Antes de começar  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] dá suporte a quatro editores: o Editor de Consulta do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para editar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , os editores DMX e MDX para editar scripts que usam essas linguagens e o editor XML/A para editar scripts XML/A ou arquivos XML. Quaisquer dos editores também podem ser usados para editar arquivos de texto.  
  
### <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Se você compartilhar arquivos com usuários em outros locais que usam páginas de código distintas, salve o arquivo com a página de código Unicode apropriada para evitar erros na leitura do arquivo. Além disso, ao salvar arquivos para UNIX ou Macintosh, verifique se salvou seus arquivos no formato de documento apropriado. No menu **Arquivo** , clique em **Salvar Como**, **Salvar com Codificação** na seta para baixo próxima ao botão **Salvar** e escolha **Unix** ou **Macintosh** em **Terminações de Linha**.  
  
### <a name="permissions"></a>Permissões  
 Operações que você executa em um editor de códigos estão sujeitas às permissões concedidas à conta de autenticação usada no logon. Por exemplo, se você abrir uma janela Editor de Consulta [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando a Autenticação do Windows, não poderá executar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que referenciam objetos os quais sua conta de logon do Windows não tem permissões para acessar.  
  
## <a name="how-to-open-editors"></a>Como abrir editores  
 Esta seção explica como abrir os vários editores no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="using-the-filenew-menu"></a>Usando o menu Arquivo/novo  
 No menu **Arquivo** , clique em **Novo**e selecione uma das opções do editor de consulta:  
  
-   **Consulta com Conexão Atual** – Abre uma nova janela do editor do tipo associado à conexão atual janela atual no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. A janela de editor usa as mesmas informações de autenticação que a conexão atual. Por exemplo, se você selecionar uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em Pesquisador de Objetos, e usar **Consulta com Conexão Atual**, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] abrirá um Editor de Consultas [!INCLUDE[ssDE](../../includes/ssde-md.md)] conectado à mesma instância usando as mesmas informações de autenticação.  
  
-   **Consulta do Mecanismo de Banco de Dados** – Abre um novo Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e uma caixa de diálogo para obter as informações necessárias para se conectar a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   **Consulta MDX do Analysis Services** – Abre um novo Editor de Consultas MDX do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e uma caixa de diálogo para obter as informações necessárias para se conectar a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   **Consulta DMX do Analysis Services** – Abre um novo Editor de Consultas DMX do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e uma caixa de diálogo para obter as informações necessárias para se conectar a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   **Consulta XML/A do Analysis Services** – Abre um novo Editor de Consultas XML/A do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e uma caixa de diálogo para obter as informações necessárias para se conectar a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="using-the-fileopen-menu"></a>Usando o menu Arquivo/Abrir  
 No menu **Arquivo** , clique em **Abrir**, navegue até um arquivo e abra-o. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] abre o tipo apropriado de editor para a extensão de arquivo, copia o conteúdo do arquivo na janela de editor e também abre uma caixa de diálogo de conexão, se necessário. Por exemplo, se você abrir um arquivo com extensão .sql, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] abrirá uma janela de Editor de Consulta [!INCLUDE[ssDE](../../includes/ssde-md.md)] , copiará o conteúdo do arquivo .sql e abrirá uma caixa de diálogo de conexão. Se você abrir um arquivo com uma extensão não associada a um editor específico, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] abrirá a janela do editor e copiará o conteúdo do arquivo.  
  
 Para obter mais informações, veja [Associar extensões de arquivo a um Editor de Códigos](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md).  
  
### <a name="using-the-toolbar"></a>Usando a barra de ferramentas  
 Na barra de ferramentas **Padrão** , clique em um dos seguintes botões:  
  
-   **Nova Consulta** – Abre uma nova janela do editor do tipo associado à conexão atual janela atual no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. A janela de editor usa as mesmas informações de autenticação que a conexão atual. Por exemplo, se você selecionar uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em Pesquisador de Objetos, e clicar no botão **Nova Consulta** , o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] abrirá um Editor de Consulta [!INCLUDE[ssDE](../../includes/ssde-md.md)] conectado à mesma instância usando as mesmas informações de autenticação.  
  
-   **Consulta do Mecanismo de Banco de Dados** – Abre um novo Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e uma caixa de diálogo para obter as informações necessárias para se conectar a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   **Consulta MDX do Analysis Services** – Abre um novo Editor de Consultas MDX do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e uma caixa de diálogo para obter as informações necessárias para se conectar a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   **Consulta DMX do Analysis Services** – Abre um novo Editor de Consultas DMX do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e uma caixa de diálogo para obter as informações necessárias para se conectar a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   **Consulta XML/A do Analysis Services** – Abre um novo Editor de Consultas XML/A do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e uma caixa de diálogo para obter as informações necessárias para se conectar a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="using-object-explorer"></a>Usando o Pesquisador de Objetos  
 No **Pesquisador de Objetos**:  
  
-   Clique com o botão direito do mouse no nó de servidor conectado a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]e selecione **Nova Consulta**. Isso abrirá uma janela Editor de Consulta [!INCLUDE[ssDE](../../includes/ssde-md.md)] conectada à mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e definirá o contexto de banco de dados da janela para o banco de dados padrão para o logon.  
  
-   Clique com o botão direito do mouse em um nó de banco de dados e selecione **Nova Consulta**. Isso abrirá uma janela Editor de Consulta [!INCLUDE[ssDE](../../includes/ssde-md.md)] conectada à mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e definirá o contexto de banco de dados da janela para o mesmo banco de dados.  
  
### <a name="using-solution-explorer"></a>Usando o Gerenciador de Soluções  
 No **Gerenciador de Soluções**, expanda uma pasta, clique com o botão direito do mouse em um item dentro da pasta e clique em **Abrir** ou clique duas vezes no item ou arquivo.  
  
### <a name="using-template-browser-to-open-the-database-engine-query-editor"></a>Usando o Gerenciador de Modelos para abrir o Editor de Consultas do Mecanismo de Banco de Dados  
  
-   No menu **Exibir** , clique em **Gerenciador de Modelos**.  
  
-   A janela **Gerenciador de Modelos** aparece no painel direito.  
  
-   Clique duas vezes em um modelo para abrir uma janela de Consulta do Mecanismo de Banco de Dados com o texto do modelo. Por exemplo, para abrir um modelo CREATE DATABASE, abra a pasta **Modelos do SQL Server** , abra a pasta **Bancos de Dados** e clique duas vezes em **criar banco de dados**.  
  
  
