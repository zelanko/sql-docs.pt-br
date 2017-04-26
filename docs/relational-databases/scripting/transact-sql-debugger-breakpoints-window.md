---
title: "Janela Pontos de Interrupção | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.breakpoints
helpviewer_keywords:
- Breakpoints Window [Transact-SQL]
ms.assetid: bad88d10-fdd5-4d3d-b5ea-a4f063847485
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d2a6741dead3853b1102514f7be8ea23c42243a1
ms.lasthandoff: 04/11/2017

---
# <a name="transact-sql-debugger---breakpoints-window"></a>Depurador do Transact-SQL – Janela Pontos de Interrupção
  A janela **Pontos de Interrupção** lista todos os pontos de interrupção definidos no atual Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Para gerenciar os pontos de interrupção, use a barra de ferramentas da janela **Pontos de Interrupção** . Pontos de interrupção são locais no código onde a execução pausa no modo de depuração de forma que é possível exibir os dados de depuração.  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para acessar a janela Pontos de Interrupção**  
  
-   No menu **Depurar** , clique em **Janelas**e em **Pontos de Interrupção**.  
  
## <a name="breakpoints-window-columns"></a>Colunas da Janela Pontos de Interrupção  
 Por padrão, a janela **Pontos de interrupção** lista as colunas a seguir.  
  
 **Nome**  
 Exibe o nome do ponto de interrupção. Os nomes dos pontos de interrupção são fornecidos pelo depurador. Esse nome inclui o nome da janela do Editor de Consultas do Mecanismo do Banco de Dados que contém o ponto de interrupção e o número da linha do Editor de Consultas onde o ponto de interrupção foi configurado.  
  
 **Condição**  
 Exibe **(nenhuma condição)**. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] não dá suporte a condições de ponto de interrupção de configuração.  
  
 **Contagem de Ocorrências**  
 Exibe**sempre é interrompido**.  
  
 Você pode adicionar e remover as seguintes colunas selecionando-as na lista **Colunas** .  
  
 **Filtro**  
 Exibe **(nenhum)**. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] não dá suporte a filtros de ponto de interrupção de configuração.  
  
 **Quando Visitado**  
 Exibe **Interrupção**.  
  
 **Idioma**  
 Exibe **Transact-SQL** para [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Função**  
 Exibe o número da linha onde o ponto de interrupção está definido.  
  
 **Arquivo**  
 Exibe o nome do arquivo de origem que contém o ponto de interrupção e o número da linha na qual o ponto de interrupção está definido.  
  
 **Endereço**  
 O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] não dá suporte a este recurso.  
  
 **Processar**  
 Exibe **[SQL]** para indicar que este é um processo do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Em seguida apresenta o nome da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] na qual o código é executado.  
  
## <a name="breakpoints-window-toolbar"></a>Barra de ferramentas da janela Pontos de Interrupção  
 Quando a janela atual do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] tem pontos de interrupção ativos, a janela **Pontos de Interrupção** exibe uma barra de ferramentas que pode ser usada para gerenciar os pontos de interrupção.  
  
 **Delete (excluir)**  
 Exclui o ponto de interrupção selecionado.  
  
 **Excluir Todos os Pontos de Interrupção**  
 Exclui todos os pontos de interrupção exibidos na janela **Pontos de Interrupção** .  
  
 **Desabilitar Todos os Pontos de Interrupção**  
 Desabilita todos os pontos de interrupção de forma que eles não interrompam a execução de código; porém, os pontos de interrupção permanecem. Quando todos os pontos de interrupção estão desabilitados, este botão se transforma em **Habilitar Todos os Pontos de Interrupção**.  
  
 **Habilitar Todos os Pontos de Interrupção**  
 Habilita todos os pontos de interrupção de forma que eles interrompam a execução de código. Quando todos os pontos de interrupção estão habilitados, este botão se transforma em **Desabilitar Todos os Pontos de Interrupção**.  
  
 **Ir para Código Fonte**  
 Posiciona o cursor na linha do Editor de Consultas que contém o ponto de interrupção selecionado.  
  
 **Colunas**  
 Lista todas as colunas que podem ser exibidas na janela **Pontos de Interrupção** . Uma caixa de seleção indica as colunas em exibição. Para adicionar ou remover uma coluna na janela **Pontos de Interrupção** , selecione a coluna na lista.  
  
## <a name="see-also"></a>Consulte também  
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
