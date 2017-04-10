---
title: "Gerenciamento de pacotes de R para SQL Server R Services | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# Gerenciamento de pacotes de R para SQL Server R Services
Para tornar mais fácil o gerenciamento de pacotes de R que são executados em uma instância do SQL Server, o pacote **RevoScaleR** agora inclui funções para dar suporte à instalação e gerenciamento de pacotes de R. 

Essa nova funcionalidade dá suporte a vários cenários:

- O cientista de dados pode instalar pacotes de R necessários no SQL Server sem ter acesso administrativo ao computador do SQL Server. Os pacotes são instalados em uma base por banco de dados.
- É fácil compartilhar pacotes com outras pessoas. Basta estabelecer um repositório local de pacotes e fazer com que cada cientista de dados instale os pacotes nos bancos de dados individuais.
- O administrador do banco de dados não precisa saber como executar comandos de R ou entender sobre dependências de pacote. O DBA usa funções do banco de dados para controlar quais usuários do SQL Server têm permissão para instalar, desinstalar ou usar os pacotes.
 
**Como funciona**

* O administrador de banco de dados é responsável por configurar funções e adicionar usuários às funções, para controlar quem tem permissão para adicionar ou remover pacotes de R no ambiente do SQL Server.
* Se você tiver permissão para instalar pacotes, você executa uma das funções de gerenciamento de pacote no código R e especifica o contexto de computação no qual pacotes devem ser adicionados ou removidos. O contexto de computação pode ser seu computador local ou um banco de dados na instância do SQL Server. 
* Se a chamada para instalar pacotes é executada no SQL Server, suas credenciais vão determinar se é possível concluir a operação no servidor. 
- As funções de instalação do pacote verificam se há dependências e certificam-se de que todos os pacotes relacionados possam ser instalados no SQL Server, assim como a instalação de pacote do R no contexto de computação local.
- A função que desinstala pacotes também calcula as dependências e garante que os pacotes que não são mais usados por outros pacotes no SQL Server sejam removidos para liberar recursos.
- Cada cientista de dados pode instalar pacotes particulares que não são visíveis para outras pessoas, dando-lhes uma área restrita isolada para trabalhar com seus próprios pacotes de R.
-  Como os pacotes podem ser definidos em um banco de dados e cada usuário obtém uma área restrita isolada de pacotes em cada banco de dados, é mais fácil para a instalação usar versões diferentes do uso do mesmo pacote R. 

> [!NOTE]
> Atualmente esse recurso está sendo lançado para uso somente com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]. 

## <a name="database-roles-and-database-scoping"></a>Funções de banco de dados e escopo do banco de dados

As novas funções de gerenciamento de pacote fornecem dois escopos para a instalação e o uso de pacotes no SQL Server em um determinado banco de dados:

- **Escopo compartilhado**

  *Escopo compartilhado* significa que os usuários que receberam permissão para a função de escopo compartilhado (**rpkgs-shared**) podem instalar e desinstalar pacotes em um banco de dados especificado. Um pacote que é instalado em uma biblioteca de escopo compartilhado pode ser usado por outros usuários do banco de dados do SQL Server, contanto que esses usuários tenham permissão para usar pacotes de R instalados. 

- **Escopo particular** 

  *Escopo particular* significa que os usuários que receberam associação na função de escopo particular (**rpkgs-private**) podem instalar ou desinstalar pacotes em um local de biblioteca particular definido para cada usuário. Portanto, todos os pacotes instalados no escopo particular podem ser usados somente pelo usuário que os instalou. Em outras palavras, um usuário do SQL Server não pode usar pacotes particulares que foram instalados por outro usuário. 

Esses modelos de escopo *compartilhado* e *particular* podem ser combinados para desenvolver sistemas seguros personalizados para implantar e gerenciar pacotes no SQL Server. 

Por exemplo, ao usar o escopo compartilhado, o líder ou o gerente de um grupo de cientistas de dados pode receber permissão para instalar pacotes e esses pacotes podem ser usados por todos os outros usuários ou os cientistas de dados na mesma instância do SQL Server. 

