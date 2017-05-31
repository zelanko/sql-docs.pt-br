---
title: Editores de Consultas e de Texto (SQL Server Management Studio) | Microsoft Docs
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
- VS.TextEditor
helpviewer_keywords:
- Query Editor [SQL Server Management Studio]
- Code Editor [SQL Server Management Studio], about Query Editor
- Query Editor [SQL Server Management Studio], full screen mode
- Query Editor [Database Engine], templates
- full screen mode [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], templates
- writing scripts
- modifying scripts
- SQL Server Management Studio [SQL Server], query editor
- Query Editor [SQL Server Management Studio], about Query Editor
- writing queries
- SQL Server Management Studio [SQL Server], editor
- scripts [SQL Server], SQL Server Management Studio
- queries [SQL Server], SQL Server Management Studio
ms.assetid: 062051e4-4b77-4969-98ae-d2547c24ce3e
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7ff32d77b3e1503bd23e4ac0ecf040653265f141
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="query-and-text-editors-sql-server-management-studio"></a>Editores de Consultas e de Texto (SQL Server Management Studio)
  Você pode usar um dos editores do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para editar e testar interativamente um script [!INCLUDE[tsql](../../includes/tsql-md.md)], MDX, DMX ou XML/A, ou para editar um arquivo de texto XML ou sem-formatação. Cada editor tem o suporte de um serviço específico de linguagem que colore palavras-chave e verifica a sintaxe e os erros no uso. O Editor de Consultas [!INCLUDE[ssDE](../../includes/ssde-md.md)] inclui um depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] que você pode usar para ajudar a corrigir problemas em código [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
## <a name="sql-server-management-studio-editors"></a>Editores do SQL Server Management Studio  
 Os quatro editores do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] compartilham uma arquitetura comum. O editor de texto implementa o nível base da funcionalidade e pode ser usado como um editor básico para arquivos de texto. Os outros três editores ou editores de consulta estendem essa base de funcionalidade incluindo um serviço de idioma que define a sintaxe de um dos idiomas com suporte no SQL Server. Os editores de consulta também implementam vários níveis de suporte para recursos de editor, como o IntelliSense e a depuração. Os editores de consulta incluem o Editor de Consultas do Mecanismo de Banco de Dados para uso na compilação de scripts que contêm instruções Transact-SQL e XQuery, o editor MDX para a linguagem MDX, o editor DMX para a linguagem DMX e o editor XML/A para a linguagem XML for Analysis.  
  
## <a name="common-components"></a>Componentes comuns  
 Todos os editores do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] compartilham esses componentes:  
  
 **Painel de Código**  
 A área onde você digita as consultas ou o texto. Nos editores de consulta, ele contém os recursos de compilação de instrução disponíveis para sua linguagem. O ambiente de edição de texto oferece suporte à localização e substituição, aos comentários em massa, e às fontes e cores personalizadas.  
  
 Você pode definir no painel de código as opções que afetam o comportamento do texto relativas a recuo, tabulação, recurso de arrastar e soltar o texto e assim por diante. As janelas de consulta podem ser configuradas para operar como guias na janela de documentos ou em documentos separados.  
  
 **Margem de seleção**  
 Uma coluna de espaço em branco entre a barra do indicador de margem e o texto de código, onde você pode clicar para selecionar as linhas do texto. Você pode ocultar ou exibir a margem de seleção.  
  
 **Barras de rolagem horizontal e vertical**  
 Permite rolar o painel de código horizontal e verticalmente de modo que você possa exibir o código que se estende além das bordas visualizáveis do painel de código.  
  
 **Numeração de Linhas**  
 Exibe os números de linhas à esquerda do texto ou código no Editor. Você pode navegar para números de linha específicos.  
  
 **Quebra automática de linha**  
 Exibe linhas longas de texto ou código como múltiplas linhas, permitindo que você veja todo o texto da linha. A quebra automática de linha não afeta o modo como o texto aparece quando é executado ou impresso. Ela é ativada na caixa de diálogo **Ferramentas**, **Opções** , na página Editor de Texto, Todos os Idiomas, Geral, ou em uma página específica do editor.  
  
