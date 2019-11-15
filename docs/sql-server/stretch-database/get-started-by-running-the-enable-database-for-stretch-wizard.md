---
title: Comece executando o Assistente para Habilitar o Banco de Dados para Alongamento
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: quickstart
f1_keywords:
- sql13.swb.stretchwizard.f1
- sql13.swb.stretchwizard.createdatabasecredentials.f1
- sql13.swb.stretchwizard.selectdatabasetables.f1
- sql13.swb.stretchwizard.validatesqlserver.f1
- sql13.swb.stretchwizard.selectazuredeployment.f1
- sql13.swb.stretchwizard.configureazuredeployment.f1
- sql13.swb.stretchwizard.Summary.f1
- sql13.swb.stretchwizard.Results.f1
- sql13.swb.stretchwizard.introduction.f1
helpviewer_keywords:
- Stretch Database, wizard
- Enable Database for Stretch Wizard
ms.assetid: 855dd9fc-f80c-4dbc-bf46-55a9736bfe15
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 5d730c8e71044154b9844174ac8d21837c9ea05f
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843799"
---
# <a name="get-started-by-running-the-enable-database-for-stretch-wizard"></a>Comece executando o Assistente para Habilitar o Banco de Dados para Alongamento
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


 Para configurar um banco de dados para o Stretch Database, execute o Assistente para Habilitar o Banco de Dados para Alongamento.  Este artigo descreve as informações que você precisa inserir, bem como as escolhas que você deve fazer no assistente.  
  
 Para saber mais sobre o Stretch Database, confira [Stretch Database](../../sql-server/stretch-database/stretch-database.md). 
 
 > [!NOTE] 
 > Mais tarde, se você desabilitar o Stretch Database, lembre-se de que desabilitar uma tabela ou um banco de dados do Stretch Database não excluirá o objeto remoto. Se você quiser excluir a tabela remota ou o banco de dados remoto, descarte-o(a) usando o Portal de Gerenciamento do Azure. Os objetos remotos continuam incorrendo em custos do Azure até que você os exclua manualmente. 
  
## <a name="launch-the-wizard"></a>Iniciar o assistente  
  
1.  No SQL Server Management Studio, no Pesquisador de objetos, selecione o banco de dados no qual você deseja habilitar o Stretch.  
  
2.  Clique com o botão direito do mouse e selecione **Tarefas**, **Stretch**e **Habilitar** para iniciar o assistente.  
  
##  <a name="Intro"></a> Introdução  
 Verifique o objetivo do assistente e os pré-requisitos.  
 
 Os pré-requisitos importantes incluem os descritos a seguir.
 -   Você precisa ser um administrador para alterar as configurações de banco de dados.
 -   Você precisa ter uma assinatura do Microsoft Azure.
 -   O SQL Server deve ter a capacidade de se comunicar com o servidor remoto do Azure.
  
 ![Página de introdução do assistente do Stretch Database](../../sql-server/stretch-database/media/stretch-wizard-1.png "Página de introdução do assistente do Stretch Database")  
  
##  <a name="Tables"></a> Selecionar tabelas  
 Selecione as tabelas para habilitar o Stretch.  
 
Tabelas com várias linhas aparecem na parte superior da lista classificada. Antes que o Assistente exiba a lista de tabelas, ele analisa os tipos de dados nela para os quais atualmente não há suporte no Stretch Database. 
  
 ![Página de seleção de tabelas do assistente do Stretch Database](../../sql-server/stretch-database/media/stretch-wizard-2.png "Página de seleção de tabelas do assistente do Stretch Database")  
  
|coluna|Descrição|  
|------------|-----------------|  
|(sem título)|Marque a caixa de seleção nesta coluna para habilitar a tabela selecionada para o Stretch.|  
|**Nome**|Especifica o nome da coluna no banco de dados.|  
|(sem título)|Um símbolo nesta coluna pode representar um aviso que não impede a habilitação da tabela selecionada para Stretch. Ele também pode representar um problema de bloqueio que impede a habilitação da tabela selecionada para Stretch – por exemplo, porque a tabela usa um tipo de dados sem suporte. Passe o mouse sobre o símbolo para exibir mais informações em uma dica de ferramenta. Para obter mais informações, veja [Limitações do Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md).|  
|**Ampliada**|Indica se a tabela já foi está habilitada para Stretch.|  
|**Migrar**|É possível migrar uma tabela inteira (**Tabela Inteira**) ou especificar um filtro em uma coluna existente na tabela. Se você quiser usar uma função de filtro diferente para selecionar linhas a serem migradas, execute a instrução ALTER TABLE para especificar a função de filtro depois de sair do assistente. Para obter mais informações sobre a função de filtro, veja [Select rows to migrate by using a filter function (Selecionar linhas a serem migradas usando uma função de filtro)](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). Para obter mais informações sobre como aplicar a função, veja [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) ou [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).|  
|**Linhas**|Especifica o número de linhas na tabela.|  
|**Tamanho (KB)**|Especifica o tamanho da tabela em KB.|  
  
