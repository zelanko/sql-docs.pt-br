---
title: Editor de Consultas do Mecanismo de Banco de Dados (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.tsqlquery.f1
dev_langs: TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
caps.latest.revision: "47"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 81d67f47cddfe48575758ec7ff3b5949a4c6f1f8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="database-engine-query-editor-sql-server-management-studio"></a>Editor de Consultas do Mecanismo de Banco de Dados (SQL Server Management Studio)
  Use o Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para criar e executar scripts que contenham instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] . O editor também dá suporte à execução de scripts que contêm comandos do **sqlcmd** .  
  
## <a name="transact-sql-f1-help"></a>Ajuda F1 do Transact-SQL  
 O Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] oferece suporte à vinculação ao tópico de referência de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] específica quando você seleciona F1. Para fazer isso, realce o nome de uma instrução Transact-SQL e selecione F1. O utilitário de pesquisa de ajuda procurará um tópico que tenha um atributo de ajuda F1 correspondente à cadeia de caracteres realçada.  
  
 Se o utilitário de pesquisa de ajuda não localizar um tópico com uma palavra-chave de ajuda F1 que corresponda exatamente à cadeia de caracteres realçada, esse tópico será exibido. Nesse caso, existem duas abordagens para localizar a ajuda que você está procurando:  
  
-   Copie e cole a cadeia de caracteres do editor que você realçou na guia de pesquisa dos Manuais Online do SQL Server e faça uma pesquisa.  
  
-   Realce apenas a parte da instrução Transact-SQL que provavelmente corresponderá a uma palavra-chave de ajuda F1 aplicada a um tópico e selecione F1 novamente. O utilitário de pesquisa requer uma correspondência exata entre a cadeia de caracteres realçada e uma palavra-chave de ajuda F1 atribuída a um tópico. Se a cadeia de caracteres realçada contiver elementos exclusivos ao seu ambiente, como nomes de coluna ou de parâmetro, o mecanismo de pesquisa não obterá uma correspondência. Os exemplos das cadeias de caracteres a serem realçadas incluem:  
  
    -   O nome de uma instrução Transact-SQL, como SELECT, CREATE DATABASE ou BEGIN TRANSACTION.  
  
    -   O nome de uma função interna, como SERVERPROPERTY ou @@VERSION.  
  
    -   O nome de uma tabela de procedimento armazenado do sistema, ou exibição, como sys.data_spaces ou sp_tableoption.  
  
