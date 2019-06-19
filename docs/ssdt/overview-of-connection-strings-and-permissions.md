---
title: Visão geral das cadeias de conexão e permissões | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: ceff114e-a738-46ad-9785-b6647a2247f9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 413d6ad71b70cc4ddca8205589d25e224bbcad76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65102027"
---
# <a name="overview-of-connection-strings-and-permissions"></a>Visão geral das cadeias de conexão e permissões
Para executar testes de unidade do SQL Server, você deve se conectar a um servidor de banco de dados usando uma ou duas cadeias de conexão específicas. Cada cadeia de conexão representa uma conta com as permissões específicas que você deve ter para executar a tarefa ou o conjunto de tarefas em um script específico como parte do teste. Você pode especificar essas cadeias de caracteres na caixa de diálogo **Configuração de Teste do SQL Server** ou editando manualmente o arquivo app.config do projeto de teste.  
  
## <a name="connection-strings"></a>Cadeias de Conexão  
Na caixa de diálogo **Configuração de Teste do SQL Server**, você pode especificar cadeias de conexão para cada uma das contas a seguir.  
  
> [!NOTE]  
> O contexto de execução e o contexto privilegiado serão diferentes somente se você usar a autenticação do SQL Server. Se você usar a autenticação do Windows, as mesmas credenciais serão usadas para ambas as cadeias de conexão.  
  
-   Contexto de execução (obrigatório) - uma conta de usuário para executar o script de teste. Essa cadeia de conexão deve ter as mesmas credenciais que você espera que os usuários tenham. Isso é importante porque garante que as permissões apropriadas sejam aplicadas ao banco de dados. Para obter mais informações, confira [Como Configurar a execução do teste de unidade do SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md).  
  
    No arquivo app.config do projeto de teste, esse é o elemento `ExecutionContext`.  
  
-   Contexto privilegiado (opcional) - uma conta no mesmo banco de dados que tenha permissões mais altas para executar a ação de pré-teste, a ação de pós-teste, os scripts TestInitialize e os scripts TestCleanup. Esses scripts definem o estado do banco de dados e, no caso da ação de pós-teste, podem ser usados para validar objetos no banco de dados. Essa cadeia de conexão também é usada para implantar alterações de banco de dados e gerar dados.  
  
    No arquivo app.config do projeto de teste, esse é o elemento `PrivilegedContext`. Se os testes de unidade do SQL Server executarem somente o script de teste, você não precisará especificar um contexto privilegiado.  
  
As cadeias de caracteres especificadas na caixa de diálogo Configuração do Projeto são armazenadas no arquivo app.config do projeto de teste. Você também pode editar esse arquivo diretamente e recompilar o projeto; depois disso, os novos valores serão exibidos na caixa de diálogo.  
  
## <a name="windows-authentication-versus-sql-server-authentication"></a>Autenticação do Windows versus autenticação do SQL Server  
Quando você especificar cadeias de conexão, escolha entre o uso da autenticação do Windows e da autenticação do SQL. Um motivo para escolher a autenticação do Windows é que ela oferece suporte ao uso dos testes por uma equipe melhor do que a autenticação do SQL Server. Se você escolher a autenticação do SQL Server, as cadeias de conexão serão criptografadas, usando a API de proteção de dados (DPAPI) com base em suas credenciais do usuário. Isso significa que os testes no projeto de teste serão executados apenas para você, não para os membros da equipe que obtêm os testes por meio do sistema de controle de origem após você realizar o check-in deles. Para executar testes no projeto teste, outras pessoas da sua equipe precisam reconfigurar o projeto de teste usando as suas próprias credenciais. Para fazer isso, eles editariam a cópia do arquivo app.config ou usariam a caixa de diálogo Configuração do Projeto.  
  
## <a name="permissions"></a>Permissões  
O script de teste é executado no nível de permissão do contexto de execução, que é o mesmo nível de permissão a ser aplicado aos comandos do usuário executados no banco de dados quando ele estiver sendo usado da maneira habitual. A ação de pré-teste, a ação de pós-teste, os scripts TestInitialize e os scripts TestCleanup são executados no nível de permissão do contexto privilegiado.  
  
Devido à conexão de permissão mais alta usada para o script da ação de pós-teste, você pode executar a validação nela. Nesse script, você também pode executar comandos de script que testam permissões. Para saber mais sobre permissões, confira a seção de testes de unidade do SQL Server de [Permissões necessárias para o SQL Server Data Tools](../ssdt/required-permissions-for-sql-server-data-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Scripts nos testes de unidade do SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md)  
[Arquivos de teste de unidade do SQL Server](../ssdt/sql-server-unit-test-files.md)  
  
