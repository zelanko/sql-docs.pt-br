---
title: 'Opções (Editor de texto: página guia Editor e barra de Status) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.editorcontextsettings
- VS.ToolsOptionsPages.Text_Editor.EditorTabAndStatusBar
ms.assetid: e4815678-7885-4631-878f-c6a2b857ee05
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 241a74861a7f634389324276daf9b03a8590e64d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055446"
---
# <a name="options-text-editor-editor-tab-and-status-bar-page"></a>Opções (Editor de Texto: página Guia Editor e Barra de Status)
  A **página Guia Editor e Barra de Status** permite que você personalize as informações exibidas pelos Editores de Consultas do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] . Você pode especificar o nível de informações exibido na guia e na barra de status da janela Editor de Consulta e se a barra de status será exibida na parte superior ou parte inferior da janela do editor.  
  
## <a name="option-settings-by-editor"></a>Configurações de opção por editor  
 A guia Editor e a barra de status estão disponíveis em todos os editores do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , mas possuem níveis diferentes de funcionalidades.  
  
 O Editor de Consultas do Mecanismo de Banco de Dados pode se conectar a um grupo de servidores e, nesse caso, ele estabelece conexões com todas as instâncias no Grupo de Servidores e pode executar a mesma consulta simultaneamente em cada conexão. Você pode usar essa caixa de diálogo para especificar que a barra de status tenha cores diferentes quando estiver conectada a várias instâncias, em vez de a uma instância. Para alterar as opções de resultados de multisservidor, use a página [Opções (Resultados da consulta/SQL Server/Multisservidor)](../../2014/database-engine/options-query-results-sql-server-multi-server.md) .  
  
## <a name="status-bar-content"></a>Conteúdo da barra de status  
 Especifica as informações que aparecem na barra de status do Editor de Consultas.  
  
 **Exibir tempo de execução**  
 Inclui a hora de execução do script. As configurações são as seguintes:  
  
 **Nenhuma**  
 A barra de status não exibe nenhuma informação de hora.  
  
 **final**  
 A barra de status exibe a hora atual enquanto o script está em execução. Quando o script é concluído, o vídeo exibe a hora em que o script foi concluído.  
  
 **Decorrido**  
 A barra de status exibe o período de tempo que o script esteve em execução. Quando o script é concluído, o vídeo exibe o período de temo gasto na execução do script.  
  
 **Incluir nome do banco de dados**  
 Inclui o nome do banco de dados atual para a conexão. Quando o editor de consultas é aberto pela primeira vez, esse é o banco de dados padrão para o logon. O contexto do banco de dados pode ser alterado posteriormente com a instrução USE do Transact-SQL.  
  
 **Incluir nome de logon**  
 Inclui o nome de logon.  
  
 **Incluir contagem de linhas**  
 Inclui uma contagem das linhas que foram processadas pelo script atualmente em execução.  
  
 **Incluir nome do servidor**  
 Inclui o nome do servidor. Para conexões locais, esse é o nome da instância. Para conexões remotas, esse é o nome do computador remoto e o nome da instância.  
  
## <a name="status-bar-layout-and-colors"></a>Layout e cores da barra de status  
 Especifica as cores dos itens na barra de status do Editor de Consultas.  
  
 **Conexões de grupo**  
 Define a cor da barra de status para quando o Editor de Consultas tiver mais de uma conexão.  
  
 **Conexões de servidor único**  
 Define a cor da barra de status para quando o Editor de Consultas tiver uma única conexão.  
  
 **Local da barra de status**  
 Especifica o local da barra de status. As configurações são as seguintes:  
  
 **Top**  
 A barra de status aparece na parte superior do Editor de Consultas.  
  
 **parte inferior**  
 A barra de status aparece na parte inferior da janela do Editor de Consultas.  
  
## <a name="tab-text"></a>Texto da Guia  
 Especifica o texto exibido na guia, na parte superior de uma janela Editor de Consultas. Se o texto for muito longo para ser exibido, você poderá visualizar toda a cadeia de caracteres em uma dica de ferramenta que é exibida quando você passa o mouse sobre a guia.  
  
 **Incluir nome do banco de dados**  
 Inclui o nome do banco de dados atual para a conexão. Quando o editor de consultas é aberto pela primeira vez, esse é o banco de dados padrão para o logon. O contexto do banco de dados pode ser alterado posteriormente com a instrução USE do Transact-SQL.  
  
 **Incluir nome do arquivo**  
 Inclui o nome do arquivo no qual o script está armazenado.  
  
 **Incluir nome da pasta**  
 Inclui o caminho da pasta na qual o arquivo de script está armazenado.  
  
 **Incluir nome de logon**  
 Inclui o nome de logon.  
  
 **Incluir nome do servidor**  
 Inclui o nome do servidor. Para conexões locais, esse é o nome da instância. Para conexões remotas, esse é o nome do computador remoto e o nome da instância.  
  
## <a name="see-also"></a>Consulte também  
 [Opções de &#40;ambiente: Fonts and Colors Page&#41;](../ssms/menu-help/options-environment-fonts-and-colors-page.md)   
 [Codificação por cores nos Editores de Consulta](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
