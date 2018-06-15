---
title: Janela Lista de Erros (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ErrorList
dev_langs:
- TSQL
helpviewer_keywords:
- error list window
- SQL Server Management Studio [SQL Server], error list window
ms.assetid: fae6327d-e268-44ae-a474-4a8f8f843129
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b040b01371c7264784ad568e75d7f01a4c7fa9da
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34334337"
---
# <a name="transact-sql-debugger---error-list-window"></a>Depurador do Transact-SQL – Janela Lista de Erros
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  A [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Error List** displays the syntax and semantic errors that are generated from the IntelliSense code in the [!INCLUDE[ssDE](../../includes/ssde-md.md)] Query Editor.  
  
## <a name="features-of-the-error-list"></a>Recursos da Lista de Erros  
 A **Lista de Erros** fornece a seguinte funcionalidade:  
  
-   À medida que os scripts são editados, a **Lista de Erros** exibe os erros e avisos gerados pelo IntelliSense no Editor de Consultas [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
-   Você pode clicar duas vezes em qualquer entrada de mensagem de erro para se concentrar na guia do arquivo de script que gerou o erro e mover-se até o local do erro.  
  
-   É possível filtrar quais entradas você quer exibir e quais colunas de informações quer que apareçam para cada entrada.  
  
-   Depois que você corrigir um erro, a entrada com erro será removida da **Lista de Erros**.  
  
-   Quando você fecha a guia para um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] , os erros desse arquivo são removidos da **Lista de Erros**.  
  
## <a name="working-with-the-error-list"></a>Trabalhando com a Lista de Erros  
 Para exibir a **Lista de Erros**, execute um destes procedimentos:  
  
-   No menu **Exibir** , clique em **Lista de Erros**.  
  
-   Insira o atalho de teclado CTRL+\\, CTRL+E.  
  
 Depois de abrir a **Lista de Erros**, você poderá personalizar sua exibição executando as seguintes ações:  
  
-   Para classificar a lista, clique em qualquer cabeçalho de coluna. Para classificar novamente por uma coluna adicional, pressione e segure a tecla SHIFT e clique em outro cabeçalho de coluna.  
  
-   Para selecionar as colunas a serem exibidas e ocultadas, selecione **Mostrar Colunas** no menu de atalho.  
  
-   Para alterar a ordem na qual as colunas são exibidas, arraste qualquer cabeçalho de coluna para a esquerda ou para a direita.  
  
 A **Lista de Erros** não está vinculada a informações adicionais sobre erros específicos.  
  
## <a name="transact-sql-errors-in-management-studio"></a>Erros de Transact-SQL no Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] exibe erros de scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] nos seguintes locais:  
  
-   A **Lista de Erros** contém todos os erros de sintaxe e semântica encontrados pelo IntelliSense no Editor do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Essa lista de erros é atualizada dinamicamente a medida que você edita scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] . A lista inclui todos os erros que o editor encontrou em cada script [!INCLUDE[tsql](../../includes/tsql-md.md)] . O editor não interrompe a análise de um arquivo após encontrar erros em um script. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o IntelliSense do Editor [!INCLUDE[ssDE](../../includes/ssde-md.md)] não dá suporte a todos os elementos de sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] . A **Lista de Erros** contém somente erros de sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] que tem suporte no IntelliSense.  
  
-   A guia **Mensagens** na parte inferior da janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] exibe todos os erros e mensagens retornados pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] quando um script [!INCLUDE[tsql](../../includes/tsql-md.md)] é executado. Essa lista não muda até que você execute o script novamente. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] interrompe a análise de um lote após encontrar um ou dois erros de compilação; dessa forma, a guia **Mensagens** pode não listar todos os erros de um script.  
  
 Às vezes são listados erros em ambos os locais. Por exemplo, um arquivo de script poderia ter um erro de sintaxe exibido na **Lista de Erros**. Se você executar o script antes de corrigir o erro, o analisador do [!INCLUDE[ssDE](../../includes/ssde-md.md)] poderá detectar a mesma condição e retornar outra cópia da mensagem de erro na guia **Mensagens** .  
  
> [!NOTE]  
>  A **Lista de Erros** exibe somente os erros do Editor de Consulta do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ; ela não exibe erros de editores MDX, DMX ou XML/A. Todos os erros de MDX, DMX e XML/A são exibidos na guia **Mensagens** desses editores.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 Quando a **Lista de Erros** estiver aberta, as informações serão exibidas nas seguintes colunas:  
  
 **Ordem Padrão**  
 Exibe um inteiro que indica a ordem na qual uma entrada foi gerada.  
  
 **Descrição**  
 Exibe o texto da entrada de erro. As descrições longas se acomodam em linhas adicionais.  
  
 **Arquivo**  
 Exibe o nome do arquivo de script que gerou o erro.  
  
 **Linha**  
 Exibe um inteiro que indica qual linha do código inclui o erro.  
  
 **Coluna**  
 Exibe um inteiro que indica a posição do erro linha na linha do código.  
  
 **Projeto**  
 Exibe o nome do projeto que inclui o arquivo de script.  
  
  