## <a name="code-editor-components"></a>Componentes do Editor de Códigos  
 Os editores de códigos contêm estes recursos, além dos compartilhados com os editores XML e de texto:  
  
 **Resultados**  
 Esta janela é usada para exibir os resultados de uma consulta. A janela pode exibir os resultados na grade ou no texto, ou os resultados poderão ser redirecionados para um arquivo. As grades de resultados podem ser exibidas como janelas com guias.  
  
 **IntelliSense**  
 Nos Editores, no menu **Editar** , aponte para **IntelliSense**para exibir as opções do [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense.  
  
 **Codificação por cores**  
 Exibe cores diferentes para cada tipo de elemento de sintaxe, o que melhora a legibilidade de instruções complexas.  
  
 **Estruturação do código**  
 Exibe grupos de códigos com linhas de estruturação à esquerda do código. Os grupos de códigos podem ser recolhidos e expandidos para facilitar o exame do código.  
  
 **Modelo**  
 Os modelos são arquivos que contêm a estrutura básica das instruções necessárias para criar objetos em um banco de dados. Eles podem ser usados para agilizar a criação de scripts.  
  
 **Mensagens**  
 Exibe erros, avisos e mensagens informativas que são retornados pelo servidor quando um script é executado. A lista de mensagens não se altera até que o script seja executado novamente.  
  
 **Barra de Status**  
 Exibe informações do sistema associadas à janela Editor de Consultas, como, por exemplo, a qual instância o Editor de Consultas está conectado.  
  
## <a name="database-engine-query-editor-components"></a>Componentes do Editor de Consultas do Mecanismo de Banco de Dados  
 Esses componentes só estão disponíveis no Editor de Consultas do Mecanismo de Banco de Dados:  
  
 **Depurador**  
 Permite pausar a execução de código em instruções específicas. Você pode exibir dados e informações do sistema para ajudar a localizar erros no código.  
  
 **Lista de Erros**  
 Exibe os erros semânticos e de sintaxe localizados pelo IntelliSense. A lista de erros é alterada de forma dinâmica à medida que você edita scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 **Plano de execução gráfico**  
 Exibe as etapas lógicas criadas no plano de execução de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 **Estatísticas do cliente**  
 Exibe informações sobre a execução da consulta agrupada em categorias. Quando a opção **Incluir Estatísticas do Cliente** é selecionada no menu **Consulta** , uma janela **Estatísticas do Cliente** é exibida na execução da consulta. São listadas estatísticas de execuções de consulta sucessivas junto com os valores médios. Selecione **Redefinir Estatísticas do Cliente** no menu **Consulta** para redefinir a média.  
  
 **Trechos de códigos**  
 Os modelos que você pode usar como ponto de partida ao adicionar instruções ao Editor de Consultas do Mecanismo de Banco de Dados. Você pode inserir os trechos predefinidos fornecidos com o SQL Server ou adicionar seus próprios trechos.  
  
 **Modo SQLCMD**  
 Executa scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] que incluem o conjunto de comandos com suporte no utilitário sqlcmd. Para saber mais, confira [Tópicos de instruções do sqlcmd](http://msdn.microsoft.com/library/dd7a2d2b-6327-4d77-ac5a-580d36073ad4).  
  
## <a name="editor-tasks"></a>Tarefas do editor  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como exibir e usar os recursos básicos do Editor de Consultas [!INCLUDE[ssDE](../../includes/ssde-md.md)] .|[Editor de Consultas do Mecanismo de Banco de Dados &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)|  
|Descreve como exibir e usar os recursos básicos do Editor de Consultas MDX.|[Editor de Consultas MDX &#40;Analysis Services - Dados Multidimensionais&#41;](http://msdn.microsoft.com/library/777f2c23-1c1c-4b72-9d19-48a4866551f8)|  
|Descreve como exibir e usar os recursos básicos do Editor de Consultas DMX.|[Editor de Consultas DMX &#40;Analysis Services – Mineração de Dados&#41;](http://msdn.microsoft.com/library/7ac877a1-0f29-46b9-9a51-73b02172bef1)|  
|Descreve como exibir e usar os recursos básicos do Editor XML/A.|[Editor XML &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/xml-editor-sql-server-management-studio.md)|  
|Descreve como configurar opções para os vários editores, como numeração de linha e opções do IntelliSense.|[Configurar editores &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-editors-sql-server-management-studio.md)|  
|Descreve os vários modos nos quais você pode abrir os editores no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].|[Abrir um editor &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/open-an-editor-sql-server-management-studio.md)|  
|Descreve como gerenciar o modo de exibição, como quebra automática de linha, divisão de uma janela ou guias.|[Gerenciar o editor e o modo de exibição](../../relational-databases/scripting/manage-the-editor-and-view-mode.md)|  
|Descreve como definir opções de formatação, como texto oculto ou recuo.|[Gerenciar formatação de código](../../relational-databases/scripting/manage-code-formatting.md)|  
|Descreve como navegar pelo texto em uma janela do editor usando recursos como pesquisa incremental ou ir para.|[Código e texto de navegação](../../relational-databases/scripting/navigate-code-and-text.md)|  
|Descreve como definir opções de codificação por cores para várias classes de sintaxe, o que facilitará a leitura de instruções complexas.|[Codificação por cores no Editor de Consultas](../../relational-databases/scripting/color-coding-in-query-editors.md)|  
|Descreve como usar a estrutura de tópicos de código para ocultar partes dos scripts complexos nos quais você não está trabalhando no momento.|[Estruturação do código](../../relational-databases/scripting/code-outlining.md)|  
|Descreve como arrastar texto de um local em um script e soltá-lo em um novo local.|[Arrastar e soltar texto](../../relational-databases/scripting/drag-and-drop-text.md)|  
|Descreve como realizar uma pesquisa global e fazer a substituição, como alterar nomes de coluna.|[Pesquisar e substituir](../../relational-databases/scripting/search-and-replace.md)|  
|Descreve como definir indicadores para localizar partes importantes de código com mais facilidade.|[Gerenciar indicadores](../../relational-databases/scripting/manage-bookmarks.md)|  
|Descreve como imprimir scripts ou resultados em uma janela ou grade.|[Imprimir código e resultados](../../relational-databases/scripting/print-code-and-results.md)|  
|Descreve como usar os recursos do sqlcmd no Editor de Consultas [!INCLUDE[ssDE](../../includes/ssde-md.md)] .|[Editar scripts SQLCMD com o Editor de Consultas](../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)|  
|Descreve como usar recursos do IntelliSense como nomes de objeto de conclusão automática à medida que os digita ou garantir que pontos de interrupção sejam colocados em locais válidos.|[IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/intellisense-sql-server-management-studio.md)|  
|Descreve como usar os trechos de códigos no Editor de Consultas [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Os trechos são modelos para instruções ou blocos geralmente usados, e podem ser personalizados ou estendidos para incluir trechos específicos de site.|[Trechos de código Transact-SQL](../../relational-databases/scripting/transact-sql-code-snippets.md)|  
|Descreve como usar o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] para percorrer informações de depuração de código e exibição, como os valores em variáveis e parâmetros.|[Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)|  
|Descreve como definir cores personalizadas para instâncias diferentes do [!INCLUDE[ssDE](../../includes/ssde-md.md)]e fazer com que essas cores sejam definidas como o plano de fundo da barra de status nas janelas do Editor de Consultas [!INCLUDE[ssDE](../../includes/ssde-md.md)] .|[Barra de status &#40;Editor de Consultas do Mecanismo de Banco de Dados&#41;](../../relational-databases/scripting/status-bar-database-engine-query-editor.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Atalhos de teclado do SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
