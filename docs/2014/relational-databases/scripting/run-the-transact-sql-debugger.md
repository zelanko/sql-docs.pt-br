---
title: Executar o depurador Transact-SQL
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, sysadmin requirement
- Transact-SQL debugger, supported versions
- Query Editor [Database Engine], right-click menu
- Transact-SQL debugger, Query Editor shortcut menu
- Transact-SQL debugger, stopping
- Transact-SQL debugger, Debug menu
- Transact-SQL debugger, Debug toolbar
- Transact-SQL debugger, keyboard shortcuts
- Transact-SQL debugger, starting
ms.assetid: 386f6d09-dbec-4dc7-9e8a-cd9a4a50168c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9dd0dc621b0d799398098cea6fb614d5021e6016
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703748"
---
# <a name="run-the-transact-sql-debugger"></a>Executar o depurador Transact-SQL
  Você pode iniciar o depurador do [!INCLUDE[tsql](../../includes/tsql-md.md)] depois de abrir uma janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Em seguida, você pode executar seu código [!INCLUDE[tsql](../../includes/tsql-md.md)] em modo de depuração até parar o depurador. Você pode definir opções para personalizar como o depurador é executado.  
  
## <a name="starting-and-stopping-the-debugger"></a>Iniciando e parando o depurador  
 Os requisitos para iniciar o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] são os seguintes:  
  
-   Se seu Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver conectado a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em outro computador, você deverá ter configurado o depurador para depuração remota. Para obter mais informações, consulte [Configurar o depurador Transact-SQL](configure-firewall-rules-before-running-the-tsql-debugger.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] deve estar sendo executado sob uma conta do Windows que seja membro da função de servidor fixa sysadmin.  
  
-   A janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve ser conectada usando um logon de Autenticação do Windows ou Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seja um membro da função de servidor fixa sysadmin.  
  
-   A janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve estar conectada a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 (SP2) ou posterior. Não é possível executar o depurador quando a janela do Editor de Consultas está conectada a uma instância que está no modo de usuário único.  
  
 É recomendável que o código [!INCLUDE[tsql](../../includes/tsql-md.md)] seja depurado em um servidor de teste, não em um servidor de produção, pelas seguintes razões:  
  
-   A depuração é uma operação altamente privilegiada. Portanto, somente membros da função de servidor fixa sysadmin estão autorizados a depurar no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   As sessões de depuração frequentemente são executadas por longos períodos de tempo enquanto você investiga as operações de várias instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] . Os bloqueios adquiridos pela sessão, como os bloqueios de atualização, podem ser mantidos por longos períodos até que a sessão seja encerrada ou a transação confirmada ou revertida.  
  
 Quando o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] é iniciado, a janela do Editor de Consultas é colocada em modo de depuração. Quando a janela do Editor de Consultas entra em modo de depuração, o depurador faz uma pausa na primeira linha de código. Nesse ponto, você pode avançar passo a passo pelo código, fazendo pausas de execução em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] específicas, e usar as janelas do depurador para exibir o estado atual de execução. Você pode iniciar o depurador com um clique no botão **Depurar** da barra de ferramentas **Consulta** ou em **Iniciar Depuração** no menu **Depurar** .  
  
 A janela do Editor de Consultas permanece em modo de depuração até que a última instrução na janela do Editor de Consultas seja concluída ou você pare o modo de depuração. Você pode parar o modo de depuração e a execução de instruções por meio de um dos seguintes métodos:  
  
-   No menu **Depurar** , clique em **Parar Depuração**.  
  
-   Na barra de ferramentas **Depurar** , clique no botão **Parar Depuração** .  
  
-   No menu **Consulta** , clique em **Cancelar Execução de Consulta**.  
  
-   Na barra de ferramentas **Consulta** , clique no botão **Cancelar Execução de Consulta** .  
  
 Também é possível parar o modo de depuração e permitir que as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] restantes sejam concluídas com um clique em **Desanexar Tudo** no menu **Depurar** .  
  
## <a name="controlling-the-debugger"></a>Controlando o depurador  
 Você pode controlar a forma como o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] opera por meio do uso dos seguintes comandos de menu, barras de ferramentas e atalhos:  
  
-   O menu **Depurar** e a barra de ferramentas **Depurar** . O menu **Depurar** e a barra de ferramentas **Depurar** permanecem inativos até que o foco seja colocado em uma janela do Editor de Consultas aberta. Eles permanecem ativos até que o projeto atual seja fechado.  
  
-   Os atalhos de teclado do depurador.  
  
-   O menu de atalho do Editor de Consultas. O menu de atalho é exibido quando você clica em uma linha com o botão direito do mouse em uma janela do Editor de Consultas. Quando a janela do Editor de Consultas está em modo de depuração, o menu de atalho exibe comandos do depurador aplicáveis à linha ou cadeia de caracteres selecionada.  
  
-   Itens de menu e comandos de contexto nas janelas que são abertas pelo depurador, como as janelas de **Inspeção** ou **Pontos de Interrupção** .  
  
 A tabela a seguir mostra os comandos de menu, botões da barra de ferramentas e atalhos de teclado do depurador.  
  
