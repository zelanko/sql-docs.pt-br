---
title: Gerenciamento de pacotes de R para o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: cebafeabd73260f166244e963754a2bd740bfe0f
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="r-package-management-for-sql-server"></a>Gerenciamento de pacotes de R para o SQL Server

Este artigo descreve os recursos para o gerenciamento de pacotes de R no SQL Server 2017 e no SQL Server 2016.

+ Métodos recomendados para o gerenciamento de pacotes de R 
+ Alterações no pacote de gerenciamento entre o SQL Server 2016 e de 2017

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

## <a name="recommended-methods-for-package-management"></a>Métodos recomendados para o gerenciamento de pacotes

No SQL Server 2016 e no SQL Server 2017, um administrador pode instalar pacotes para cada instância em que o aprendizado de máquina tiver sido habilitado. 

Pacotes são instalados no sistema de arquivos, usando bibliotecas de instância e não podem ser compartilhados entre instâncias. Atualmente, isso é o método recomendado para SQL Server 2016 e 2017 do SQL Server.

+ [Instalar pacotes R adicionais no SQL Server](install-additional-r-packages-on-sql-server.md)
+ [Determinar quais pacotes estão instalados no SQL Server](determine-which-packages-are-installed-on-sql-server.md)

Além disso, se você tiver **dbo** associação de função em uma instância do SQL Server onde o aprendizado de máquina tiver sido habilitado, você pode instalar pacotes de R de um cliente remoto, usando novas funções de RevoScaleR.

