---
title: Sincronização de pacote R do sistema de arquivos
description: Atualize as bibliotecas de R no SQL Server com versões mais recentes instaladas no sistema de arquivos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 86e170caab47df6f3644881925ea0997ea812365
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345268"
---
# <a name="r-package-synchronization-for-sql-server"></a>Sincronização de pacote R para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A versão do RevoScaleR incluída no SQL Server 2017 inclui a capacidade de sincronizar coleções de pacotes de R entre o sistema de arquivos e a instância e o banco de dados em que os pacotes são usados.

Esse recurso foi fornecido para facilitar o backup de coleções de pacotes de R associadas a bancos de dados do SQL Server. Usando esse recurso, um administrador pode restaurar não apenas o banco de dados, mas todos os pacotes do R que foram usados por cientistas de data trabalhando nesse banco de dado.

Este artigo descreve o recurso de sincronização de pacote e como usar a função [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) para executar as seguintes tarefas:

+ Sincronizar uma lista de pacotes para um banco de dados SQL Server inteiro

+ Sincronizar pacotes usados por um usuário individual ou por um grupo de usuários

+ Se um usuário mudar para um SQL Server diferente, você poderá fazer um backup do banco de dados de trabalho do usuário e restaurá-lo para o novo servidor, e os pacotes para o usuário serão instalados no sistema de arquivos no novo servidor, conforme exigido pelo R.

Por exemplo, você pode usar a sincronização de pacote nesses cenários:

+ O DBA restaurou uma instância do SQL Server em um novo computador e solicita que os usuários se conectem de seus clientes `rxSyncPackages` de R e executem para atualizar e restaurar seus pacotes.

+ Você considera que um pacote R no sistema de arquivos está corrompido, `rxSyncPackages` portanto, você executa o SQL Server.

## <a name="requirements"></a>Requisitos

Para poder usar a sincronização de pacote, você deve ter a versão apropriada do Microsoft R ou Machine Learning Server. Esse recurso é fornecido no Microsoft R versão 9.1.0 ou posterior. 

Você também deve habilitar o [recurso de gerenciamento de pacotes](r-package-how-to-enable-or-disable.md) no servidor.

### <a name="determine-whether-your-server-supports-package-management"></a>Determinar se o servidor dá suporte ao gerenciamento de pacotes

Esse recurso está disponível no SQL Server 2017 CTP 2 ou posterior.

Você pode adicionar esse recurso a uma instância do SQL Server 2016 atualizando a instância do para usar a versão mais recente do Microsoft R. Para obter mais informações, consulte [usar Sqlbindr. exe para atualizar SQL Server R Services](../install/upgrade-r-and-python.md).

### <a name="enable-the-package-management-feature"></a>Habilitar o recurso de gerenciamento de pacotes

Para usar a sincronização de pacote, é necessário que o novo recurso de gerenciamento de pacotes esteja habilitado na instância do SQL Server e em bancos de dados individuais. Para obter mais informações, consulte [habilitar ou desabilitar o gerenciamento de pacotes para SQL Server](r-package-how-to-enable-or-disable.md).

1. O administrador do servidor habilita o recurso para a instância de SQL Server.
2. Para cada banco de dados, o administrador concede aos usuários individuais a capacidade de instalar ou compartilhar pacotes de R usando funções de banco de dados.

Quando isso for feito, você poderá usar as funções RevoScaleR, como [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) para instalar pacotes em um banco de dados.  As informações sobre os usuários e os pacotes que eles podem usar são armazenadas na instância do SQL Server. 

Sempre que você adicionar um novo pacote usando as funções de gerenciamento de pacote, os registros em SQL Server e no sistema de arquivos serão atualizados. Essas informações podem ser usadas para restaurar informações de pacote para todo o banco de dados.

### <a name="permissions"></a>Permissões

+ A pessoa que executa a função de sincronização de pacote deve ser uma entidade de segurança na instância de SQL Server e no banco de dados que tem os pacotes.

+ O chamador da função deve ser um membro de uma dessas funções de gerenciamento de pacote: **rpkgs-Shared** ou **rpkgs-Private**.

+ Para sincronizar os pacotes marcados como **compartilhados**, a pessoa que está executando a função deve ter a associação na função **rpkgs-Shared** e os pacotes que estão sendo movidos devem ter sido instalados em uma biblioteca de escopo compartilhado.

+ Para sincronizar os pacotes marcados como **particulares**, o proprietário do pacote ou o administrador deve executar a função, e os pacotes devem ser privados.

+ Para sincronizar pacotes em nome de outros usuários, o proprietário deve ser um membro da função de banco de dados **db_owner** .

## <a name="how-package-synchronization-works"></a>Como funciona a sincronização de pacotes

Para usar a sincronização do pacote, chame [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), que é uma nova função no [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). 

Para cada chamada para `rxSyncPackages`, você deve especificar uma SQL Server instância e um banco de dados. Em seguida, liste os pacotes a serem sincronizados ou especifique o escopo do pacote.

1. Crie o SQL Server contexto de computação usando a `RxInSqlServer` função. Se você não especificar um contexto de computação, o contexto de computação atual será usado.

2. Forneça o nome de um banco de dados na instância no contexto de computação especificado. Os pacotes são sincronizados por banco de dados.

3. Especifique os pacotes a serem sincronizados usando o argumento Scope.

    Se você usar escopo **privado** , somente os pacotes pertencentes ao proprietário especificado serão sincronizados. Se você especificar o escopo **compartilhado** , todos os pacotes não privados no banco de dados serão sincronizados. 
    
    Se você executar a função sem especificar o escopo **privado** ou **compartilhado** , todos os pacotes serão sincronizados.

4. Se o comando for bem-sucedido, os pacotes existentes no sistema de arquivos serão adicionados ao banco de dados, com o escopo e o proprietário especificados.

    Se o sistema de arquivos estiver corrompido, os pacotes serão restaurados com base na lista mantida no banco de dados.

    Se o recurso de gerenciamento de pacotes não estiver disponível no banco de dados de destino, um erro será gerado: "O recurso de gerenciamento de pacotes não está habilitado no SQL Server ou a versão é muito antiga"

### <a name="example-1-synchronize-all-package-by-database"></a>Exemplo 1. Sincronizar todos os pacotes por banco de dados

Este exemplo obtém quaisquer pacotes novos do sistema de arquivos local e instala os pacotes no banco de dados [TestDB]. Como nenhum proprietário é específico, a lista inclui todos os pacotes que foram instalados para escopos privados e compartilhados.

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

O exemplo a seguir demonstra como sincronizar somente os pacotes que foram instalados para um usuário específico. Neste exemplo, o usuário é identificado pelo nome de logon do SQL, *Usuário1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>Recursos relacionados

[Gerenciamento de pacotes R para SQL Server](install-additional-r-packages-on-sql-server.md)
