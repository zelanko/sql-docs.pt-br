---
title: Permissões necessárias para SQL Server Data Tools
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: b27038c4-94ab-449c-90b7-29d87ce37a8b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1eb77a0990d8f0e19458dd66ea7f73b933de961c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65101847"
---
# <a name="required-permissions-for-sql-server-data-tools"></a>Permissões necessárias para SQL Server Data Tools
Antes de você realizar uma ação em um banco de dados no Visual Studio, faça logon com uma conta que tem determinadas permissões nesse banco de dados. As permissões específicas de que você precisa variam com base na ação que você deseja realizar. As seções a seguir descrevem cada ação que você pode querer realizar e a permissão específica de que você precisa para realizá-la.  
  
-   [Permissões para criar ou implantar um banco de dados](#DatabaseCreationAndDeploymentPermissions)  
  
-   [Permissões para refatorar um banco de dados](#DatabaseRefactoringPermissions)  
  
-   [Permissões para realizar testes de unidade em um banco de dados do SQL Server](#DatabaseUnitTestingPermissions)  
  
-   [Permissões para gerar dados](#DataGenerationPermissions)  
  
-   [Permissões para comparar esquemas e dados](#SchemaAndDataComparePermissions)  
  
-   [Permissões para executar o Editor do Transact-SQL](#Transact-SQLEditorPermissions)  
  
-   [Permissões para projetos SQL CLR (Common Language Runtime do SQL Server)](#SQLCLRPermissions)  
  
## <a name="DatabaseCreationAndDeploymentPermissions"></a>Permissões para criar ou implantar um banco de dados  
Você deve ter as permissões a seguir para criar ou implantar um banco de dados.  
  
|||  
|-|-|  
|Ações|Permissões necessárias|  
|Importar objetos de banco de dados e configurações|Você deve ser capaz de se conectar ao banco de dados de origem.<br /><br />Se o banco de dados de origem estiver baseado no SQL Server 2005, você também deverá ter a permissão **VIEW DEFINITION** em cada objeto.<br /><br />Se o banco de dados de origem estiver baseado no SQL Server 2008 ou posterior, você também deverá ter a permissão **VIEW DEFINITION** em cada objeto. Seu logon deve ter a permissão **VIEW SERVER STATE** (para chaves de criptografia de banco de dados).|  
|Importar objetos de servidor e configurações|Você deve ser capaz de se conectar ao banco de dados mestre no servidor especificado.<br /><br />Se o servidor estiver executando o SQL Server 2005, você deverá ter a permissão **VIEW ANY DEFINITION** no servidor.<br /><br />Se o banco de dados de origem estiver baseado no SQL Server 2008 ou posterior, você também deverá ter a permissão **VIEW ANY DEFINITION** no servidor. Seu logon deve ter a permissão **VIEW SERVER STATE** (para chaves de criptografia de banco de dados).|  
|Criar ou atualizar um projeto de banco de dados|Você não precisa de permissões de banco de dados para criar ou modificar um projeto de banco de dados.|  
|Implantar um novo banco de dados ou implantar com o conjunto de opções **Sempre recriar banco de dados**|Você deve ter a permissão **CREATE DATABASE** ou ser membro da função **dbcreator** no servidor de destino.<br /><br />Quando você cria um banco de dados, o Visual Studio conecta-se ao banco de dados modelo e copia seus conteúdos. O logon inicial (por exemplo, *seuLogon*) que você usa para se conectar ao banco de dados de destino deve ter as permissões **db_creator** e **CONNECT SQL**. Esse logon deve ter um mapeamento de usuário no banco de dados modelo. Se você tiver permissões de **sysadmin**, poderá criar o mapeamento emitindo as seguintes instruções de Transact\-SQL:<br /><br />`USE [model] CREATE USER yourUser FROM LOGIN yourLogin`<br /><br />O usuário (neste exemplo, yourUser) deve ter as permissões **CONNECT** e **VIEW DEFINITION** no modelo de banco de dados. Se você tiver permissões de **sysadmin**, poderá conceder essas permissões emitindo as seguintes instruções de Transact\-SQL:<br /><br />`USE [model] GRANT CONNECT to yourUser GRANT VIEW DEFINITION TO yourUser`<br /><br />Se você implantar um banco de dados que contém restrições não nomeadas e a opção **CheckNewContraints** estiver habilitada (ela é habilitada por padrão), deverá ter as permissões de **db_owner** ou **sysadmin** ou ocorrerá uma falha na implantação. Isso é verdadeiro somente para restrições não nomeadas. Para obter mais informações sobre a opção **CheckNewConstraints**, consulte [Configurações do projeto de banco de dados](../ssdt/database-project-settings.md).|  
|Implantar atualizações em um banco de dados existente|Você deve ser um usuário de banco de dados válido. Você também deve ser membro da função **db_ddladmin**, possuir o esquema ou possuir os objetos que deseja criar ou modificar no banco de dados de destino. Você precisa de permissões adicionais para trabalhar com conceitos mais avançados como logons ou servidores vinculados em seus scripts de pré-implantação ou pós-implantação.<br /><br />**OBSERVAÇÃO:** se implantar no banco de dados mestre, você também deverá ter a permissão **VIEW ANY DEFINITION** no servidor da implantação.|  
|Use um assembly com a opção EXTERNAL_ACCESS em um projeto de banco de dados|Você deve definir a propriedade TRUSTWORTHY para seu projeto de banco de dados. Você deve ter a permissão EXTERNAL ACCESS ASSEMBLY para seu logon do SQL Server.|  
|Implantar assemblies em um banco de dados novo ou existente|Você deve ser um membro da função sysadmin no servidor de implantação de destino.|  
  
Para obter mais informações, consulte os Manuais Online do SQL Server.  
  
## <a name="DatabaseRefactoringPermissions"></a>Permissões para refatorar um banco de dados  
A *refatoração de banco de dados* ocorre somente dentro de um projeto de banco de dados. Você deve ter permissões para usar o projeto de banco de dados. Você não precisa de permissões em um banco de dados de destino até implantar suas alterações nele.  
  
## <a name="DatabaseUnitTestingPermissions"></a>Permissões para realizar testes de unidade em um banco de dados do SQL Server  
Você deve ter as permissões a seguir para realizar testes de unidade em um banco de dados.  
  
|||  
|-|-|  
|Ações|Permissões necessárias|  
|Executar uma ação de teste|Você deve usar a conexão de banco de dados do contexto de execução. Para obter mais informações, consulte [Visão geral das cadeias de conexão e permissões](../ssdt/overview-of-connection-strings-and-permissions.md).|  
|Executar uma ação de pré-teste ou pós-teste|Você deve usar a conexão de banco de dados do contexto privilegiado. Essa conexão de banco de dados tem mais permissões do que a conexão do contexto de execução.|  
|Executar os scripts TestInitialize e TestCleanup|Você deve usar a conexão de banco de dados do contexto privilegiado.|  
|Implantar alterações de banco de dados antes de executar os testes|Você deve usar a conexão de banco de dados do contexto privilegiado. Para obter mais informações, confira [Como Configurar a execução do teste de unidade do SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md).|  
|Gerar dados antes de executar os testes|Você deve usar a conexão de banco de dados do contexto privilegiado. Para obter mais informações, confira [Como Configurar a execução do teste de unidade do SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md).|  
  
## <a name="DataGenerationPermissions"></a>Permissões para gerar dados  
Você deve ter as permissões **INSERT** e **SELECT** nos objetos no banco de dados de destino para gerar os dados de teste usando o Gerador de Dados. Se você limpar os dados antes de gerar dados, também deverá ter as permissões **DELETE** nos objetos no banco de dados de destino. Para redefinir a coluna **IDENTITY** em uma tabela, você deverá possuir a tabela ou ser membro da função db_owner ou db_ddladmin.  
  
## <a name="SchemaAndDataComparePermissions"></a>Permissões para comparar esquemas e dados  
Você deve ter as permissões a seguir para comparar esquemas ou dados.  
  
|||  
|-|-|  
|Ações|Permissões necessárias|  
|Comparar os esquemas de dois bancos de dados|Você deve ter as permissões para importar objetos e configurações dos bancos de dados, conforme descrito em [Permissões para criar ou implantar um banco de dados](#DatabaseCreationAndDeploymentPermissions).|  
|Compare os esquemas de um banco de dados e um projeto de banco de dados|Você deve ter as permissões para importar objetos e configurações do banco de dados, conforme descrito em [Permissões para criar ou implantar um banco de dados](#DatabaseCreationAndDeploymentPermissions). Você também deve o projeto de banco de dados aberto no Visual Studio.|  
|Escrever atualizações em um banco de dados de destino|Você deve ter as permissões para implantar atualizações no banco de dados de destino, conforme descrito em [Permissões para criar ou implantar um banco de dados](#DatabaseCreationAndDeploymentPermissions).|  
|Comparar os dados de dois bancos de dados|Além das permissões necessárias para comparar os esquemas de dois bancos de dados, você também precisa da permissão **SELECT** em todas as tabelas que deseja comparar e da permissão para **VIEW DATABASE STATE**.|  
  
Para obter mais informações, consulte os Manuais Online do SQL Server.  
  
## <a name="Transact-SQLEditorPermissions"></a>Permissões para executar o Editor do Transact\-SQL  
O que você pode fazer dentro do editor do Transact\-SQL é determinado pelo seu contexto de execução para o banco de dados de destino.  
  
## <a name="SQLCLRPermissions"></a>Permissões para projetos Common Language Runtime do SQL Server  
A tabela a seguir lista as permissões que você deve ter para implantar ou depurar projetos de CLR:  
  
|Ações|Permissões necessárias|  
|-----------|------------------------|  
|Implantar (inicial ou incremental) de um assembly de conjunto de permissões de segurança|db_DDLAdmin - essa permissão concede as permissões CREATE e ALTER para os assemblies e tipos de objetos que você implantar<br /><br />VIEW DEFINITION (nível do banco de dados) - necessário à implantação<br /><br />CONNECT (nível do banco de dados) - concede a habilidade de conectar-se ao banco de dados|  
|Implantar um assembly de conjunto de permissões de acesso externo|db_DDLAdmin - essa permissão concede as permissões CREATE e ALTER para os assemblies e tipos de objetos que você implantar<br /><br />VIEW DEFINITION (nível do banco de dados) - necessário à implantação<br /><br />CONNECT (nível do banco de dados) - concede a habilidade de conectar-se ao banco de dados<br /><br />Além disso, você também deve ter:<br /><br />opção TRUSTWORTHY do banco de dados definida como ON<br /><br />O logon que você usa para implantar deve ter a permissão External Access Assembly.|  
|Implantar um assembly de conjunto de permissões inseguro|db_DDLAdmin - essa permissão concede as permissões CREATE e ALTER para os assemblies e tipos de objetos que você implantar<br /><br />VIEW DEFINITION (nível do banco de dados) - necessário à implantação<br /><br />CONNECT (nível do banco de dados) - concede a habilidade de conectar-se ao banco de dados<br /><br />Além disso, você também deve ter:<br /><br />opção TRUSTWORTHY do banco de dados definida como ON<br /><br />O logon que você usa para implantar deve ter a permissão Unsafe Assembly.|  
|Depurar remotamente um assembly do SQL CLR|Você deve ter a permissão de função fixa sysadmin.|  
  
> [!IMPORTANT]  
> Em todos os casos, o proprietário do assembly deve ser o usuário que você está usando para implantar o assembly ou o proprietário deve ser uma função na qual esse usuário é um membro. Esse requisito também se aplica aos assemblies referenciados pelo assembly que você implanta.  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
  
