---
title: "Pacote de instalação, desinstale e sincronizar | Microsoft Docs"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 959282395d178a090a3d447769ced4dca8882f89
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---

# <a name="r-package-synchronization-for-sql-server"></a>Sincronização de pacotes de R para o SQL Server

SQL Server 2017 CTP 2.0 inclui uma nova função para sincronização de pacotes de R, para dar suporte a backup e restauração de coleções de pacote de R associados a bancos de dados do SQL Server. Esse recurso ajuda a garantir que os conjuntos complexos de pacotes de R criados por usuários não sejam perdidos e podem ser facilmente restaurados.  

Este tópico descreve o que faz o recurso de sincronização do pacote e como usar o `rxSyncPackages()` função para executar as seguintes tarefas:

+  Sincronizar uma lista de pacotes para um banco de dados inteiro do SQL Server
+  Sincronizar os pacotes usados por um usuário individual, ou um grupo de usuários

> [!NOTE]
> Essa função é fornecida como parte do software de pré-lançamento e está sujeita a alterações antes do lançamento final.

## <a name="what-is-package-synchronization"></a>O que é sincronização de pacotes 

A sincronização do pacote é contextos de computação de um novo recurso que funciona especificamente com o SQL Server. Ele é projetado para obter uma lista de pacotes R instalados em um determinado banco de dados, para um determinado usuário ou grupo, e certifique-se de que os pacotes listados na correspondência de sistema de arquivo aqueles no banco de dados. 

Isso é útil se você precisar mover um banco de dados de usuário e mover os pacotes junto com o banco de dados. Você também pode usar a sincronização de pacotes quando você fazer backup e restaurar um banco de dados do SQL Server usado para trabalhos de R.

Uma nova função, a sincronização de pacote usa `rxSyncPackages()`. Para sincronizar a lista de pacotes, abra um prompt de comando de R, passar o contexto de computação que define a instância e banco de dados que você deseja trabalhar e, em seguida, fornecer um escopo de pacote ou um nome de usuário ou o proprietário. 

### <a name="how-packages-are-managed-in-r-and-sql-server"></a>Como os pacotes são gerenciados em R e SQL Server

Normalmente, quando você executar scripts R usando ferramentas padrão de R, pacotes R instalados no sistema de arquivos. Se várias pessoas usam R no mesmo computador, pode haver várias cópias dos mesmos pacotes, em pastas diferentes ou em bibliotecas de usuário diferente.

No entanto, para usar um pacote de R no SQL Server, o pacote deve ser instalado na biblioteca R padrão que é associada à instância. Um computador do servidor pode hospedar várias instâncias do SQL Server com R habilitado e, nesse caso, cada instância pode ter um conjunto separado de pacotes de R. 

O administrador de banco de dados é responsável pela instalação de pacotes na instância. No entanto, com as bibliotecas de gerenciamento de pacote, o administrador pode delegar essa responsabilidade aos usuários. 

+ Para cada banco de dados, o administrador pode fornecer aos usuários a capacidade de livremente instalar os pacotes de R precisarem. Esse mecanismo garante que vários usuários podem instalar versões diferentes de pacotes de R sem causar conflitos para outros usuários do computador do SQL Server. Usuários individuais podem instalar pacotes para seu próprio uso, usando um local de sistema de arquivos marcado como **privada**, se eles pertencem à função de banco de dados **rpkgs particular**.

+ O administrador pode configurar um grupo de usuários do pacote em um banco de dados e instalar os pacotes que são compartilhados por todos os usuários no grupo. Pacotes podem ser compartilhados entre os membros da função de banco de dados **compartilhado rpkgs**. Esses usuários também podem instalar pacotes para locais de escopo particular. 

### <a name="goal-of-package-synchronization"></a>Meta de sincronização do pacote

Se um banco de dados em um servidor é perdido ou deve ser movido, usando a sincronização do pacote, você poderá restaurar conjuntos de pacotes específicos para um banco de dados, usuário ou grupo. 

As informações sobre usuários e os pacotes que eles já têm instalado são armazenadas na instância do SQL Server e são usadas para atualizar os pacotes no sistema de arquivos. Sempre que você adicionar um novo pacote usando as funções de gerenciamento de pacote, ambos os registros no SQL Server e o sistema de arquivos são atualizados. Portanto, se um usuário for movido para um SQL Server diferente, você pode fazer um backup de banco de dados de trabalho do usuário e restaurá-lo para o novo servidor e os pacotes para o usuário serão instalados no sistema de arquivos no novo servidor, conforme exigido por R.


