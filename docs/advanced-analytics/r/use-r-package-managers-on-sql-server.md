---
title: Usar gerenciadores de pacotes R
description: Use comandos do R padrão como install.packages para adicionar novos pacotes do R aos SQL Server 2016 R Services ou aos Serviços de Machine Learning do SQL Server (no banco de dados).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f6d828a7267ab2b4b1def17f9d1c6bf4a6018dc
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633613"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Usar gerenciadores de pacotes do R para instalar pacotes do R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Você pode usar as ferramentas padrão do R para instalar novos pacotes em uma instância do SQL Server 2016 ou do SQL Server 2017, desde que o computador tenha uma porta aberta 80 e você tenha direitos de administrador.

> [!IMPORTANT] 
> Instale os pacotes na biblioteca padrão associada à instância atual. Nunca instale pacotes em um diretório de usuário.

Este procedimento usa o RGui, mas você pode usar o RTerm ou qualquer outra ferramenta de linha de comando do R que dê suporte ao acesso com privilégios elevados.

## <a name="install-a-package-using-rgui"></a>Instalar um pacote usando RGui

1. [Determine a localização da biblioteca de instâncias](../package-management/r-package-information.md). Navegue até a pasta em que as ferramentas do R estão armazenadas. Por exemplo, o caminho padrão para uma instância padrão do SQL Server 2017 é o seguinte: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. Clique com o botão direito do mouse em RGui.exe e selecione **Executar como administrador**. Se você não tiver as permissões necessárias, contate o administrador de banco de dados e forneça uma lista dos pacotes necessários.

1. Na linha de comando, se você souber o nome do pacote, poderá digitar: `install.packages("the_package-name")` Aspas duplas são necessárias para o nome do pacote.

1. Quando você for solicitado a inserir um site de espelhamento, selecione qualquer um que seja conveniente para sua localização.

Se o pacote de destino depender de outros pacotes, o instalador do R baixará automaticamente as dependências e as instalará para você.

Se você tiver várias instâncias do SQL Server, como instâncias lado a lado do SQL Server 2016 R Services e os Serviços de Machine Learning do SQL Server, execute a instalação separadamente para cada instância se desejar usar o pacote em ambos os contextos. Os pacotes não podem ser compartilhados entre diferentes instâncias.

## <a name = "bkmk_offlineInstall"></a> Instalação offline usando as ferramentas do R

Se o servidor não tiver acesso à Internet, outras etapas serão necessárias para preparar os pacotes. Para instalar os pacotes do R em um servidor que não tem acesso à Internet, você deverá:

+ Analisar dependências com antecedência.
+ Baixar o pacote de destino para um computador com acesso à Internet.
+ Baixar os pacotes necessários para o mesmo computador e colocar todos os pacotes em um único arquivo de pacote.
+ Compactar o arquivo se ele ainda não estiver em formato compactado.
+ Copiar os arquivos de pacote para uma localização no servidor.
+ Instalar o pacote de destino especificando o arquivo morto como fonte.

> [!IMPORTANT] 
>  Lembre-se de analisar todas as dependências e baixar **todos** os pacotes necessários **antes de** iniciar a instalação. Recomendamos o [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para esse processo. Este pacote do R usa uma lista de pacotes que você deseja instalar, analisa dependências e obtém todos os arquivos compactados para você. O miniCRAN cria um único repositório que você pode copiar para o computador do servidor. Para obter detalhes, confira [Criar um repositório de pacotes local usando o miniCRAN](create-a-local-package-repository-using-minicran.md)

Este procedimento pressupõe que você preparou todos os pacotes de que precisa, em formato compactado, e está pronto para copiá-los para o servidor.

1. Copie o arquivo compactado do pacote ou, para vários pacotes, o repositório completo que contém todos os pacotes em formato compactado, para uma localização que o servidor possa acessar.

2. Abra a pasta no servidor na qual as ferramentas do R para a instância estão instaladas. Por exemplo, se você estiver usando o prompt de comando do Windows em um sistema com os SQL Server 2016 R Services, alterne para `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Clique com o botão direito do mouse no RGui ou no RTerm e selecione **Executar como administrador**.

4. Execute o comando do R `install.packages` e especifique o nome do pacote ou do repositório e a localização dos arquivos compactados.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Esse comando extrai o pacote `mynewpackage` do R de seu arquivo compactado local, supondo que você tenha salvado a cópia no diretório `C:\Temp\Downloaded packages`, e instala o pacote no computador local. Se o pacote tiver dependências, o instalador verificará se há pacotes existentes na biblioteca. Se você tiver criado um repositório que inclui as dependências, o instalador instalará os pacotes necessários também.

    Se os pacotes necessários não estiverem presentes na biblioteca de instâncias e não puderem ser encontrados nos arquivos compactados, a instalação do pacote de destino falhará.

## <a name="see-also"></a>Confira também

+ [Instalar os novos pacotes R](install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)
