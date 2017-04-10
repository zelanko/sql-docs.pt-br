---
title: "Gerenciar formata&#231;&#227;o de c&#243;digo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "recuando código [SQL Server]"
  - "exibindo URLs"
  - "formatação de código [SQL Server Management Studio]"
  - "recolhendo texto "
  - "formatos [SQL Server], formatação de código no SQL Server Management Studio"
  - "ocultando texto"
  - "formatos [SQL Server]"
  - "texto [SQL Server], formatos de código"
  - "recuo automático"
  - "convertendo texto para minúscula"
  - "Editor de Consulta [SQL Server Management Studio], gerenciando formatos de código"
  - "URL exibida em código [SQL Server Management Studio]"
  - "convertendo texto para maiúscula"
  - "texto [SQL Server]"
  - "expandindo código"
ms.assetid: ddbac4d2-6bdc-4467-a352-e869ec880eed
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Gerenciar formata&#231;&#227;o de c&#243;digo
  Com o Editor, você pode formatar seu código com recuo, texto oculto, URLs etc. Você também pode formatar o código automaticamente usando o Recuo Inteligente.  
  
## Recuo  
 Você pode escolher três estilos diferentes de recuo de texto. Você também pode especificar quantos espaços compõem um único recuo ou tabulação e se o editor usa tabulações ou caracteres de espaço quando estabelece o recuo.  
  
#### Para escolher um estilo de recuo  
  
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
  
#### Para alterar configurações tabulação de recuo  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Clique em **Editor de Texto**.  
  
3.  Selecione a pasta de **Todos os Idiomas** para definir recuo para todos os idiomas.  
  
4.  Clique em **Tabulações**.  
  
5.  Para especificar caracteres de tabulação para operações de recuo e tabulação, clique em **Manter tabulações**. Para especificar caracteres de espaço, selecione **Inserir espaços**.  
  
     Se você selecionar **Inserir espaços**, digite o número de caracteres de espaço que cada tabulação ou recuo representa em **Tamanho da Tabulação** ou **Tamanho do Recuo**, respectivamente.  
  
#### Para recuar código  
  
1.  Selecione o texto que você deseja recuar.  
  
2.  Pressione TAB ou clique no botão **Recuar** na barra de ferramentas Padrão.  
  
#### Para remover o recuo de código  
  
1.  Selecione o texto em que você deseja remover o recuo.  
  
2.  Pressione SHIFT+TAB ou clique no botão **Desfazer recuo** na barra de ferramentas Padrão.  
  
#### Para recuar todo o código automaticamente  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Clique em **Editor de Texto**.  
  
3.  Clique em **Todos os Idiomas**.  
  
4.  Clique em **Tabulações**.  
  
5.  Clique em **Inteligente**.  
  
> [!NOTE]  
>  A opção **Inteligente** não está disponível para alguns idiomas.  
  
#### Para converter espaços vazios em tabulações  
  
1.  Selecione o texto cujo espaço em branco que você deseja converter em tabulações.  
  
2.  No menu **Editar**, aponte para **Avançado** e clique em **Tabular Seleção**.  
  
#### Para converter tabulações em espaços  
  
1.  Selecione o texto cujas tabulações você deseja converter em espaços.  
  
2.  No menu **Editar**, aponte para **Avançado** e clique em **Destabular Seleção**.  
  
 O comportamento desses comandos depende das configurações de tabulação da caixa de diálogo **Opções**. Por exemplo, se a configuração de tabulação for 4, **Tabular Seleção** criará uma tabulação a cada 4 espaços contíguos e **Destabular Seleção** criará 4 espaços a cada tabulação.  
  
## Convertendo texto em maiúsculas ou minúsculas  
 Você pode usar comandos para converter texto em maiúsculas ou minúsculas.  
  
#### Para alternar texto entre maiúsculas ou minúsculas  
  
1.  Selecione o texto que você deseja converter.  
  
2.  Para converter texto para maiúsculas, pressione CTRL+SHIFT+U ou clique em **Colocar em Maiúsculas** no submenu **Avançado** no menu **Editar**.  
  
3.  Para converter texto para maiúsculas, pressione CTRL+SHIFT+L ou clique em **Colocar em Minúsculas** no submenu **Avançado** no menu **Editar**.  
  
> [!NOTE]  
>  Para obter uma lista completa de teclas de atalho do teclado, consulte [Atalhos de teclado do SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
## Exibindo e vinculando a URLs  
 Você pode criar e exibir URLs clicáveis em seu código. Por padrão, as URLs:  
  
-   São sublinhadas.  
  
-   Mudam o ponteiro de mouse para uma mão quando você passa por cima delas.  
  
-   Abrem a URL quando clicada, se a URL é válida.  
  
#### Para exibir uma URL clicável  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Clique em **Editor de Texto**.  
  
3.  Para alterar a opção para apenas um idioma, clique nessa pasta do idioma e clique em **Geral**. Para alterar a opção para todos os idiomas, clique em **Todos os Idiomas** e clique em **Geral**.  
  
4.  Selecione **Habilitar navegação de URL com um só clique**.  
  
  