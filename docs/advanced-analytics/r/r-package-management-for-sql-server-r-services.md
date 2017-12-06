---
title: Gerenciamento de pacotes de R para o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 10/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5cd3924b79ce5d33adf88bb6c7c267cdc43a3418
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="r-package-management-for-sql-server"></a>Gerenciamento de pacotes de R para o SQL Server

Este artigo descreve os recursos para o gerenciamento de pacotes de R no SQL Server 2017 e SQL Server 2016.

+ Alterações nos métodos de instalação de pacote de R entre 2016 e de 2017
+ Métodos recomendados para o gerenciamento de pacotes de R
+ Novas funções de banco de dados para o gerenciamento de pacote no SQL Server 2017
+ Nova instrução T-SQL para o gerenciamento de pacote no SQL Server 2017

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

## <a name="differences-in-package-management-between-sql-server-2016-and-sql-server-2017"></a>Diferenças entre o gerenciamento de pacote entre o SQL Server 2016 e o SQL Server 2017

Em **SQL Server 2017**, você pode habilitar o gerenciamento de pacotes no nível de instância e gerenciar permissões de usuário para adicionar ou usar os pacotes no nível do banco de dados.

Isso requer que o administrador de banco de dados habilitar o recurso de gerenciamento de pacote executando um script que cria os objetos de banco de dados necessários. Para obter mais informações, consulte [como habilitar o gerenciamento de pacotes de R](r-package-how-to-enable-or-disable.md).

Em **SQL Server 2016**, um administrador deve instalar pacotes R na biblioteca R associada à instância. Todos os usuários que estão executando o código R na instância usam esses pacotes. Código de R em execução no SQL server não pode usar pacotes instalados em bibliotecas de usuário. No entanto, o administrador pode conceder a usuários individuais a capacidade de executar scripts R em um banco de dados específico.

**Resumo das diferenças e vantagens**

+ Se você estiver usando serviços de aprendizado de máquina em 2017 do SQL Server, você pode gerenciar e instalar pacotes de R usando o método tradicional, com base em ferramentas de R, ou usando as novas funções de banco de dados e instruções T-SQL.

+ É recomendável que o último método, porque ele fornece um controle mais refinado por administradores, juntamente com mais liberdade para usuários. Por exemplo, os usuários podem instalar seus próprios pacotes, usando um procedimento armazenado ou por meio de código R e o compartilhamento de pacotes com outras pessoas. 

    Como pacotes podem ser definidos para um banco de dados, e cada usuário obtenha uma área restrita do pacote isolado, é mais fácil de instalar versões diferentes do mesmo pacote de R. Você pode facilmente copiar ou mover os usuários e seus pacotes entre bancos de dados. 

+ Uso do recurso de gerenciamento de pacote no SQL Server torna muito mais fácil a operações de backup e restauração. Ao migrar seu banco de dados do trabalho para um novo servidor, você pode usar a função de sincronização do pacote para ler uma lista de todos os seus pacotes e instalá-los em um banco de dados no novo servidor.

+ Talvez seja mais conveniente para instalar pacotes de R como um administrador no computador, usando ferramentas tradicionais de R, se você for a única pessoa usando o servidor para trabalhos de aprendizado de máquina.

+ Se você estiver usando o SQL Server 2016 R Services, você deve continuar a instalar os pacotes de R usados pela instância usando ferramentas de R > Certifique-se de usar a biblioteca de R associada com a instância.

As seções a seguir fornecem mais detalhes sobre como o gerenciamento de pacotes é realizada usando essas duas opções.

## <a name="r-package-management-using-t-sql"></a>Gerenciamento de pacotes de R usando o T-SQL

SQL Server 2017 inclui novas instruções T-SQL que oferecem o DBA mais controle sobre os pacotes de R no nível do banco de dados. Ao mesmo tempo, o DBA pode dar aos usuários a capacidade de instalar os pacotes precisam e compartilhá-los com outras pessoas.

Se você precisa compartilhar pacotes com outras pessoas, ou se precisam de várias pessoas executar tarefas de aprendizado de máquina do servidor, recomendamos que você habilite o gerenciamento de pacotes, atribuir usuários a funções de banco de dados e carregar pacotes de forma que os usuários possam compartilhá-las.

Gerenciamento de pacotes no SQL Server 2017 se baseia em novos objetos de banco de dados e recursos:

+ Novas funções de banco de dados, para gerenciar o acesso de pacote e uso
+ Escopo do pacote, separado compartilhado e pacotes privados
+ Instrução Criar biblioteca externa, para carregar novas bibliotecas de código para o servidor
+ Contexto de computação de novas funções de R RevoScaleR para oferecer suporte a instalação de pacotes em um SQL Server
+ Sincronização de pacotes, para garantir o backup fácil e restauração de pacotes

### <a name="database-roles-for-package-management"></a>Funções de banco de dados para gerenciamento de pacotes

O administrador de banco de dados deve criar as funções usadas para gerenciamento de pacote executando um script conforme descrito aqui: [habilitar ou desabilitar o gerenciamento de pacote](r-package-how-to-enable-or-disable.md).