## <a name="optionally-provide-a-row-filter"></a>Opcionalmente, forneça um filtro de linha  
 Se você quiser fornecer uma função de filtro para selecionar linhas a serem migradas, siga o procedimento indicado na página **Selecionar tabelas** .  
  
1.  Na lista **Selecione as tabelas que deseja ampliar** , clique em **Tabela Inteira** na linha da tabela. A caixa de diálogo **Selecionar linhas para ampliar** será aberta.  
  
     ![Definir um predicado de filtro baseado em data](../../sql-server/stretch-database/media/stretch-wizard-2a.png "Definir um predicado de filtro baseado em data")  
  
2.  Na caixa de diálogo **Selecionar linhas para ampliar** , selecione **Escolher Linhas**.  
  
3.  No **campo Nome**, forneça um nome para a função de filtro.  
  
4.  Para a cláusula **Where** , escolha uma coluna da tabela, selecione um operador e forneça um valor.  
  
5.  Clique em **Verificar** para testar a função. Se a função retornar os resultados da tabela – ou seja, se houver linhas a serem migradas que atendam à condição – o teste relatará **Êxito**.  

> [!NOTE] 
> A caixa de texto que exibe a consulta de filtro é somente leitura. Não é possível editar a consulta na caixa de texto.
  
6.  Clique em Concluído para retornar à página **Selecionar tabelas** .  

A função de filtro é criada no SQL Server apenas quando o assistente é concluído. Até lá, você pode retornar à página **Selecionar tabelas** para alterar ou renomear a função de filtro.

![Página de seleção de tabelas após definir um predicado de filtro](../../sql-server/stretch-database/media/stretch-wizard-2b.png "Página de seleção de tabelas após definir um predicado de filtro")

Se você desejar usar um tipo diferente de função de filtro para selecionar as linhas a serem migradas, siga um destes procedimentos.  
  
-   Saia do assistente e execute a instrução ALTER TABLE para habilitar o Stretch para a tabela e especificar uma função de filtro. Para obter mais informações, veja [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).  
  
-   Execute a instrução ALTER TABLE para especificar uma função de filtro depois que você sair do assistente. Para as etapas obrigatórias, consulte [Adicionar uma função de filtro após executar o assistente](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz).  
  
##  <a name="Configure"></a> Configurar o Azure  
  
1.  Entre no Microsoft Azure com uma conta da Microsoft.  
  
     ![Entrar no Azure – assistente do Stretch Database](../../sql-server/stretch-database/media/stretch-wizard-3.png "Entrar no Azure – assistente do Stretch Database")  
  
2.  Selecione a assinatura do Azure a ser usada para o Stretch Database. 

> [!NOTE] 
> Para habilitar o Stretch em um banco de dados, você deve ter direitos de administrador para a assinatura que você está usando. O assistente do Stretch Database só mostrará assinaturas em que o usuário tem direitos de administrador.
  