### <a name="supported-versions"></a>Versões com suporte

Essa função está incluída no SQL Server de 2017 CTP 2.0.

Como essa função é parte do Microsoft R version 9.1.0, você pode adicionar esse recurso a uma instância do SQL Server 2016 atualizando a instância para usar a versão mais recente do Microsoft R. Para obter mais informações, consulte [SqlBindR.exe usado para atualizar o SQL Server R Services](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="to-synchronize-packages"></a>Para sincronizar os pacotes

Você chamar `rxSyncPackages` após restaurando uma instância do SQL Server para uma nova máquina, ou se um R pacote no sistema de arquivos se acredita estar corrompido.

Se o comando for executado com êxito, os pacotes existentes no sistema de arquivos são adicionados ao banco de dados, o escopo e o proprietário especificado. Se o sistema de arquivos está corrompido, os pacotes são restred com base na lista mantida no banco de dados.

### <a name="syntax"></a>Sintaxe
`rxSyncPackages(computeContext = rxGetOption("computeContext"),  scope = c("shared", "private"), owner = c(), verbose = getOption("verbose"))`

+ Contexto de computação

    Defina um contexto de computação do SQL Server, consiste em uma instância e banco de dados e os pacotes a serem sincronizados. Criar o contexto de SQ Server usando o `RxInSqlServer` função. Se você não especificar um contexto de computação, o contexto de computação atual será usado. 

+ Escopo

  Indique se você estiver instalando os pacotes para um único usuário ou para um grupo de usuários: 

    + **privada** a operação incluirá somente os pacotes que foram instalados para uso por um proprietário especificado.
    + **compartilhado** o oepration incluirá todos os pacotes instalados para um grupo de usuários. 

  Se você executar a função sem especificar o escopo particular ou compartilhado, ambos os escopos são aplicados. Como resultado, todo o conjunto de pacotes disponíveis para todos os escopos e os usuários será copiado.

+ Proprietário 

    Especifique o proprietário dos pacotes para sincronizar. O nome do proprietário deve ser um usuário válido do banco de dados SQL. Se você deixar vazio, o nome de usuário de logon SQL especificado na conexão será usado.


### <a name="requirements"></a>Requisitos

+ A pessoa que executa a função deve ser uma entidade de segurança na instância do SQL Server e banco de dados que tem os pacotes e deve ser um membro de uma função de gerenciamento de pacote: **compartilhado rpkgs** ou **rpkgs privada** 
  + Para sincronizar os pacotes marcados como **compartilhado**, a pessoa que está executando a função deve estar associado a **compartilhado rpkgs** função e os pacotes que estão sendo movidos devem ter sido instalado para compartilhado biblioteca de escopo.
  + Para sincronizar pacotes marcados como **privada**, seja o proprietário do pacote ou o administrador deve executar a função e os pacotes devem ser privados.
+ **usuários rpkgs** -membros dessa função podem executar o código que usa pacotes instalados na instância do SQL Server, mas não é possível instalar ou synch pacotes.
+ Para sincronizar os pacotes em nome de outros usuários, o proprietário deve ser um membro do **db_owner** função de banco de dados.

## <a name="examples"></a>Exemplos

Os exemplos a seguir cria uma conexão com uma instância específica do SQL Server, especifique um banco de dados e, em seguida, especificam um conjunto de pacotes para sincronizar. 

Quando a chamada para `rxSyncPackages` é feita, o pacote que listas são sincronizadas entre o sistema de arquivos e o banco de dados. 

### <a name="synchronize-all-by-database"></a>Sincronizar ao banco de dados

Este exemplo obtém todos os pacotes instalados no banco de dados [TestDB]. Como nenhum proprietário é específico, a lista inclui todos os pacotes que foram instalados para escopos privados e compartilhados.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-scope"></a>Restringir pacotes sincronizados por escopo 

A seguir sincronizar exemplos apenas os pacotes no escopo compartilhado ou escopo particular.

**Escopo compartilhado**

```R
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)
```

**Escopo particular**

```R
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-owner"></a>Restringir pacotes sincronizados pelo proprietário 

O exemplo a seguir demonstra como obter apenas os pacotes que foram instalados para um usuário específico. Neste exemplo, o usuário é identificado pelo nome de logon do SQL, *user1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="see-also"></a>Consulte também

[Gerenciamento de pacotes de R para o SQL Server](../r/r-package-management-for-sql-server-r-services.md)
