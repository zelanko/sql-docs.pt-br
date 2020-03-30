---
title: Registrar um banco de dados como um DAC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerdacwizard.summary.f1
- sql13.swb.registerdacwizard.introduction.f1
- sql13.swb.registerdacwizard.setproperties.f1
- sql13.swb.registerdacwizard.registerdac.f1
helpviewer_keywords:
- wizard [DAC], register
- How to [DAC], register
- register DAC
- data-tier application [SQL Server], register
ms.assetid: 08e52aa6-12f3-41dd-a793-14b99a083fd5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 726955115dc956f2ad16e39775610deb16c445a1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68134682"
---
# <a name="register-a-database-as-a-dac"></a>Registrar um banco de dados como um DAC
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Use o **Assistente para Registrar o Aplicativo da Camada de Dados** ou um script do Windows PowerShell para compilar uma definição do DAC (aplicativo da camada de dados) que descreva os objetos em um banco de dados existente e registre a definição do DAC no banco de dados do sistema **msdb** (**master** no [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]).  
  
-   **Antes de começar:**  [Limitações e Restrições](#LimitationsRestrictions), [Permissões](#Permissions)  
  
-   **Para atualizar um DAC, usando:**  [O Assistente de Aplicativo da Camada de Dados de Registro](#UsingRegisterDACWizard), [PowerShell](#RegisterDACPowerShell)  
  
## <a name="before-you-begin"></a>Antes de começar  
 O processo de registro cria uma definição do DAC que define os objetos no banco de dados. A combinação da definição do DAC e do banco de dados forma uma instância do DAC. Se você registrar um banco de dados como um DAC em uma instância do Mecanismo de Banco de Dados, o DAC registrado será incorporado ao Utilitário do SQL Server na próxima vez que o conjunto de coleta do utilitário for enviado da instância para o Ponto de Controle do Utilitário. O DAC estará presente no nó **Aplicativos no Nível de Dados Implantados** do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Gerenciador do Utilitário** e é relatado na página de detalhes **Aplicativos no Nível de Dados Implantados**.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitações e restrições  
 O registro do DAC só pode ser executado em um banco de dados no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ou no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) ou posterior. O registro do DAC não poderá ser executado se um DAC já estiver registrado para o banco de dados. Por exemplo, se o banco de dados foi criado através da implantação de um DAC, você não poderá executar o **Assistente para Registrar o Aplicativo da Camada de Dados**.  
  
 Você não poderá registrar um DAC se o banco de dados tiver objetos que não tenham suporte em um DAC ou usuários contidos. Para obter mais informações sobre os tipos de objetos com suporte em um DAC, consulte [DAC Support For SQL Server Objects and Versions](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md).  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 O registro de um DAC em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] requer, pelo menos, permissões VIEW DEFINITION de escopo de banco de dados e ALTER ANY LOGIN, permissões SELECT em **sys.sql_expression_dependencies**, e associação na função de servidor fixa **dbcreator** . Os membros da função de servidor fixa **sysadmin** ou a conta interna do administrador do sistema do SQL Server denominada **sa** também podem registrar um DAC. O registro de um DAC que não contém logons no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] exige associação nas funções **dbmanager** ou **serveradmin** . O registro de um DAC que contém logons no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] exige associação nas funções **loginmanager** or **serveradmin** .  
  
##  <a name="using-the-register-data-tier-application-wizard"></a><a name="UsingRegisterDACWizard"></a> Usando o Assistente para Registrar o Aplicativo da Camada de Dados  
 **Para registrar um DAC usando um assistente**  
  
1.  No **Pesquisador de Objetos**, expanda o nó da instância que contém o banco de dados a ser registrado como um DAC.  
  
2.  Expanda o nó **Bancos de Dados** .  
  
3.  Clique com o botão direito do mouse no banco de dados a ser registrado, aponte para **Tarefas** e selecione **Registrar como Aplicativo da Camada de Dados...**  
  