3.  Selecione a região do Azure a ser usada para o Stretch Database.
    -   Se você criar um novo servidor, o servidor será criado nessa região.  
    -   Se você houver servidores na região selecionada, o assistente os listará quando você escolher **Servidor existente**.
  
     Para minimizar a latência, escolha a região do Azure onde seu SQL Server está localizado. Para saber mais sobre regiões, confira [Regiões do Azure](https://azure.microsoft.com/regions/).  
  
4.  Especifique se você deseja usar um servidor existente ou criar um novo servidor do Azure.  
  
     Se o Active Directory em seu SQL Server for federado com o Azure Active Directory, você pode usar como opção uma conta de serviço federado do SQL Server a fim de se comunicar com o servidor remoto do Azure. Para obter mais informações sobre os requisitos para essa opção, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
    -   **Criar novo servidor**  
  
        1.  Crie um logon e senha para o administrador do servidor.  
  
        2.  Opcionalmente, você pode usar uma conta de serviço federado do SQL Server para comunicar-se com o servidor remoto do Azure.  
  
         ![Criar novo servidor do Azure – assistente de Stretch Database](../../relational-databases/tables/media/stretch-wizard-4.png "Criar novo servidor do Azure – assistente de Stretch Database")  
  
    -   **Servidor existente**  
  
        1.  Selecione o servidor do Azure existente.  
  
        2.  Selecione o método de autenticação.  
  
            -   Se você selecionar **Autenticação do SQL Server**, forneça o logon de administrador e a senha.  
  
            -   Selecione **Autenticação Integrada do Active Directory** para usar uma conta de serviço federado do SQL Server para comunicar-se com o servidor remoto do Azure. Se o servidor selecionado não estiver integrado ao Azure Active Directory, essa opção não aparecerá.
  
         ![Selecionar servidor do Azure existente – assistente do Stretch Database](../../sql-server/stretch-database/media/stretch-wizard-5.png "Selecionar servidor do Azure existente – assistente do Stretch Database")  
  
##  <a name="Credentials"></a> Proteger credenciais  
 Você precisa ter uma chave mestra de banco de dados para proteger as credenciais usadas pelo Stretch Database para se conectar ao banco de dados remoto.  
  
 Se já existir uma chave mestra de banco de dados, insira a senha dela.  
  
 ![Página Proteger credenciais do assistente de Stretch Database](../../sql-server/stretch-database/media/stretch-wizard-6b.PNG "Página Proteger credenciais do assistente de Stretch Database")  
  
 Se o banco de dados não tiver uma chave mestra, insira uma senha forte para criar uma chave mestra de banco de dados.  
  
 ![Página Proteger credenciais do assistente de Stretch Database](../../relational-databases/tables/media/stretch-wizard-6.png "Página Proteger credenciais do assistente de Stretch Database")  
  
 Para obter mais informações sobre a chave mestra do banco de dados, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) e [Criar uma chave mestra de banco de dados](../../relational-databases/security/encryption/create-a-database-master-key.md). Para obter mais informações sobre as credenciais criadas pelo assistente, veja [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
##  <a name="Network"></a> Selecionar endereço IP  
 Use o intervalo de endereços IP de sub-rede (recomendado) ou o endereço IP público do SQL Server, para criar uma regra de firewall no Azure que permite ao SQL Server se comunicar com o servidor remoto do Azure.  
  
 O endereço, ou endereços, IP que você fornecer nesta página informarão ao servidor do Azure que permita a passagem de dados de entrada, consultas e operações de gerenciamento iniciadas pelo SQL Server pelo firewall do Azure. O assistente não altera qualquer outra coisa nas configurações do firewall no SQL Server.  
  
 ![Página Selecionar endereço IP do assistente Stretch Database](../../relational-databases/tables/media/stretch-wizard-7.png "Página Selecionar endereço IP do assistente Stretch Database")  
  
##  <a name="Summary"></a> Resumo  
 Examine os valores que você inseriu e as opções selecionadas no assistente, além dos custos estimados no Azure. Em seguida, escolha **Concluir** para habilitar o Stretch.  
  
 ![Página de resumo do assistente do Stretch Database](../../sql-server/stretch-database/media/stretch-wizard-8.png "Página de resumo do assistente do Stretch Database")  
  
##  <a name="Results"></a> Resultados  
 Analise os resultados.  
  
 Para monitorar o status da migração de dados, veja [Monitorar e solucionar problemas de migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).  
  
 ![Página de resultados do assistente do Stretch Database](../../sql-server/stretch-database/media/stretch-wizard-9.PNG "Página de resultados do assistente do Stretch Database")  
  
##  <a name="KnownIssues"></a> Solução de problemas do assistente  
 **O assistente do Stretch Database falhou.**  
 Se Stretch Database ainda tiver sido habilitado no nível do servidor, e você executar o assistente sem as permissões de administrador do sistema, o assistente falhará. Peça ao administrador do sistema para habilitar o Stretch Database na instância do servidor local e, depois, execute o assistente novamente. Para obter mais informações, confira [Pré-requisito: permissão para habilitar o Stretch Database no servidor.](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md#EnableTSQLServer)  
  
## <a name="next-steps"></a>Próximas etapas  
 Habilite outras tabelas para o Stretch Database. Monitore a migração dos dados e gerencie os bancos de dados e tabelas habilitados para o Stretch.  
  
-   [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) para habilitar outras tabelas.  
  
-   [Monitorar e solucionar problemas de migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) para ver o status da migração de dados.  
  
-   [Pausar e retomar a migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [Gerenciar e solucionar problemas no Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [Fazer backup de bancos de dados habilitados para Stretch](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [Restaurar bancos de dados habilitados para Stretch](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar o Stretch Database para um banco de dados](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