Depois de executar esse script, você deve ver as novas funções de banco de dados a seguir:

+ `rpkgs-users`: Os membros desta função podem usar qualquer pacote compartilhado que foi instalado por outro `rpkgs-shared` membro da função.

+ `rpkgs-private`: Os membros dessa função têm acesso aos pacotes compartilhados, com as mesmas permissões que os membros do `rpkgs-users` função. Os membros desta função também podem instalar, remover e usar pacotes em particular no escopo.

+ `rpkgs-shared`: Os membros dessa função têm as mesmas permissões que os membros do `rpkgs-private` função. Além disso, os membros desta função podem instalar ou remover pacotes de compartilhado.

+ `db_owner`: Os membros dessa função têm as mesmas permissões que os membros do `rpkgs-shared` função. Além disso, os membros dessa função podem **conceder** outros usuários o direito de instalar ou remover ambos compartilhado e pacotes privados.

O DBA adiciona usuários às funções em uma base por banco de dados, para controlar a capacidade do usuário para instalar pacotes.

### <a name="package-scope"></a>Escopo do pacote

Os novos recursos de gerenciamento de pacote distinguem pacotes se eles são particulares ou podem ser compartilhados por vários usuários.

+ **Escopo compartilhado**

    *Escopo compartilhado* significa que os usuários que receberam permissão para a função de escopo compartilhado (`rpkgs-shared`) pode instalar e desinstalar pacotes para um banco de dados especificado. Um pacote que é instalado em uma biblioteca de escopo compartilhado pode ser usado por outros usuários do banco de dados do SQL Server, contanto que esses usuários tenham permissão para usar pacotes de R instalados.

+ **Escopo particular**

    *Escopo particular* significa que os usuários que receberam associação na função de escopo particular (`rpkgs-private`) pode instalar ou desinstalar pacotes em um local de biblioteca particular definido por usuário. Portanto, todos os pacotes instalados no escopo particular podem ser usados somente pelo usuário que os instalou. Em outras palavras, um usuário do SQL Server não pode usar pacotes particulares que foram instalados por outro usuário.

Esses modelos de escopo *compartilhado* e *particular* podem ser combinados para desenvolver sistemas seguros personalizados para implantar e gerenciar pacotes no SQL Server.

Por exemplo, ao usar o escopo compartilhado, o líder ou o gerente de um grupo de cientistas de dados pode receber permissão para instalar pacotes e esses pacotes podem ser usados por todos os outros usuários ou os cientistas de dados na mesma instância do SQL Server.

Outro cenário poderia exigir maior isolamento entre usuários, ou o uso de diferentes versões de pacotes. Nesse caso, o escopo particular pode ser usado para fornecer permissões individuais aos cientistas de dados, que seriam responsáveis por instalar e usar apenas os pacotes que precisam. Como os pacotes são instalados em uma base individual, os pacotes instalados por um usuário não afetariam o trabalho de outros usuários que estão usando o mesmo banco de dados do SQL Server.

### <a name="create-external-library"></a>CRIAR BIBLIOTECA EXTERNA

O [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) é uma nova instrução T-SQL, introduzida no SQL Server 2017 para ajudar o administrador de banco de dados a trabalhar com pacotes sem a necessidade de ferramentas de R de usuário. 

Você usa o **criar biblioteca externa** instrução carregar bibliotecas externas para uma instância no formato de arquivo compactado. Os usuários autorizados, em seguida, podem acessar as bibliotecas e instalá-los para seu próprio uso.

Por exemplo, você pode criar várias cópias do seu projeto de R, cada uma para uma versão diferente. Carregando-os como bibliotecas separadas permite manter algumas versões particulares e compartilhar algumas versões com outros usuários.

"Biblioteca" é basicamente uma coleção de pacotes externos que você deseja disponibilizar para os usuários em um único nome. Por exemplo, você pode publicar qualquer um dos seguintes para o SQL Server como uma biblioteca externa:

+ Um único pacote de R que você escreveu, sem dependências
+ Um pacote que você deseja instalar e dependências necessárias para a instalação
+ Uma coleção de pacotes de R relacionado a uma tarefa específica ou projeto, com suas dependências

O nome da biblioteca é para gerenciar o pacote ou uma coleção de pacotes no SQL Server e pode ser independente dos pacotes que estão instalados. No entanto, os nomes de biblioteca devem ser exclusivos em uma instância.

