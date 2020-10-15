---
title: Instalar pacotes com ferramentas de R
description: Saiba como usar as ferramentas padrão do R para instalar novos pacotes do R em uma instância de Serviços de Machine Learning do SQL Server ou SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/20/2019
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 55e02294fcf59b4dc8d826f468b21ff8718492ef
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956668"
---
# <a name="install-packages-with-r-tools"></a>Instalar pacotes com ferramentas de R

[!INCLUDE [SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

Este artigo descreve como usar as ferramentas padrão do R para instalar novos pacotes de R em uma instância de Serviços de Machine Learning do SQL Server ou SQL Server R Services. Você pode instalar pacotes em um SQL Server que tenha uma conexão de Internet, bem como um isolado da Internet.

Além das ferramentas padrão do R, você pode instalar pacotes de R usando:

+ [RevoScaleR](install-r-packages-with-revoscaler.md)
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
+ [T-SQL](install-r-packages-with-tsql.md) (CRIAR BIBLIOTECA EXTERNA)
::: moniker-end

## <a name="general-considerations"></a>Considerações gerais

+ O código R em execução no SQL Server pode usar apenas os pacotes instalados na biblioteca de instâncias padrão. O SQL Server não pode carregar pacotes de bibliotecas externas, mesmo que a biblioteca esteja no mesmo computador.
Isso inclui bibliotecas do R instaladas com outros produtos da Microsoft.

+ A biblioteca de pacotes do R está localizada na pasta Arquivos de Programas de sua instância do SQL Server e, por padrão, a instalação nessa pasta requer permissões de administrador. Para obter mais informações, confira [Localização da biblioteca de pacotes](../package-management/r-package-information.md#default-r-library-location).

  ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
  Não administradores podem instalar pacotes usando o RevoScaleR 9.0.1 e posterior ou usando a opção CRIAR BIBLIOTECA EXTERNA. O usuário **dbo_owner** ou um usuário com a permissão CRIAR BIBLIOTECA EXTERNA, pode instalar pacotes de R no banco de dados atual. Para obter mais informações, consulte:
  + [Usar o RevoScaleR para instalar pacotes de R](install-r-packages-with-revoscaler.md)
  + [Use o T-SQL (CRIAR BIBLIOTECA EXTERNA) para instalar pacotes de R no SQL Server](install-r-packages-with-tsql.md)
  ::: moniker-end

  ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  Não administradores podem instalar pacotes usando o RevoScaleR 9.0.1 e posterior. O usuário **dbo_owner** pode instalar pacotes de R no banco de dados atual. Para obter mais informações, confira [usar o RevoScaleR para instalar pacotes de R](install-r-packages-with-revoscaler.md).
  ::: moniker-end

+ Em um ambiente do SQL Server protegido, talvez você queira evitar o seguinte:
  + Pacotes que exigem acesso à rede
  + Pacotes que exigem acesso elevado ao sistema de arquivos
  + Pacotes usados para desenvolvimento Web ou outras tarefas que não se beneficiam da execução dentro do SQL Server

## <a name="online-installation-with-internet-access"></a>Instalação online (com acesso à Internet)

Se o SQL Server tiver acesso à Internet, você poderá usar ferramentas de instalação de pacote padrão para instalar pacotes de R.

1. Determine a localização da biblioteca de instâncias (confira [Obter informações do pacote do R](../package-management/r-package-information.md)) e navegue até a pasta em que as ferramentas do R estão instaladas.

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   Por exemplo, o caminho padrão para uma instância padrão do SQL Server é:

   `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   Por exemplo, o caminho padrão para uma instância padrão do SQL Server é:

   `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

1. Execute **R** ou **Rgui** como administrador nesta pasta.

1. Execute o comando do R `install.packages` e especifique o nome do pacote. Se o pacote tiver alguma dependência, o instalador baixará automaticamente as dependências e as instalará.

Se você tiver várias instâncias lado a lado do SQL Server, execute a instalação separadamente para cada instância na qual você deseja usar o pacote. Os pacotes não podem ser compartilhados entre diferentes instâncias.

## <a name="offline-installation-no-internet-access"></a><a name = "bkmk_offlineInstall"></a> Instalação offline (sem acesso à Internet)

Frequentemente, os servidores que hospedam bancos de dados de produção não têm uma conexão de Internet. Para instalar pacotes de R nesse ambiente, você baixa e prepara pacotes e dependências com antecedência (como arquivos compactados) e, então, copia os arquivos para uma pasta no servidor. Depois que os arquivos estiverem no lugar, os pacotes poderão ser instalados offline.

Identificar todas as dependências é complicado. Para R, recomendamos que você use [**miniCRAN**](https://andrie.github.io/miniCRAN/) para criar um repositório local.
**miniCRAN** usa uma lista de pacotes que você deseja instalar, analisa dependências e obtém todos os arquivos compactados para você. Em seguida, ele cria um repositório que você pode copiar para a instância de SQL Server isolada. O pacote [**igraph**](https://igraph.org/r/) também é útil na análise das dependências do pacote.

Para mais informações, confira [Criar um repositório de pacotes do R local usando o miniCRAN](create-a-local-package-repository-using-minicran.md).

Depois que o arquivo zip estiver na instância do SQL Server, você poderá instalá-lo usando as ferramentas padrão do R no servidor.

1. Determine a localização da biblioteca de instâncias (confira [Obter informações do pacote do R](../package-management/r-package-information.md)) e navegue até a pasta em que as ferramentas do R estão instaladas. 

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   Por exemplo, o caminho padrão para uma instância padrão do SQL Server é:

   `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   Por exemplo, o caminho padrão para uma instância padrão do SQL Server é:

   `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

1. Execute **R** ou **Rgui** como administrador nesta pasta.

1. Execute o comando do R `install.packages` e especifique o nome do pacote ou do repositório e a localização dos arquivos compactados. Por exemplo:

   ```R
   install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
   ```

   Esse comando extrai o pacote do R `mynewpackage` de seu arquivo compactado local e instala o pacote. Se o pacote tiver dependências, o instalador verificará se há pacotes existentes na biblioteca. Se você tiver criado um repositório que inclui as dependências, o instalador instalará os pacotes necessários também.

   > [!NOTE]
   > Se os pacotes necessários não estiverem presentes na biblioteca de instâncias e não puderem ser encontrados nos arquivos compactados, a instalação do pacote de destino falhará.

Como alternativa a **miniCRAN**, você pode executar estas etapas manualmente:

1. Identifique todas as dependências do pacote.
1. Verifique se os pacotes necessários já estão instalados no servidor. Se o pacote estiver instalado, verifique se a versão está correta.
1. Baixe o pacote e todas as dependências em um computador separado com acesso à Internet.
1. Coloque o pacote e as dependências em um arquivo de pacote.
1. Compacte o arquivo se ele ainda não estiver em formato compactado.
1. Mova os arquivos para uma pasta acessível pelo servidor.
1. Execute um comando de instalação com suporte ou uma instrução DDL para instalar o pacote na biblioteca de instâncias.

## <a name="see-also"></a>Confira também

+ [Obter informações sobre o pacote do R](r-package-information.md)
+ [Dicas para usar pacotes de R](tips-for-using-r-packages.md)
+ [Tutoriais da linguagem R do SQL Server](../tutorials/r-tutorials.md)