4.  Conclua as etapas das caixas de diálogo do assistente:  
  
    1.  [Página de Introdução](#Introduction)  
  
    2.  [Página Definir Propriedades](#Set_properties)  
  
    3.  [Página Validação e Resumo](#Summary)  
  
    4.  [Página Registrar o DAC](#Register)  
  
##  <a name="introduction-page"></a><a name="Introduction"></a> Página de Introdução  
 Essa página descreve as etapas do registro de um aplicativo da camada de dados.  
  
 **Não mostrar esta página novamente.** - Clique na caixa de seleção para interromper a exibição da página no futuro.  
  
 **Avançar >** - Continua na página **Definir Propriedades**.  
  
 **Cancelar** - Finaliza o assistente sem registrar um DAC.  
  
 [Usando o Assistente para Registrar o Aplicativo da Camada de Dados](#UsingRegisterDACWizard)  
  
##  <a name="set-properties-page"></a><a name="Set_properties"></a> Página Definir Propriedades  
 Use essa página para especificar propriedades no nível do DAC, como o nome e a versão do aplicativo.  
  
 **Nome do aplicativo.** – Uma cadeia de caracteres que especifica o nome usado para identificar a definição do DAC, o campo foi populado com o nome do banco de dados.  
  
 **Versão.** - Um valor numérico que identifica a versão do DAC. A versão do DAC é usada no Visual Studio para identificar a versão do DAC em que os desenvolvedores estão trabalhando. Ao implantar um DAC, a versão é armazenada no banco de dados **msdb** e é exibida posteriormente no nó **Aplicativos da Camada de Dados** em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Descrição.** - Opcional. Texto que explica a finalidade do DAC. Ao implantar um DAC, a descrição é armazenada no banco de dados **msdb** e é exibida posteriormente no nó **Aplicativos da Camada de Dados** em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **< Anterior** - Retorna para a página de **Introdução**.  
  
 **Avançar >** - Verifica se um DAC pode ser compilado por meio dos objetos do banco de dados e exibe os resultados na página de **Validação e Resumo**.  
  
 **Cancelar** - Finaliza o assistente sem registrar o DAC.  
  
 [Usando o Assistente para Registrar o Aplicativo da Camada de Dados](#UsingRegisterDACWizard)  
  
##  <a name="validation-and-summary-page"></a><a name="Summary"></a> Página Validação e Resumo  
 Use essa página para revisar as ações do assistente ao registrar o DAC. A página faz transição por três estados ao verificar se um DAC pode ser compilado a partir dos objetos do banco de dados.  
  
 [Usando o Assistente para Registrar o Aplicativo da Camada de Dados](#UsingRegisterDACWizard)  
  
### <a name="retrieving-objects"></a>Recuperando objetos  
 **Recuperando os objetos de banco de dados e de servidor.** - Exibe uma barra de progresso enquanto o assistente recupera todos os objetos necessários do banco de dados e da instância do Mecanismo de Banco de Dados.  
  
 **< Anterior** - Retorna para a página **Definir propriedades** para alterar suas entradas.  
  
 **Avançar >** - Registra o DAC e exibe os resultados na página **Registrar o DAC**.  
  
 **Cancelar** - Finaliza o assistente sem registrar o DAC.  
  
 [Usando o Assistente para Registrar o Aplicativo da Camada de Dados](#UsingRegisterDACWizard)  
  
### <a name="validating-objects"></a>Validando objetos  
 **Verificando** _SchemaName_ **.** _ObjectName_ **.** - Exibe uma barra de progresso enquanto o assistente verifica as dependências dos objetos recuperados e se todos eles são objetos válidos para um DAC. _SchemaName_ **.** _ObjectName_ identifica qual objeto está sendo verificado no momento.  
  
 **< Anterior** - Retorna para a página **Definir propriedades** para alterar suas entradas.  
  
 **Avançar >** - Registra o DAC e exibe os resultados na página **Registrar o DAC**.  
  
 **Cancelar** - Finaliza o assistente sem registrar o DAC.  
  
 [Usando o Assistente para Registrar o Aplicativo da Camada de Dados](#UsingRegisterDACWizard)  
  
### <a name="summary"></a>Resumo  
 **A configuração a seguir será usada para registrar o DAC.** - Exibe um relatório das propriedades e objetos que serão incluídos no DAC.  
  
 **Salvar Relatório** - Selecione esse botão para salvar uma cópia do relatório de validação em um arquivo HTML. A pasta padrão é **SQL Server Gerenciamento Studio\DAC Packages** na pasta Documentos da conta do Windows.  
  
 **< Anterior** - Retorna para a página **Definir propriedades** para alterar suas entradas.  
  
 **Avançar >** - Registra o DAC e exibe os resultados na página **Registrar o DAC**.  
  
 **Cancelar** - Finaliza o assistente sem registrar o DAC.  
  
 [Usando o Assistente para Registrar o Aplicativo da Camada de Dados](#UsingRegisterDACWizard)  
  
##  <a name="register-dac-page"></a><a name="Register"></a> Página Registrar o DAC  
 Essa página relata o êxito ou a falha da operação de registro.  
  
 **Registrando o DAC** - Relata o êxito ou a falha de cada ação realizada para registrar o DAC. Analise as informações para determinar o êxito ou falha de cada ação. Todas as ações que encontrarem um erro terão um link na coluna **Resultado** . Selecione o link para exibir um relatório do erro para aquela ação.  
  
 **Salvar Relatório** - Selecione esse botão para salvar o relatório de registro em um arquivo HTML. O arquivo relata o status de cada ação, inclusive todos os erros gerados por qualquer uma das ações. A pasta padrão é **SQL Server Gerenciamento Studio\DAC Packages** na pasta Documentos da conta do Windows. O nome de arquivo está no formato \<DACPackageName>_RegisterDACReport_yyyymmdd.html, em que \<*DACPackageName*> é o nome do pacote que está sendo implantado, *yyyy* = ano atual, *mm* = mês atual e *dd* = dia atual.  
  
 **Concluir** – Encerra o assistente.  
  
 [Usando o Assistente para Registrar o Aplicativo da Camada de Dados](#UsingRegisterDACWizard)  
  
##  <a name="register-a-dac-using-powershell"></a><a name="RegisterDACPowerShell"></a> Registrar um DAC usando o PowerShell  
 **Para registrar um banco de dados como um DAC usando o método Register() em um script de PowerShell**  
  
1.  Crie um objeto de servidor SMO e defina-o como a instância que contém o banco de dados a ser registrado como um DAC.  
  
2.  Adicione uma variável que especifique o nome do banco de dados.  
  
3.  Especifique os metadados do DAC, como o nome, a versão e a descrição do DAC.  
  
4.  Execute o método Register com as informações especificadas acima.  
  
### <a name="example-powershell"></a>Exemplo (PowerShell)  
 O exemplo a seguir registra um banco de dados chamado MyDB como um DAC.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Specify the database to register as a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Register the DAC.  
$registerunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$registerunit.Description = $description  
$registerunit.Register()  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativos da camada de dados](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