Para usar esta instrução, o recurso de gerenciamento de pacote deve ter sido habilitado na instância. Para obter mais informações, consulte [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

> [!NOTE]
> No momento, você pode usar essa instrução para criar bibliotecas somente baseados no Windows para suporte de r está planejado no futuro para pacotes do Python e para pacotes que executam em outras plataformas, como o Linux.

Depois que a biblioteca externa foi carregada para o servidor, você deve instalá-lo para a biblioteca de pacote de R associada com a instância. Há várias maneiras de fazer isso:

+ Execute o comando de R padrão `install.packages` em sp_execute_external_script. Certifique-se de conectar-se usando uma conta que tenha permissões para instalar pacotes.

+ Conecte-se ao SQL Server de um cliente remoto do R e executar [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) no contexto de computação do SQL Server. Novamente, você deve ter permissões para instalar os pacotes no escopo particular ou compartilhado para fazer isso.

Para ver exemplos de instalação usando o T-SQL e R, consulte [instalar outros pacotes no SQL Server](install-additional-r-packages-on-sql-server.md).

### <a name="new-r-functions-for-package-installation"></a>Novas funções de R para a instalação do pacote

Depois que as funções de banco de dados de gerenciamento de pacote foram habilitadas, os usuários também podem usar novas funções no [ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) para instalar os pacotes na instância especificada como o contexto de computação do SQL Server.

+ O cientista de dados pode instalar pacotes de R necessários no SQL Server sem ter acesso direto ao computador do SQL Server.

+ Um usuário pode instalar um pacote e compartilhar com outras pessoas, instalando o pacote com escopo compartilhado. Em seguida, outros usuários autorizados do mesmo banco de dados do SQL Server podem acessar o pacote.

+ Os usuários podem instalar pacotes privados que não são visíveis para outras pessoas, a criação de uma área restrita privada pacotes R.

As seguintes funções de gerenciamento de pacote são fornecidas em RevoScaleR, para instalação e remoção de pacotes em um contexto de computação especificado:

-   [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages): para obter informações sobre os pacotes instalados no contexto de computação especificado.

-   [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages): instalar os pacotes em um contexto de computação, de um repositório especificado ou lendo salvos localmente compactados pacotes.

-   [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages): remover os pacotes instalados em um contexto de computação.

-   [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage): obter o caminho para um ou mais pacotes no contexto de computação especificado.

-   [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages): copia uma biblioteca de pacote entre o sistema de arquivos e bancos de dados em contextos de computação especificado.

-   [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): obter o caminho de pesquisa para árvores de biblioteca de pacotes durante a execução dentro do SQL Server.

Para usar essas funções, conecte-se a uma instância do SQL Server em que você tem as permissões necessárias, usando um contexto de computação do SQL Server. Quando você se conectar, suas credenciais de determinam se é possível concluir a operação no servidor.

As funções de instalação do pacote verificam se há dependências e certificam-se de que todos os pacotes relacionados possam ser instalados no SQL Server, assim como a instalação de pacote do R no contexto de computação local. A função que desinstala pacotes também calcula as dependências e garante que os pacotes que não são mais usados por outros pacotes no SQL Server sejam removidos para liberar recursos.

> [!NOTE]
> 
> Essas novas funções são incluídas por padrão no SQL Server 2017. Você pode atualizar sua versão do RevoScaleR para obter essas funções ao atualizar a instância para usar uma versão posterior do Microsoft R Server, como o Microsoft R Server 9.0.1.
> 
> Para obter mais informações, consulte [SqlBindR.exe usando a atualizador](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="synchronization-of-r-package-libraries"></a>Sincronização das bibliotecas de pacote de R

A versão do CTP 2.0 do SQL Server 2017 (e a versão de abril de 2017 do Microsoft R Server) incluem novas funções de R para *sincronizando pacotes*.

A sincronização do pacote significa que o mecanismo de banco de dados controla os pacotes que são usados por um proprietário específico e um grupo e podem gravar esses pacotes ao sistema de arquivos, se necessário. Você pode usar a sincronização do pacote nestes cenários:

+ Você deseja mover os pacotes de R entre instâncias do SQL Server.
+ Você precisa reinstalar pacotes para um usuário específico ou grupo depois que um banco de dados for restaurado.

Para obter mais informações sobre como habilitar e usar esse recurso, consulte [sincronização de pacotes de R para o SQL Server](package-install-uninstall-and-sync.md).

## <a name="r-package-management-using-traditional-r-tools"></a>Gerenciamento de pacotes de R usando ferramentas tradicionais de R

O método tradicional de gerenciamento de pacotes de R em uma instância é instalar e listar os pacotes por meio de comandos e ferramentas de R. 

+ Essa opção pode ser a única opção se você estiver usando uma versão mais recente do SQL Server 2016.  
+ Essa opção também pode ser conveniente se você for o único usuário pacotes de R e ter acesso administrativo ao servidor.
+ Para facilitar o gerenciamento versões de pacote de R, você pode usar [miniCRAN](create-a-local-package-repository-using-minicran.md) para criar um repositório local e compartilhá-la entre instâncias.

Para obter detalhes, consulte estes artigos:

+ [Instalar pacotes R adicionais no SQL Server](install-additional-r-packages-on-sql-server.md)
+ [Determinar quais pacotes estão instalados no SQL Server](determine-which-packages-are-installed-on-sql-server.md)

Para o SQL Server 2017, recomendamos que você use criar biblioteca externa e as funções de banco de dados fornece para gerenciar usuários e seus pacotes de R.

## <a name="next-steps"></a>Próximas etapas

[Como habilitar ou desabilitar o gerenciamento de pacotes de R](../r/r-package-how-to-enable-or-disable.md)