## <a name="working-with-the-database-engine-query-editor"></a>Trabalhando com o Editor de Consultas do Mecanismo de Banco de Dados  
 O Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é um dos quatro editores implementados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter uma descrição da funcionalidade implementada no Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e as tarefas principais que você pode executar usando o editor, consulte [Editores de Consultas e de Texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
## <a name="sql-editor-toolbar"></a>Barra de ferramentas do Editor SQL  
 Quando o Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está aberto, a barra de ferramentas do Editor SQL é exibida com os botões a seguir.  
  
 **Connect**  
 Abra a caixa de diálogo **Conectar ao Servidor** . Use esta caixa de diálogo para estabelecer uma conexão a um servidor.  
  
 **Desconectar**  
 Desconecta o Editor de Consultas do servidor.  
  
 **Alterar Conexão**  
 Abra a caixa de diálogo **Conectar ao Servidor** . Use esta caixa de diálogo para estabelecer uma conexão a um servidor diferente.  
  
 **Nova Consulta com Conexão Atual**  
 Abre uma nova janela do Editor de Consultas e usa as informações de conexão da janela atual do Editor de Consultas.  
  
 **Bancos de Dados Disponíveis**  
 Alteram a conexão com um banco de dados diferente do mesmo servidor.  
  
 **Execute (executar)**  
 Executa o código selecionado ou, se nenhum código estiver selecionado, executa todo o código no Editor de Consultas.  
  
 **Depurador**  
 Habilita o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] . Este depurador dá suporte a ações de depuração, como definir pontos de interrupção, detectar variáveis e depurar através de código.  
  
 **Cancelar Consulta de Execução**  
 Envia uma solicitação de cancelamento ao servidor. Algumas consultas não podem ser canceladas imediatamente, mas precisam esperar por uma condição de cancelamento satisfatória. Quando transações são canceladas, podem ocorrer atrasos enquanto as transações são revertidas.  
  
 **Analisar**  
 Verifica a sintaxe do código selecionado. Se nenhum código estiver selecionado, esta opção verificará a sintaxe de todo o código na janela Editor de Consultas.  
  
 **Exibir Plano de Execução Estimado**  
 Solicita um plano de execução de consulta do processador de consultas sem executar realmente a consulta e exibe o plano na janela **Plano de execução** . Esse plano usa estatísticas de índice como uma estimativa do número de linhas que se espera que retornem durante cada parte da execução da consulta. O plano de consulta real que é usado pode ser diferente do plano de execução estimado. Isso pode ocorrer se o número de linhas retornadas for consideravelmente diferente da estimativa e o processador de consultas alterar o plano para torná-lo mais eficiente.  
  
 **Opções de consulta**  
 Abre a caixa de diálogo **Opções de Consulta** . Use esta caixa de diálogo para configurar as opções padrão para execução da consulta e para resultados da consulta.  
  
 **IntelliSense habilitado**  
 Especifica se a funcionalidade IntelliSense está disponível no Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 **Incluir Plano de Execução Atual**  
 Executa a consulta e retorna os resultados da consulta e o plano de execução usado para a consulta. Estes aparecem como um plano de consulta gráfica na janela **Plano de Execução** .  
  
 **Incluir Estatísticas do Cliente**  
 Inclui a janela **Estatísticas do Cliente** com estatísticas sobre a consulta e sobre os pacotes de rede, além do tempo decorrido da consulta.  
  
 **Resultados em Texto**  
 Retorna os resultados da consulta como texto na janela **Resultados** .  
  
 **Resultados em Grade**  
 Retorna os resultados da consulta como uma ou mais grades na janela **Resultados** .  
  
 **Resultados em Arquivo**  
 Quando a consulta é executada, a caixa de diálogo **Salvar Resultados** é exibida. Em **Salvar em**, selecione a pasta na qual você deseja salvar o arquivo. Em **Nome do arquivo**, digite o nome do arquivo e clique em **Salvar** para salvar os resultados da consulta como um arquivo de **Relatório** com a extensão .rpt. Para opções avançadas, clique na seta para baixo no botão **Salvar** e clique em **Salvar com Codificação**.  
  
 **Comentário de seleção**  
 Transforma a linha atual em um comentário adicionando um operador de comentário (--) no começo da linha.  
  
 **Remover comentário de seleção**  
 Transforma a linha atual em uma instrução de fonte ativa ao remover um operador de comentário (--) do começo da linha.  
  
 **Diminuir Recuo de Linha**  
 Move o texto da linha para a esquerda ao remover espaços em branco no começo da linha.  
  
 **Aumentar Recuo de Linha**  
 Move o texto da linha para a direita ao adicionar espaços em branco no começo da linha.  
  
 **Especificar Valores para Parâmetros de Modelo**  
 Abre uma caixa de diálogo que você pode usar para especificar valores para parâmetros em procedimentos e funções armazenados.  
  
 Você também pode adicionar a barra de ferramentas Editor de Consultas selecionando o menu **Exibir** , **Barras de Ferramentas**e, em seguida, **Editor SQL**. Se você adicionar a barra de ferramentas do SQL Editor quando nenhuma janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver aberta, todos os botões ficarão indisponíveis.  
  
## <a name="sql-editor-toolbar"></a>Barra de ferramentas do Editor SQL  
 Quando uma janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está aberta, você também pode adicionar a barra de ferramentas Depurar selecionando o menu **Exibir** , **Barras de Ferramentas**e, em seguida, **Depurar**. Se você adicionar a barra de ferramentas Depurar quando nenhuma janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver aberta, todos os botões ficarão indisponíveis.  
  
 **Continue**  
 Executa o código na janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] até encontrar um ponto de interrupção.  
  
 **Interromper Tudo**  
 Define o depurador para interromper todos os processos aos quais o depurador está anexado quando ocorrer uma interrupção.  
  
 **Parar Depuração**  
 Retira a janela selecionada do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] do modo de depuração e restaura o modo de execução padrão.  
  
 **Mostrar Próxima Instrução**  
 Move o cursor para a próxima instrução a ser executada.  
  
 **Depuração Completa**  
 A próxima instrução é executada. Se a próxima instrução chamar um procedimento armazenado, uma função ou um gatilho Transact-SQL, o depurador exibirá uma nova janela do **Editor de Consultas** que contém o código do módulo. A janela está no modo de depuração e a execução pausa na primeira instrução do módulo. Você pode mover-se pelo módulo, por exemplo, definindo pontos de interrupção ou percorrendo o código.  
  
 **Depuração Parcial**  
 A próxima instrução é executada. Se a instrução chamar um procedimento armazenado, uma função ou um gatilho Transact-SQL, o módulo será executado até o fim, e os resultados serão retornados ao código de chamada. Se você tiver certeza de que não há erros no módulo, poderá passar por ele. A execução pausa na instrução que segue a chamada para o módulo.  
  
 **Depuração Circular**  
 Retorna para o próximo nível de chamada mais alto (função, procedimento armazenado ou gatilho). A execução pausa na instrução que segue a chamada do procedimento armazenado, da função ou do gatilho.  
  
 **Windows**  
 Abre a janela **Ponto de Interrupção** ou a janela **Imediato** .  
  
## <a name="see-also"></a>Consulte também  
 [Atalhos de teclado do SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
