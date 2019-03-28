---
title: Sincronização de pacotes de R do sistema de arquivos - serviços do SQL Server Machine Learning
description: Atualize bibliotecas do R no SQL Server com as versões mais recentes instaladas no sistema de arquivos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 57677e8d7573411be2e77baa7ffd8564ec9cbeb4
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511353"
---
# <a name="r-package-synchronization-for-sql-server"></a>Sincronização de pacotes de R para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A versão do RevoScaleR incluído no SQL Server 2017 inclui a capacidade de sincronizar coleções de pacotes de R entre o sistema de arquivos e a instância e banco de dados onde os pacotes são usados.

Esse recurso foi fornecido para tornar mais fácil fazer backup de coleções de pacote de R associados a bancos de dados do SQL Server. Usando esse recurso, um administrador pode restaurar não apenas o banco de dados, mas todos os pacotes R que foram usados por cientistas de dados trabalhando nesse banco de dados.

Este artigo descreve o recurso de sincronização de pacotes e como usar o [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) função para executar as seguintes tarefas:

+ Sincronizar uma lista de pacotes para um banco de dados inteiro do SQL Server

+ Sincronizar pacotes usados por um usuário individual, ou um grupo de usuários

+ Se um usuário move para um SQL Server diferente, você pode fazer um backup de banco de dados de trabalho do usuário e restaurá-lo para o novo servidor, e os pacotes para o usuário serão instalados no sistema de arquivos no novo servidor, conforme exigido pelo R.

Por exemplo, você pode usar a sincronização de pacotes nestes cenários:

+ O DBA tiver restaurado uma instância do SQL Server para um novo computador e solicitam que os usuários para conectar-se dos seus clientes de R e executar `rxSyncPackages` para atualizar e restaurar seus pacotes.

+ Você acha que um pacote de R no sistema de arquivos está corrompido, portanto você executar `rxSyncPackages` no SQL Server.

## <a name="requirements"></a>Requisitos

Antes de você pode usar a sincronização de pacote, você deve ter a versão apropriada do Microsoft R ou Machine Learning Server. Esse recurso é fornecido no Microsoft R version 9.1.0 ou posterior. 

Você também deve habilitar o [recurso de gerenciamento de pacotes](r-package-how-to-enable-or-disable.md) no servidor.

### <a name="determine-whether-your-server-supports-package-management"></a>Determinar se o servidor dá suporte a gerenciamento de pacotes

Esse recurso está disponível no SQL Server 2017 CTP 2 ou posterior.

Você pode adicionar esse recurso a uma instância do SQL Server 2016, atualizando a instância para usar a versão mais recente do Microsoft R. Para obter mais informações, consulte [SqlBindR.exe Use para atualizar o SQL Server R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="enable-the-package-management-feature"></a>Habilitar o recurso de gerenciamento de pacote

Para usar a sincronização do pacote requer que o novo recurso de gerenciamento de pacote ser habilitada na instância do SQL Server e nos bancos de dados individuais. Para obter mais informações, consulte [habilitar ou desabilitar o pacote de gerenciamento para SQL Server](r-package-how-to-enable-or-disable.md).

1. O administrador do servidor permite que o recurso para a instância do SQL Server.
2. Para cada banco de dados, o administrador concede a usuários individuais a capacidade de instalar ou compartilhar pacotes de R, usando funções de banco de dados.

Quando isso for feito, você pode usar funções de RevoScaleR, tais como [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) para instalar os pacotes em um banco de dados.  Informações sobre usuários e os pacotes que eles podem usar são armazenadas na instância do SQL Server. 

Sempre que você adicionar um novo pacote usando as funções de gerenciamento de pacote, ambos os registros no SQL Server e o sistema de arquivos são atualizados. Essas informações podem ser usadas para restaurar as informações de pacote para o banco de dados inteiro.

### <a name="permissions"></a>Permissões

+ A pessoa que executa a função de sincronização do pacote deve ser um objeto na instância do SQL Server e banco de dados que tem os pacotes de segurança.

+ O chamador da função deve ser um membro de uma dessas funções de gerenciamento de pacote: **rpkgs-shared** ou **rpkgs-private**.

+ Sincronizar pacotes marcados como **compartilhada**, a pessoa que está executando a função deve estar associado a **rpkgs-shared** função e os pacotes que estão sendo movidos devem ter sido instalado para um compartilhamento biblioteca de escopo.

+ Sincronizar pacotes marcados como **privada**, seja o proprietário do pacote ou o administrador deve executar a função e os pacotes devem ser privados.

+ Para sincronizar os pacotes em nome de outros usuários, o proprietário deve b um membro do **db_owner** função de banco de dados.

## <a name="how-package-synchronization-works"></a>Como funciona a sincronização do pacote

Para usar a sincronização do pacote, chame [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), que é uma nova função no [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). 

Para cada chamada para `rxSyncPackages`, você deve especificar uma instância do SQL Server e o banco de dados. Em seguida, listar os pacotes para sincronizar ou especificar o escopo do pacote.

1. Criar o contexto de computação do SQL Server usando o `RxInSqlServer` função. Se você não especificar um contexto de computação, o contexto de computação atual será usado.

2. Forneça o nome de um banco de dados na instância no contexto de computação especificado. Pacotes são sincronizados por banco de dados.

3. Especifica os pacotes para sincronizar usando o argumento de escopo.

    Se você usar **privada** escopo, apenas pacotes que pertencem ao proprietário especificado são sincronizados. Se você especificar **compartilhado** escopo, todos os pacotes não privado no banco de dados são sincronizados. 
    
    Se você executar a função sem especificar **privados** ou **compartilhado** escopo, todos os pacotes são sincronizados.

4. Se o comando for bem-sucedido, os pacotes existentes no sistema de arquivos são adicionados ao banco de dados, com o escopo especificado e o proprietário.

    Se o sistema de arquivos está corrompido, os pacotes são restaurados com base na lista mantida no banco de dados.

    Se o recurso de gerenciamento de pacote não está disponível no banco de dados de destino, um erro será gerado: "O recurso de gerenciamento de pacotes é não habilitado no SQL Server ou versão é muito antigo"

### <a name="example-1-synchronize-all-package-by-database"></a>Exemplo 1. Sincronizar todos os pacotes pelo banco de dados

Este exemplo obtém todos os novos pacotes do sistema de arquivos local e instala os pacotes no banco de dados [TestDB]. Como nenhum proprietário é específico, a lista inclui todos os pacotes que foram instalados para escopos privados e compartilhados.

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

O exemplo a seguir demonstra como sincronizar apenas os pacotes que foram instalados para um usuário específico. Neste exemplo, o usuário é identificado pelo nome de logon do SQL, *user1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>Recursos relacionados

[Gerenciamento de pacotes R para SQL Server](install-additional-r-packages-on-sql-server.md)
