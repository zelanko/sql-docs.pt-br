---
title: Sincronização do pacote R por meio do sistema de arquivos
description: Atualize as bibliotecas R no SQL Server com as versões mais recentes instaladas no sistema de arquivos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 71ff0b6232eb69af7e5e138d2681f8126a12d915
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74485251"
---
# <a name="r-package-synchronization-for-sql-server"></a>Sincronização de pacotes R para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A versão do RevoScaleR incluída no SQL Server 2017 abrange a capacidade de sincronizar coleções de pacotes R entre o sistema de arquivos e a instância e o banco de dados em que os pacotes são usados.

Esse recurso foi fornecido para facilitar o backup de coleções de pacotes R associadas aos bancos de dados do SQL Server. Usando esse recurso, um administrador pode restaurar não apenas o banco de dados, mas todos os pacotes R que foram usados por cientistas que trabalham nesse banco de dados.

Este artigo descreve o recurso de sincronização de pacotes e como usar a função [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) para executar as seguintes tarefas:

+ Sincronizar uma lista de pacotes de um banco de dados inteiro do SQL Server

+ Sincronizar pacotes usados por um usuário individual ou por um grupo de usuários

+ Se um usuário mudar para um SQL Server diferente, você poderá fazer um backup do banco de dados de trabalho do usuário e restaurá-lo no novo servidor. Os pacotes do usuário serão instalados no sistema de arquivos no novo servidor, conforme exigido por R.

Por exemplo, você pode usar a sincronização de pacotes nos seguintes cenários:

+ Caso o DBA tenha restaurado uma instância do SQL Server em uma nova máquina e solicitar aos usuários que se conectem a partir de seus clientes R e executem `rxSyncPackages` para atualizar e restaurar seus pacotes.

+ Caso você ache que um pacote R no sistema de arquivos está corrompido e, portanto, execute `rxSyncPackages` no SQL Server.

## <a name="requirements"></a>Requisitos

Para usar a sincronização de pacotes, é necessário ter a versão apropriada do Microsoft R ou do Machine Learning Server. Esse recurso é fornecido no Microsoft R versão 9.1.0 ou posterior. 

Também é necessário ativar o [recurso de gerenciamento de pacotes](r-package-how-to-enable-or-disable.md) no servidor.

### <a name="determine-whether-your-server-supports-package-management"></a>Determine se o seu servidor dará suporte ao gerenciamento de pacotes

Esse recurso está disponível no SQL Server 2017 CTP 2 ou posterior.

Você pode adicionar esse recurso a uma instância do SQL Server 2016 atualizando a instância para usar a versão mais recente do Microsoft R. Para obter mais informações, confira [Usar SqlBindR.exe para atualizar o SQL Server R Services](../install/upgrade-r-and-python.md).

### <a name="enable-the-package-management-feature"></a>Habilite o recurso de gerenciamento de pacotes

Para usar a sincronização de pacotes, é necessário ativar o novo recurso de gerenciamento de pacotes na instância do SQL Server e em bancos de dados individuais. Para obter mais informações, confira [Habilitar ou desabilitar o gerenciamento de pacotes para o SQL Server](r-package-how-to-enable-or-disable.md).

1. O administrador do servidor habilita o recurso para a instância do SQL Server.
2. Para cada banco de dados, o administrador concede a usuários individuais a capacidade de instalar ou compartilhar pacotes R, usando funções de banco de dados.

Quando isso é feito, você pode usar as funções do RevoScaleR, como [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages), para instalar pacotes em um banco de dados.  As informações sobre os usuários e os pacotes que eles podem usar são armazenadas na instância do SQL Server. 

Sempre que você adiciona um novo pacote usando as funções de gerenciamento de pacotes, os registros no SQL Server e no sistema de arquivos são atualizados. Essas informações podem ser usadas para restaurar as informações do pacote para todo o banco de dados.

### <a name="permissions"></a>Permissões

+ A pessoa que executa a função de sincronização de pacotes deve ser uma entidade de segurança na instância e no banco de dados do SQL Server que contém os pacotes.

+ O responsável pela chamada da função deve ser membro de uma destas funções de gerenciamento de pacotes: **rpkgs-shared** ou **rpkgs-private**.

+ Para sincronizar pacotes marcados como **compartilhado**, a pessoa que está executando a função deve ser membro da função **rpkgs-shared**, e os pacotes que estão sendo movidos devem ter sido instalados em uma biblioteca de escopo compartilhada.

+ Para sincronizar pacotes marcados como **privado**, o proprietário ou o administrador do pacote deve executar a função, e os pacotes devem ser marcados como privados.

+ Para sincronizar pacotes em nome de outros usuários, o proprietário deve ser membro da função de banco de dados **db_owner**.

## <a name="how-package-synchronization-works"></a>Como a sincronização de pacotes funciona

Para usar a sincronização de pacotes, chame [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), que é uma nova função no [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). 

Para cada chamada para `rxSyncPackages`, é necessário especificar uma instância e um banco de dados do SQL Server. Em seguida, liste os pacotes a serem sincronizados ou especifique o escopo do pacote.

1. Crie o contexto de computação do SQL Server usando a função `RxInSqlServer`. Se você não especificar um contexto de computação, o contexto de computação atual será usado.

2. Forneça o nome de um banco de dados na instância no contexto de computação especificado. Os pacotes são sincronizados por banco de dados.

3. Especifique os pacotes a serem sincronizados usando o argumento de escopo.

    Se você usar o escopo **privado**, apenas os pacotes pertencentes ao proprietário especificado serão sincronizados. Se você especificar o escopo **compartilhado**, todos os pacotes não privados no banco de dados serão sincronizados. 
    
    Se você executar a função sem especificar o escopo **privado** ou **compartilhado**, todos os pacotes serão sincronizados.

4. Se o comando for bem-sucedido, os pacotes existentes no sistema de arquivos serão adicionados ao banco de dados, com o escopo e o proprietário especificados.

    Se o sistema de arquivos estiver corrompido, os pacotes serão restaurados com base na lista mantida no banco de dados.

    Se o recurso de gerenciamento de pacotes não estiver disponível no banco de dados de destino, será gerado um erro: "O recurso de gerenciamento de pacotes não está habilitado no SQL Server ou a versão é muito antiga"

### <a name="example-1-synchronize-all-package-by-database"></a>Exemplo 1. Sincronizar todos os pacotes por banco de dados

Este exemplo obtém quaisquer novos pacotes do sistema de arquivos local e instala os pacotes no banco de dados [TestDB]. Como nenhum proprietário foi especificado, a lista inclui todos os pacotes que foram instalados para escopos privados e compartilhados.

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

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>Exemplo 3. Restringir pacotes sincronizados por proprietário

O exemplo a seguir demonstra como sincronizar apenas os pacotes que foram instalados para um usuário específico. Neste exemplo, o usuário é identificado pelo nome de login do SQL, *user1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>Recursos relacionados

[Gerenciamento de pacotes R para SQL Server](install-additional-r-packages-on-sql-server.md)