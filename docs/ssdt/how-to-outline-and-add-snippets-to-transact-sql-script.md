---
title: 'Como fazer: estruturar tópicos e adicionar snippets a scripts Transact-SQL | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 543e7ce7-8639-4281-8a91-85314755e5de
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c8ab757cac0622c5674bb2008b5bafbbc07c182c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035122"
---
# <a name="how-to-outline-and-add-snippets-to-transact-sql-script"></a>Como fazer: Estruturar tópicos e adicionar snippets a scripts Transact-SQL
O SQL Server Data Tools inclui uma biblioteca de códigos que consiste em snippets de código prontos para serem inseridos no seu aplicativo. Cada snippet executa uma tarefa de script completa, como a criação de uma função, tabela, gatilho, índice, exibição, tipo de dados definido pelo usuário etc. Você pode inserir um snippet em seu código-fonte com alguns cliques do mouse. Estes snippets aumentam sua produtividade reduzindo a quantidade de tempo você gasta digitando.  
  
Quando você precisa navegar para um snippet apropriado, pode usar o selecionador de snippet, que dá a você listas categorizadas de snippets para escolher. Depois de você ter adicionado o snippet a seu código, algumas partes dele podem precisar de personalização, como substituir nomes de variável por nomes mais apropriados, ou adicionar a lógica real de um procedimento armazenado. Você perceberá que o código de snippet inserido tem um ou mais pontos de substituição realçados no código para esta finalidade. Se você passar o ponteiro do mouse sobre o ponto de substituição, uma Dica de Ferramenta aparecerá para explicar como você pode alterar o código.  
  
Por padrão, todo texto é exibido no Editor Transact\-SQL, mas você pode optar por ocultar a exibição de algum código. O Editor Transact\-SQL permite selecionar uma região de código para torná-la recolhível, para que apareça sob um sinal de adição (+). Você poderá então expandir ou ocultar a região clicando no sinal de adição (+) ao lado do símbolo. O código de estrutura de tópicos não é excluído e sim apenas ocultado da exibição.  
  
> [!WARNING]  
> Os procedimentos a seguir utilizam entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-insert-snippets"></a>Para inserir snippets  
  
1.  Clique com o botão direito do mouse no projeto **TradeDev** no **Gerenciador de Soluções** e selecione **Adicionar** e depois **Script**. Na caixa de diálogo **Adicionar Novo Item**, clique em **Adicionar**.  
  
2.  Clique com o botão direito do mouse no editor Transact\-SQL e selecione **Inserir Snippet**. O selecionador de snippet de código é exibido.  
  
3.  Clique duas vezes na **Tabela** no selecionador de snippet de código e clique duas vezes em **Criar Tabela**.  
  
4.  Observe que os pontos de substituição são realçados em amarelo. Passe o mouse sobre `Sample_Table` e uma infodica exibe uma descrição da substituição. Clique duas vezes em `Sample_Table` e altere-a para `Shipper2`.  
  
5.  Use a tecla TAB para se mover para o próximo ponto de substituição que é `column_1`. Renomeie-o como `Id`. Siga as mesmas etapas para renomear `column_2` como `name` e altere seu tipo de dados como `nvarchar(128)` e permita `NULL`.  
  
### <a name="to-outline-code"></a>Para código de estrutura de tópicos  
  
1.  Observe o sinal **-** ao lado da instrução CREATE TABLE. Clique no sinal **-** ao lado de uma seção no script para ocultá-lo.  
  
2.  Clique com o botão direito do mouse no Editor Transact\-SQL e selecione **Estrutura de Tópicos** e **Interromper Estrutura de Tópicos** para remover as informações de estrutura de tópicos sem afetar seu código subjacente no editor.  
  
3.  Para iniciar a estrutura de tópicos de seu código novamente, clique com o botão direito do mouse no Editor Transact\-SQL e selecione **Estrutura de Tópicos** e **Iniciar Estrutura de Tópicos Automática**. Você também pode selecionar **Ativar/desativar estrutura de tópicos** para tudo para alternar as seções expandir/ocultar.  
  