|Comando do menu Depurar|Comando de atalho do Editor|Botão da barra de ferramentas|Atalho do teclado|Ação|  
|------------------------|-----------------------------|--------------------|-----------------------|------------|  
|**Janelas/Pontos de Interrupção**|Não disponível|**Pontos de Interrupção**|CTRL+ALT+B|Exibir a janela **Pontos de Interrupção** , que permite exibir e gerenciar pontos de interrupção.|  
|**Janelas/Inspeção/Inspeção1**|Não disponível|**Pontos de Interrupção/Inspeção/Inspeção1**|CTRL+ALT+W, 1|Exibir a janela **Inspeção1** .|  
|**Janelas/Inspeção/Inspeção2**|Não disponível|**Pontos de Interrupção/Inspeção/Inspeção2**|CTRL+ALT+W, 2|Exibir a janela **Inspeção2** .|  
|**Janelas/Inspeção/Inspeção3**|Não disponível|**Pontos de Interrupção/Inspeção/Inspeção3**|CTRL+ALT+W, 3|Exibir a janela **Inspeção3** .|  
|**Janelas/Inspeção/Inspeção4**|Não disponível|**Pontos de Interrupção/Inspeção/Inspeção4**|CTRL+ALT+W, 4|Exibir a janela **Inspeção4** .|  
|**Janelas/Locais**|Não disponível|**Pontos de Interrupção/Locais**|CTRL+ALT+V, L|Exibir a janela **Locais** .|  
|**Janelas/Pilha de Chamadas**|Não disponível|**Pontos de Interrupção/Pilha de Chamadas**|CTRL+ALT+C|Exibir a janela **Pilha de Chamadas** .|  
|**Janelas/Threads**|Não disponível|**Pontos de Interrupção/Threads**|CTRL+ALT+H|Exibir a janela **Threads** .|  
|**Continuar**|Não disponível|**Continuar**|ALT+F5|Executar até o próximo ponto de interrupção. **Continuar** permanece inativo até que o foco esteja em uma janela do Editor de Consultas que esteja em modo de depuração.|  
|**Iniciar Depuração**|Não disponível|**Iniciar Depuração**|ALT+F5|Colocar uma janela do Editor de Consultas em modo de depuração e executar até o primeiro ponto de interrupção. Se o foco estiver em uma janela do Editor de Consulta que esteja em modo de depuração, **Iniciar Depuração** é substituído por **Continuar**.|  
|**Interromper Tudo**|Não disponível|**Interromper Tudo**|CTRL+ALT+BREAK|Esse recurso não é usado pelo depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**Parar depuração**|Não disponível|**Parar depuração**|SHIFT+F5|Tirar uma janela do Editor de Consultas do modo de depuração e retorná-la para o modo normal.|  
|**Desanexar Tudo**|Não disponível|Não disponível|Não disponível|Para o modo de depuração, mas executa as instruções restantes na janela do Editor de Consultas.|  
|**Intervir**|Não disponível|**Intervir**|F11|Executar a próxima instrução e também abrir uma nova janela do Editor de Consultas em modo de depuração se a próxima instrução executar um procedimento armazenado, gatilho, ou função.|  
|**Contornar**|Não disponível|**Contornar**|F10|O mesmo que **Intervir**, mas nenhuma função, procedimento armazenado ou gatilho é depurado.|  
|**Sair**|Não disponível|**Sair**|Shift+F11|Executar o código restante de um gatilho, função ou procedimento armazenado sem fazer uma pausa em qualquer ponto de interrupção. O modo de depuração normal é retomado quando o controle é retornado ao código que chamou o módulo.|  
|Não disponível|**Executar Até** o Cursor|Não disponível|CTRL+F10|Executar todo o código desde o último local de parada até o local atual do cursor sem parar em qualquer ponto de interrupção.|  
|**QuickWatch**|**QuickWatch**|Não disponível|CTRL+ALT+Q|Exibir a janela **QuickWatch** .|  
|**Alternar ponto de interrupção**|**Ponto de Interrupção/Inserir Ponto de Interrupção**|Não disponível|F9|Posicionar um ponto de interrupção na instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] atual ou selecionada.|  
|Não disponível|**Ponto de Interrupção/Excluir Ponto de Interrupção**|Não disponível|Não disponível|Excluir o ponto de interrupção da linha selecionada.|  
|Não disponível|**Ponto de Interrupção/Desabilitar Ponto de Interrupção**|Não disponível|Não disponível|Desabilitar o ponto de interrupção na linha selecionada. O ponto de interrupção permanecerá na linha de código, mas não parará a execução até ser reativado.|  
|Não disponível|**Ponto de Interrupção/Habilitar Ponto de Interrupção**|Não disponível|Não disponível|Habilitar o ponto de interrupção na linha selecionada.|  
|**Excluir Todos os Pontos de Interrupção**|Não disponível|Não disponível|Ctrl+Shift+F9|Excluir todos os pontos de interrupção.|  
|**Desabilitar Todos os Pontos de Interrupção**|Não disponível|Não disponível|Não disponível|Desabilitar todos os pontos de interrupção.|  
|Não disponível|**Adicionar Inspeção**|Não disponível|Não disponível|Adicionar a expressão selecionada à janela **Inspeção** .|  
  
## <a name="see-also"></a>Consulte Também  
 [Depurador do Transact-SQL](transact-sql-debugger.md)   
 [Percorrer código Transact-SQL](step-through-transact-sql-code.md)   
 [Informações do depurador Transact-SQL](transact-sql-debugger-information.md)   
 [Editor de Consultas do Mecanismo de Banco de Dados &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)  
  
  
