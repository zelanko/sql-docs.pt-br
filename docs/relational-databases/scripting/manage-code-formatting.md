---
title: "Gerenciar a formatação de código | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indenting code [SQL Server]
- displaying URLs
- code formatting [SQL Server Management Studio]
- collapsing text
- formats [SQL Server], code formatting in SQL Server Management Studio
- hiding text
- formats [SQL Server]
- text [SQL Server], code formats
- automatic indentation
- converting text to lower case
- Query Editor [SQL Server Management Studio], managing code formats
- URL displayed in code [SQL Server Management Studio]
- converting text to upper case
- text [SQL Server]
- unindenting code
ms.assetid: ddbac4d2-6bdc-4467-a352-e869ec880eed
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 96141b7eb166d6ffd8e082890ce005a0cc52c650
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="manage-code-formatting"></a>Gerenciar formatação de código
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Com o Editor, você pode formatar seu código com recuo, texto oculto, URLs, etc. Você também pode formatar o código automaticamente usando o Recuo Inteligente.  
  
## <a name="indenting"></a>Recuo  
 Você pode escolher três estilos diferentes de recuo de texto. Você também pode especificar quantos espaços compõem um único recuo ou tabulação e se o editor usa tabulações ou caracteres de espaço quando estabelece o recuo.  
  
#### <a name="to-choose-an-indenting-style"></a>Para escolher um estilo de recuo  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Clique em **Editor de Texto**.  
  
3.  Clique na pasta e selecione **Todos os Idiomas** para definir o recuo para todos os idiomas.  
  
4.  Clique em **Tabulações**.  
  
5.  Clique em uma das opções a seguir:  
  
    -   **None**. O cursor vai para o começo da próxima linha.  
  
    -   **Bloquear**. O cursor alinha a próxima linha com a linha anterior.  
  
    -   **Inteligente** (Padrão). O serviço de idiomas determina o estilo do recuo adequado.  
  
    > [!NOTE]  
    >  Alguns idiomas não oferecem as três opções de recuo.  
  
#### <a name="to-change-indent-tab-settings"></a>Para alterar configurações tabulação de recuo  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Clique em **Editor de Texto**.  
  
3.  Selecione a pasta de **Todos os Idiomas** para definir recuo para todos os idiomas.  
  
4.  Clique em **Tabulações**.  
  
5.  Para especificar caracteres de tabulação para operações de recuo e tabulação, clique em **Manter tabulações**. Para especificar caracteres de espaço, selecione **Inserir espaços**.  
  
     Se você selecionar **Inserir espaços**, digite o número de caracteres de espaço que cada tabulação ou recuo representa em **Tamanho da Tabulação** ou **Tamanho do Recuo**, respectivamente.  
  
#### <a name="to-indent-code"></a>Para recuar código  
  
1.  Selecione o texto que você deseja recuar.  
  
2.  Pressione TAB ou clique no botão **Recuar** na barra de ferramentas Padrão.  
  
#### <a name="to-unindent-code"></a>Para remover o recuo de código  
  
1.  Selecione o texto em que você deseja remover o recuo.  
  
2.  Pressione SHIFT+TAB ou clique no botão **Desfazer recuo** na barra de ferramentas Padrão.  
  
#### <a name="to-automatically-indent-all-of-your-code"></a>Para recuar todo o código automaticamente  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Clique em **Editor de Texto**.  
  
3.  Clique em **Todos os Idiomas**.  
  
4.  Clique em **Tabulações**.  
  
5.  Clique em **Inteligente**.  
  
> [!NOTE]  
>  A opção **Inteligente** não está disponível para alguns idiomas.  
  
#### <a name="to-convert-white-space-to-tabs"></a>Para converter espaços vazios em tabulações  
  
1.  Selecione o texto cujo espaço em branco que você deseja converter em tabulações.  
  
2.  No menu **Editar** , aponte para **Avançado**e clique em **Tabular Seleção**.  
  
#### <a name="to-convert-tabs-to-spaces"></a>Para converter tabulações em espaços  
  
1.  Selecione o texto cujas tabulações você deseja converter em espaços.  
  
2.  No menu **Editar** , aponte para **Avançado**e clique em **Destabular Seleção**.  
  
 O comportamento desses comandos depende das configurações de tabulação da caixa de diálogo **Opções** . Por exemplo, se a configuração de tabulação for 4, **Tabular Seleção** criará uma tabulação a cada 4 espaços contíguos e **Destabular Seleção** criará 4 espaços a cada tabulação.  
  
## <a name="converting-text-to-upper-and-lower-case"></a>Convertendo texto em maiúsculas ou minúsculas  
 Você pode usar comandos para converter texto em maiúsculas ou minúsculas.  
  
#### <a name="to-switch-text-to-upper-or-lower-case"></a>Para alternar texto entre maiúsculas ou minúsculas  
  
1.  Selecione o texto que você deseja converter.  
  
2.  Para converter texto para maiúsculas, pressione CTRL+SHIFT+U ou clique em **Colocar em Maiúsculas** no submenu **Avançado** no menu **Editar** .  
  
3.  Para converter texto para maiúsculas, pressione CTRL+SHIFT+L ou clique em **Colocar em Minúsculas** no submenu **Avançado** no menu **Editar** .  
  
> [!NOTE]  
>  Para obter uma lista completa de teclas de atalho do teclado, consulte [Atalhos de teclado do SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
## <a name="displaying-and-linking-to-urls"></a>Exibindo e vinculando a URLs  
 Você pode criar e exibir URLs clicáveis em seu código. Por padrão, as URLs:  
  
-   São sublinhadas.  
  
-   Mudam o ponteiro de mouse para uma mão quando você passa por cima delas.  
  
-   Abrem a URL quando clicada, se a URL é válida.  
  
#### <a name="to-display-a-clickable-url"></a>Para exibir uma URL clicável  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Clique em **Editor de Texto**.  
  
3.  Para alterar a opção para apenas um idioma, clique nessa pasta do idioma e clique em **Geral**. Para alterar a opção para todos os idiomas, clique em **Todos os Idiomas** e clique em **Geral**.  
  
4.  Selecione **Habilitar navegação de URL com um só clique**.  
  
  
