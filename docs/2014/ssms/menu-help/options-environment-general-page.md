---
title: Opções (ambiente – página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Environment.SQLEnvironmentOptions
ms.assetid: c32ccdb8-2cf8-4c78-b474-a3abd3dbbd13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a96b77c3f1243bc3d95cf38242463724348134b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68188509"
---
# <a name="options-environment-general-page"></a>Opções (página Ambiente-Geral)
  Use a caixa de diálogo **Opções** para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] configurar ações de inicialização, opções gerais de gerenciamento de janelas e outras configurações gerais. No menu **Ferramentas** , clique em **Opções**, expanda a pasta **Ambiente** e clique em **Geral**.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Na inicialização**  
 Selecione a ação a ser executada pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quando for iniciado. As opções são:  
  
-   **Abrir** pesquisador de objetos solicita uma conexão e, em seguida, abre o pesquisador de objetos.  
  
-   **Abrir nova janela de consulta** solicita uma conexão e, em seguida, abre o editor de consultas SQL.  
  
-   Abra o pesquisador de **objetos e a nova consulta** solicita uma conexão e, em seguida, abre o pesquisador de objetos e o editor de consultas SQL com essa conexão.  
  
-   **Abrir ambiente vazio** abre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sem uma janela do editor de consultas SQL e sem conectar o pesquisador de objetos a um servidor.  
  
 **Ocultar objetos do sistema no Pesquisador de objetos**  
 Marque essa caixa de seleção para remover os bancos de dados, tabelas e exibições do sistema e os procedimentos armazenados do sistema da exibição em árvore no Pesquisador de Objetos. As funções e tipos de dados do sistema não são ocultos. Essa opção só se aplica a instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não afeta servidores já conectados no Pesquisador de Objetos.  
  
## <a name="environment-layout"></a>Layout do Ambiente  
 Você deve fechar e reabrir o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para alternar entre os modos de ambiente de documentos com guias e de ambiente MDI.  
  
 **Documentos com guias**  
 Selecione esta opção para exibir janelas de documentos com guias em editores. Janelas de documentos com guias são úteis para organizar e alternar entre vários documentos abertos.  
  
 **Ambiente MDI**  
 Selecione esta opção para abrir documentos em um ambiente MDI. Janelas de documentos MDI são úteis para garantir o espaço na tela que, de outra forma, seria ocupado pelas guias no ambiente de documentos com guias. Ao trabalhar no modo MDI, você pode alternar entre os documentos pressionando CTRL+TAB ou usar as opções lado a lado localizadas no menu **Janela** .  
  
## <a name="docked-tool-window-behavior"></a>Comportamento da Janela de Ferramentas Encaixada  
 **O botão fechar afeta somente a guia ativa**  
 Especifica que, quando essa caixa de seleção for marcada, somente a janela de ferramentas exibida no momento será fechada e não todas as janelas de ferramentas do conjunto encaixado. Por padrão, esta caixa é selecionada.  
  
 **Ocultar Automaticamente botão afeta somente a guia ativa**  
 Especifica que, quando essa caixa de seleção for marcada, somente a janela de ferramentas exibida no momento será oculta automaticamente e não todas as janelas de ferramentas do conjunto encaixado. Por padrão, essa caixa de seleção é desmarcada.  
  
## <a name="display"></a>Exibição  
 **Exibir n arquivos na lista de usados recentemente**  
 Personaliza o número de projetos e arquivos recentes exibidos no menu **Arquivo** . Digite um número entre 1 e 24. O padrão é 4. Esse é um modo fácil de recuperar projetos de script e projetos de arquivos e script recentemente usados.  
  
  