+ [Novas funções de R para a instalação do pacote](#bkmk_remoteInstall)

### <a name="installation-on-servers-with-no-internet-access"></a>Instalação em servidores sem acesso à Internet

Para tornar mais fácil de determinar as versões necessárias do pacote R e forneça todas as dependências do pacote, você pode usar [miniCRAN](https://mran.microsoft.com/package/miniCRAN). Este pacote de R usa uma lista de pacotes de destino e cria um repositório local que contém os pacotes de destino juntamente com todas as suas dependências, em formato compactado. Você pode copiar que para o servidor off-line, ou compartilhar o repositório entre várias instâncias.

Para obter mais informações, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="python-packages"></a>Pacotes do Python

Instalação de novos pacotes do Python segue as mesmas diretrizes: 

+ Verificar pacotes do Python com antecedência para determinar a compatibilidade com a versão atual do Python
+ Avaliar a adequação de pacote do Python para um ambiente protegido do SQL Server
+ Use as ferramentas Python para instalar os pacotes como administrador
+ Instale os pacotes que devem ser executado no contexto do SQL Server somente na biblioteca de instância. 
+ Se você usar vários ambientes de teste, produção, etc., certifique-se de que a mesma versão do pacote do Python é instalada na biblioteca de instância.

Para etapas de instalação, consulte [instalar novos pacotes de Python no SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="features-for-package-management-in-sql-server-2016-and-sql-server-2017"></a>Recursos para gerenciamento de pacotes no SQL Server 2016 e 2017 do SQL Server

SQL Server 2017 adicionado alguns novos recursos para dar suporte a facilitar o gerenciamento de pacotes de R (e Python) por administradores de banco de dados. Esses novos recursos incluem:

+ A capacidade de instalar ou gerenciar bibliotecas de pacote usando o T-SQL
+ Gerenciamento de permissões de usuário no nível do banco de dados por meio de funções de banco de dados. 

Em versões futuras, esses recursos são deve fornecer o principal método de gerenciamento de pacotes por administradores de banco de dados e tornar mais fácil para os cientistas de dados instalar as bibliotecas necessárias.

Em aproximadamente ao mesmo tempo, o Microsoft R Server e o servidor de aprendizado de máquina adicionadas novas funções de R para tornar mais fácil de instalar e compartilhar pacotes em um contexto de computação do SQL Server. Essas funções operam independentemente dos recursos do SQL Server com base em T-SQL e devem ser executados de um cliente remoto do R.

Esta seção fornece uma visão geral desses recursos.

### <a name="bkmk_remoteInstall"></a>Novas funções de RevoScaleR para a instalação do pacote 

Os usuários com uma versão recente do R Server ou do servidor de aprendizado de máquina também podem usar novas funções no [ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) para instalar os pacotes em uma instância especificada como o contexto de computação do SQL Server.

+ O cientista de dados pode instalar pacotes de R necessários no SQL Server sem ter acesso direto ao computador do SQL Server. No entanto, o usuário deve ser um membro do proprietário do banco de dados (**dbo**) função.

+ O usuário pode compartilhar pacotes com outras pessoas, instalando pacotes com escopo compartilhado. Outros usuários autorizados do mesmo banco de dados do SQL Server podem acessar o pacote.

+ Os usuários podem instalar pacotes privados que não são visíveis para outras pessoas, a criação de uma área restrita privada pacotes R.

+ Sincronização de pacote permite fácil backup e restauração de pacotes

#### <a name="package-installation-functions"></a>Funções de instalação do pacote

As seguintes funções de gerenciamento de pacote são fornecidas em RevoScaleR, para instalação e remoção de pacotes em um contexto de computação especificado:

-   [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages): para obter informações sobre os pacotes instalados no contexto de computação especificado.

-   [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages): instalar os pacotes em um contexto de computação, de um repositório especificado ou lendo salvos localmente compactados pacotes.

-   [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages): remover os pacotes instalados em um contexto de computação.

-   [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage): obter o caminho para um ou mais pacotes no contexto de computação especificado.

-   [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages): copia uma biblioteca de pacote entre o sistema de arquivos e bancos de dados em contextos de computação especificado.

-   [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths): obter o caminho de pesquisa para árvores de biblioteca de pacotes durante a execução dentro do SQL Server.

Para usar essas funções, conecte-se a uma instância do SQL Server em que você tem as permissões necessárias, usando um contexto de computação do SQL Server. 

> [!IMPORTANT]
> As credenciais que você use a conexão determinam se é possível concluir a operação no servidor.

Essas funções de instalação do pacote verificar se há dependências e certifique-se de que todos os pacotes relacionados podem ser instalados no SQL Server, assim como a instalação do pacote de R no contexto de computação local. A função que desinstala pacotes também calcula as dependências e garante que os pacotes que não são mais usados por outros pacotes no SQL Server sejam removidos para liberar recursos.

Essas novas funções são incluídas na versão do RevoScaleR está instalado no SQL Server 2017. Você também pode obter essas funções [atualizando a instância do SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md) para usar uma versão recente do [Microsoft R Server ou o servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server). Requer a versão 9.0.1 ou posterior.

#### <a name="package-synchronization-functions"></a>Funções de sincronização do pacote

Sincronização do pacote é um novo recurso somente pacotes de R. O mecanismo de banco de dados controla os pacotes que são usados por um proprietário específico e um grupo e podem gravar esses pacotes ao sistema de arquivos, se necessário. Normalmente você poderia usar a sincronização do pacote nestes cenários:

+ Você deseja mover os pacotes de R entre instâncias do SQL Server.
+ Você precisa reinstalar pacotes para um usuário específico ou grupo depois que um banco de dados for restaurado.

Para obter mais informações sobre como habilitar e usar esse recurso, consulte [sincronização de pacotes de R para o SQL Server](package-install-uninstall-and-sync.md).

### <a name="package-management-using-t-sql"></a>Gerenciamento de pacotes usando o T-SQL

SQL Server 2017 adicionadas novas instruções T-SQL para dar o DBA mais controle sobre os pacotes de R no nível do banco de dados. O DBA não deve ter que aprender a usar R ou as ferramentas Python, mas em vez disso, deve ser capaz de fornecer aos usuários de R ou Python a capacidade de instalar os pacotes precisam e compartilhá-los com outras pessoas.

Esse recurso destina-se para facilitar o gerenciamento de versão e de colaboração em ambientes multiusuário: por exemplo:

+ Você deseja compartilhar pacotes que você tiver desenvolvido com outras pessoas da sua equipe.
+ Vários analistas estiver trabalhando no mesmo banco de dados e precisem usar versões diferentes do mesmo pacote.
+ Você deseja mover os pacotes e suas permissões ao mesmo tempo que você move um banco de dados, ou quando você executa o backup e restaurar operações.

Gerenciamento de pacotes no SQL Server 2017 se baseia em novos objetos de banco de dados e recursos:

+ [Novas funções de banco de dados](#bkmk_roles), para o gerenciamento de acesso de pacote e usar
+ [Criar biblioteca externa](#bkmk_createExternalLibrary) instrução, para carregar as bibliotecas de pacote para o servidor

O uso desses recursos requer alguma preparação adicional em nível de banco de dados de instância e: 

+  O administrador de banco de dados deve habilitar explicitamente o recurso de gerenciamento de pacote executando um script que cria os objetos de banco de dados necessários. Para obter mais informações, consulte [como habilitar o gerenciamento de pacotes de R](r-package-how-to-enable-or-disable.md).

+ Os usuários devem ser atribuídos a funções, em um nível por banco de dados. Essas funções dar aos usuários a capacidade de instalar pacotes compartilhados ou privados.

+ Bibliotecas de pacote podem ser instaladas usando a nova instrução T-SQL, criar biblioteca externa. No entanto, todas as dependências do pacote devem ser preparadas antecipadamente e instaladas como parte de um único arquivo compactado.

> [!NOTE]
> Embora os recursos descritos aqui são totalmente funcionais no momento, as versões futuras contêm aprimoramentos adicionais para tornar mais fácil de preparar as bibliotecas de pacote e para gerenciar as dependências. Se você estiver familiarizado com a instalação do pacote de R, é recomendável que você continue a usar as ferramentas de R por enquanto.

#### <a name="bkmk_createExternalLibrary"></a>CRIAR BIBLIOTECA EXTERNA 

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

Para garantir que todas as dependências de pacote são fornecidas, é recomendável usar [miniCRAN](create-a-local-package-repository-using-minicran.md) para criar um repositório local. Você pode usar esse arquivo compactado para instalar o pacote de destino e suas dependências.

#### <a name="bkmk_roles"></a>Funções de banco de dados de gerenciamento de pacote 

As novas funções fornecidas no SQL Server para o gerenciamento de pacotes não são incluídas por padrão, mesmo em casos onde o aprendizado de máquina foi instalado e habilitado. Você deve adicionar as funções executando um script conforme descrito aqui: [habilitar ou desabilitar o gerenciamento de pacote](r-package-how-to-enable-or-disable.md).

Depois de executar esse script, você deve ver as novas funções de banco de dados a seguir:

+ `rpkgs-users`: Os membros desta função podem usar qualquer pacote compartilhado que foi instalado por outro `rpkgs-shared` membro da função.

+ `rpkgs-private`: Os membros dessa função têm acesso aos pacotes compartilhados, com as mesmas permissões que os membros do `rpkgs-users` função. Os membros desta função também podem instalar, remover e usar pacotes em particular no escopo.

+ `rpkgs-shared`: Os membros dessa função têm as mesmas permissões que os membros do `rpkgs-private` função. Além disso, os membros desta função podem instalar ou remover pacotes de compartilhado.

+ `db_owner`: Os membros dessa função têm as mesmas permissões que os membros do `rpkgs-shared` função. Além disso, os membros dessa função podem **conceder** outros usuários o direito de instalar ou remover ambos compartilhado e pacotes privados.

O DBA pode adicionar usuários a funções em uma base por banco de dados.



## <a name="next-steps"></a>Próximas etapas

[Gerenciamento de pacotes para o aprendizado de máquina do SQL Server](r-package-management-for-sql-server-r-services.md)
