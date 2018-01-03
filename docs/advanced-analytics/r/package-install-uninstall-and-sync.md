---
title: "Sincronização de pacotes de R para o SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/02/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7530d67c2c74b4918228ea91597f1667c0abbd6
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="r-package-synchronization-for-sql-server"></a>Sincronização de pacotes de R para o SQL Server

SQL Server 2017 inclui a capacidade de sincronizar coleções de pacotes de R entre o sistema de arquivos e a instância e banco de dados onde os pacotes são usados.
Esse recurso foi fornecido para tornar mais fácil de fazer backup de coleções de pacote de R associados a bancos de dados do SQL Server. Usando esse recurso, um administrador pode restaurar não apenas o banco de dados, mas todos os pacotes R que foram usados por cientistas de dados trabalhando nesse banco de dados.

Este tópico descreve o recurso de sincronização do pacote e como usar o [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages) função para executar as seguintes tarefas:

+ Sincronizar uma lista de pacotes para um banco de dados inteiro do SQL Server

+ Sincronizar os pacotes usados por um usuário individual, ou um grupo de usuários

+ Se um usuário for movido para um SQL Server diferente, você pode fazer um backup de banco de dados de trabalho do usuário e restaurá-lo para o novo servidor, e os pacotes para o usuário serão instalados no sistema de arquivos no novo servidor, conforme exigido por R.

Por exemplo, você pode usar a sincronização de pacote nestes cenários:

+ O DBA restaurou a uma instância do SQL Server para uma nova máquina e solicita que os usuários se conectem de seus clientes de R e executar `rxSyncPackages` para atualizar e restaurar seus pacotes.

+ Você acha que um pacote R no sistema de arquivos está corrompido, você executar `rxSyncPackages` no SQL Server.

## <a name="requirements"></a>Requisitos

Antes de você pode usar a sincronização do pacote, você deve ter a versão apropriada do Microsoft R e habilitou o recurso de banco de dados relacionado.

### <a name="determine-whether-your-server-supports-package-management"></a>Determinar se o servidor oferecer suporte a gerenciamento de pacotes

Este recurso está disponível no SQL Server de 2017 CTP 2 ou posterior.

Como esse recurso usa funções de R no Microsoft R version 9.1.0, você pode adicionar esse recurso a uma instância do SQL Server 2016 atualizando a instância para usar a versão mais recente do Microsoft R. Para obter mais informações, consulte [SqlBindR.exe usado para atualizar o SQL Server R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="enable-the-package-management-feature"></a>Habilitar o recurso de gerenciamento de pacote

Para usar a sincronização de pacote requer que os novos recursos de gerenciamento do pacote ser habilitado na instância do SQL Server e bancos de dados individuais usados para executar tarefas de R.

1. O administrador do servidor permite que o recurso para a instância do SQL Server.
2. Para cada banco de dados, o administrador concede aos usuários a capacidade de instalar ou compartilhamento de pacotes de R.

Quando isso for feito, informações sobre usuários e os pacotes que eles já têm instalado são armazenadas na instância do SQL Server. Essas informações podem ser aplicadas, em seguida, para atualizar os pacotes de R no sistema de arquivos.

Sempre que você adicionar um novo pacote usando as funções de gerenciamento de pacote, ambos os registros no SQL Server e o sistema de arquivos são atualizados.

> [!NOTE]
> Você não pode usar a sincronização de pacote se você vem instalando pacotes de R a maneira tradicional, usando ferramentas de R para instalar os pacotes diretamente no sistema de arquivos.
### <a name="permissions"></a>Permissões

+ A pessoa que executa a função de sincronização do pacote deve ser um objeto na instância do SQL Server e banco de dados que tem os pacotes de segurança.

+ O chamador da função deve ser um membro de uma dessas funções de gerenciamento de pacote: **compartilhado rpkgs** ou **rpkgs particular**.

+ Para sincronizar os pacotes marcados como **compartilhado**, a pessoa que está executando a função deve estar associado a **compartilhado rpkgs** função e os pacotes que estão sendo movidos devem ter sido instalado para compartilhado biblioteca de escopo.

+ Para sincronizar os pacotes marcados como **privada**, seja o proprietário do pacote ou o administrador deve executar a função e os pacotes devem ser privados.

+ Para sincronizar os pacotes em nome de outros usuários, o proprietário deve ser um membro do **db_owner** função de banco de dados.

## <a name="how-package-synchronization-works"></a>Como funciona a sincronização do pacote

Para usar a sincronização do pacote, chame [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), que é uma nova função no [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler). Você pode chamar essa função do SQL Server usando sp_execute_external_script, ou você pode executá-lo de um cliente remoto do R e especificar o contexto de computação do SQL Server. 

Como os pacotes são gerenciados no nível do banco de dados, cada chamada para `rxSyncPackages`, você deve especificar uma instância do SQL Server e banco de dados e, em seguida, listar os pacotes ou especifique o escopo do pacote.

1. Criar o contexto de computação do SQL Server usando o `RxInSqlServer` função. Se você não especificar um contexto de computação, o contexto de computação atual será usado.

2. Forneça o nome de um banco de dados na instância no contexto de computação especificado. Pacotes são gerenciados por banco de dados.

3. Lista os pacotes para sincronizar.

4.  Opcionalmente, use o *escopo* argumento para indicar se você estiver sincronizando pacotes para um único usuário ou para um grupo de usuários. Se você executar a função sem especificar um **privada** ou **compartilhado** escopo, todo o conjunto de pacotes disponíveis para todos os escopos e os usuários serão copiados.

Se o comando for executado com êxito, os pacotes existentes no sistema de arquivos são adicionados ao banco de dados, com o escopo especificado e o proprietário. Se o sistema de arquivos está corrompido, os pacotes são restaurados com base na lista mantida no banco de dados.

### <a name="example-1-synchronize-all-package-by-database"></a>Exemplo 1. Sincronizar todos os pacotes por banco de dados

Este exemplo obtém todos os pacotes instalados no banco de dados [TestDB]. Como nenhum proprietário é específico, a lista inclui todos os pacotes que foram instalados para escopos privados e compartilhados.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>Exemplo 2. Restringir pacotes sincronizados por escopo

Os exemplos a seguir sincronizam apenas os pacotes no escopo especificado.

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>Exemplo 3. Restringir pacotes sincronizados pelo proprietário

O exemplo a seguir demonstra como obter apenas os pacotes que foram instalados para um usuário específico. Neste exemplo, o usuário é identificado pelo nome de logon do SQL, *user1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

### <a name="example-4-restrict-synchronized-packages-by-owner"></a>Exemplo 4. Restringir pacotes sincronizados pelo proprietário

O exemplo a seguir sincroniza os pacotes instalados no sistema de arquivos com a lista de pacotes gerenciados no banco de dados. Se qualquer pacote estiver ausente, ele é instalado no sistema de arquivos.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="related-resources"></a>Recursos relacionados

[Gerenciamento de pacotes R para SQL Server](r-package-management-for-sql-server-r-services.md)