Outro cenário poderia exigir maior isolamento entre usuários, ou o uso de diferentes versões de pacotes. Nesse caso, o escopo particular pode ser usado para fornecer permissões individuais aos cientistas de dados, que seriam responsáveis por instalar e usar apenas os pacotes que precisam. Como os pacotes são instalados em uma base individual, os pacotes instalados por um usuário não afetariam o trabalho de outros usuários que estão usando o mesmo banco de dados do SQL Server. 

### <a name="database-roles-for-package-management"></a>Funções de banco de dados para gerenciamento de pacotes

As seguintes novas funções de banco de dados oferecem suporte à instalação segura e gerenciamento de pacotes para o SQL R Services: 

- **rpkgs-users** permite que os usuários usem quaisquer pacotes compartilhados que foram instalados por membros da função **rpkgs-shared**.

- **rpkgs-private** fornece acesso aos pacotes compartilhados com as mesmas permissões que a função **rpkgs-users**. Os membros desta função também podem instalar, remover e usar pacotes com escopo definido como particular.

-  **rpkgs-shared** fornece as mesmas permissões que a função **rpkgs-private**. Os usuários que são membros dessa função também podem instalar ou remover pacotes compartilhados. 
 
- **db_owner** – tem as mesmas permissões que a função **rpkgs-shared**. Também pode conceder o aos usuários o direito de instalar ou remover pacotes compartilhados e privados.



## <a name="new-package-management-functions"></a>Novas funções de gerenciamento de pacote


+ `rxInstalledPackages`: Localizar informações sobre pacotes instalados no contexto de computação especificado.

+ `rxInstallPackages`: Instalar pacotes em um contexto de computação, de um repositório especificado ou lendo pacotes compactados salvos localmente.

+ `rxRemovePackages`: Remover os pacotes instalados de um contexto de computação.

+ `rxFindPackage`: Obter o caminho para um ou mais pacotes no contexto de computação especificado.

+ `rxSqlLibPaths`: Obter o caminho de pesquisa das árvores de biblioteca para os pacotes durante a execução no SQL Server.

## <a name="examples"></a>Exemplos

### <a name="get-package-location-on-sql-server-compute-context"></a>Obter o local do pacote no contexto de computação do SQL Server

Este exemplo obtém o caminho para o pacote **RevoScaleR** no contexto de computação *sqlServer*.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```
  
  ### <a name="get-locations-for-multiple-packages"></a>Obter locais de vários pacotes

O exemplo a seguir obtém os caminhos para os pacotes **RevoScaleR** e **lattice**, no contexto de computação *sqlServer*. Ao encontrar informações sobre vários pacotes, transmite um vetor de cadeia de caracteres que contém os nomes dos pacotes.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```



### <a name="list-packages-in-specified-compute-context"></a>Listar pacotes em um contexto de computação especificado

Este exemplo lista e, em seguida, exibe no console todos os pacotes instalados no contexto de computação *sqlServer*.

  ```R
  myPackages <- rxInstalledPackages(computeContext = sqlServer) 
  myPackages
  ```

### <a name="get-package-versions"></a>Obter versões de pacote

Este exemplo obtém o número de build e os números de versão de um pacote instalado no contexto de computação *sqlServer*.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer) 
```

### <a name="install-a-package-on-sql-server"></a>Instalar um pacote no SQL Server

Este exemplo instala o pacote **ggplot2** e suas dependências no contexto de computação *sqlServer*.

  ```R
  pkgs <- c("ggplot2")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="remove-a-package-from-sql-server"></a>Remover um pacote do SQL Server

Este exemplo remove o pacote **ggplot2** e suas dependências do contexto de computação *sqlServer*.

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

## <a name="see-also"></a>Consulte também

[Como habilitar ou desabilitar o gerenciamento de pacotes de R](../../advanced-analytics/r-services/how-to-enable-or-disable-r-package-management.md)