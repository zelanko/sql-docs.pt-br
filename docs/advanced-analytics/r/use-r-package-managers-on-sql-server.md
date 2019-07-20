---
title: Usar gerenciadores de pacotes R
description: Use comandos R padrão como install. Packages para adicionar novos pacotes de R a SQL Server 2016 R Services ou SQL Server 2017 Serviços de Machine Learning (no banco de dados).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: da14d2f00a6eb0c0ed52a50d27b6f1d06b062cf5
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344865"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Usar gerenciadores de pacotes do R para instalar pacotes R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Você pode usar as ferramentas padrão do R para instalar novos pacotes em uma instância do SQL Server 2016 ou SQL Server 2017, fornecendo ao computador uma porta aberta 80 e você tem direitos de administrador.

> [!IMPORTANT] 
> Certifique-se de instalar pacotes na biblioteca padrão associada à instância atual. Nunca instale pacotes em um diretório de usuário.

Este procedimento usa RGui, mas você pode usar o RTerm ou qualquer outra ferramenta de linha de comando do R que dê suporte ao acesso elevado.

## <a name="install-a-package-using-rgui"></a>Instalar um pacote usando o RGui

1. [Determine o local da biblioteca de instâncias](../package-management/default-packages.md). Navegue até a pasta em que as ferramentas do R estão instaladas. Por exemplo, o caminho padrão para uma instância padrão do SQL Server 2017 é o seguinte:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. Clique com o botão direito do mouse em RGui. exe e selecione **Executar como administrador**. Se você não tiver as permissões necessárias, entre em contato com o administrador do banco de dados e forneça uma lista dos pacotes necessários.

1. Na linha de comando, se você souber o nome do pacote, poderá digitar: `install.packages("the_package-name")`Aspas duplas são necessárias para o nome do pacote.

1. Quando solicitado por um site de espelhamento, selecione qualquer site que seja conveniente para seu local.

Se o pacote de destino depender de pacotes adicionais, o instalador do R baixará automaticamente as dependências e as instalará para você.

Se você tiver várias instâncias do SQL Server, como instâncias lado a lado de SQL Server 2016 R Services e SQL Server 2017 Serviços de Machine Learning, execute a instalação separadamente para cada instância se desejar usar o pacote em ambos os contextos. Os pacotes não podem ser compartilhados entre instâncias.

## <a name = "bkmk_offlineInstall"></a>Instalação offline usando ferramentas de R

Se o servidor não tiver acesso à Internet, serão necessárias etapas adicionais para preparar os pacotes. Para instalar pacotes do R em um servidor que não tem acesso à Internet, você deve:

+ Analise as dependências com antecedência.
+ Baixe o pacote de destino em um computador com acesso à Internet.
+ Baixe os pacotes necessários para o mesmo computador e coloque todos os pacotes em um único arquivo de pacote.
+ Compacte o arquivo morto se ele ainda não estiver no formato compactado.
+ Copie o arquivo morto do pacote para um local no servidor.
+ Instale o pacote de destino especificando o arquivo morto como fonte.

> [!IMPORTANT] 
>  Certifique-se de analisar todas as dependências e baixar **todos os** pacotes necessários **antes** de começar a instalação. Recomendamos [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para esse processo. Este pacote R usa uma lista de pacotes que você deseja instalar, analisa as dependências e obtém todos os arquivos compactados para você. em seguida, o miniCRAN cria um único repositório que você pode copiar para o computador do servidor. Para obter detalhes, consulte [criar um repositório de pacotes local usando miniCRAN](create-a-local-package-repository-using-minicran.md)

Este procedimento pressupõe que você preparou todos os pacotes necessários, no formato compactado, e está pronto para copiá-los para o servidor.

1. Copie o arquivo compactado do pacote ou para vários pacotes, o repositório completo que contém todos os pacotes no formato zipado, para um local que o servidor possa acessar.

2. Abra a pasta no servidor onde as ferramentas do R para a instância do estão instaladas. Por exemplo, se você estiver usando o prompt de comando do Windows em um sistema com SQL Server 2016 R Services, `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`mude para.

3. Clique com o botão direito do mouse em RGui ou RTerm e selecione **Executar como administrador**.

4. Execute o comando `install.packages` do R e especifique o nome do pacote ou do repositório e o local dos arquivos compactados.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Esse comando extrai o pacote `mynewpackage` R de seu arquivo zipado local, supondo que você salvou a cópia no diretório `C:\Temp\Downloaded packages`e instala o pacote no computador local. Se o pacote tiver alguma dependência, o instalador verificará os pacotes existentes na biblioteca. Se você tiver criado um repositório que inclui as dependências, o instalador instalará os pacotes necessários também.

    Se os pacotes necessários não estiverem presentes na biblioteca de instâncias e não puderem ser encontrados nos arquivos compactados, a instalação do pacote de destino falhará.

## <a name="see-also"></a>Confira também

+ [Instalar os novos pacotes R](install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)
