---
title: Usar gerenciadores de pacotes de R – serviços do SQL Server Machine Learning
description: Use os comandos de R padrão como Packages para adicionar novos pacotes do R para SQL Server 2016 R Services ou serviços SQL Server 2017 Machine Learning (no banco de dados).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2582d519893fac3a49ce997674980d2d58d5cf32
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140773"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Usar gerenciadores de pacotes de R para instalar pacotes R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Você pode usar ferramentas padrão do R para instalar novos pacotes em uma instância do SQL Server 2016 ou SQL Server 2017, fornecendo o computador tem uma porta aberta 80 e direitos de administrador.

> [!IMPORTANT] 
> Certifique-se de instalar os pacotes na biblioteca padrão que está associado com a instância atual. Nunca instale pacotes em um diretório de usuário.

Este procedimento usa o RGui, mas você pode usar o RTerm ou qualquer outra R linha de comando ferramenta que dá suporte ao acesso com privilégios elevados.

## <a name="install-a-package-using-rgui"></a>Instalar um pacote usando o RGui

1. [Determinar o local da biblioteca de instância](../package-management/default-packages.md). Navegue até a pasta onde as ferramentas do R estão instaladas. Por exemplo, o caminho padrão para uma instância do SQL Server 2017 padrão é da seguinte maneira: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. RGui.exe com o botão direito e selecione **executar como administrador**. Se você não tiver as permissões necessárias, contate o administrador de banco de dados e fornecer uma lista de pacotes que você precisa.

1. Na linha de comando, se você souber o nome do pacote, você pode digitar: `install.packages("the_package-name")` As aspas duplas são necessárias para o nome do pacote.

1. Quando for solicitado para um site de espelhamento, selecione qualquer site que é conveniente para seu local.

Se o pacote de destino depende de pacotes adicionais, o instalador do R automaticamente baixa as dependências e os instala para você.

Se você tiver várias instâncias do SQL Server, como instâncias de lado a lado do SQL Server 2016 R Services e serviços do SQL Server 2017 Machine Learning, execute a instalação separadamente para cada instância se você quiser usar o pacote em ambos os contextos. Pacotes não podem ser compartilhados entre instâncias.

## <a name = "bkmk_offlineInstall"></a> Instalação offline, usando as ferramentas do R

Se o servidor não tiver acesso à internet, etapas adicionais são necessárias para preparar os pacotes. Para instalar pacotes R em um servidor que não tem acesso à internet, você deve:

+ Analise as dependências de antemão.
+ Baixe o pacote de destino em um computador com acesso à Internet.
+ Baixe os pacotes necessários no mesmo computador e coloque todos os pacotes em um arquivo de pacote único.
+ O arquivo zip, se ele não ainda estiver em formato compactado.
+ Copie o arquivo de pacote para um local no servidor.
+ Instale o pacote de destino especificando o arquivo morto como código-fonte.

> [!IMPORTANT] 
>  Certifique-se de que você analise todas as dependências e baixe **todos os** os pacotes necessários **antes de** começar a instalação. É recomendável [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para esse processo. Esse pacote R utiliza uma lista de pacotes que você deseja instalar, analisa as dependências e obtém os arquivos compactados para você. miniCRAN, em seguida, cria um único repositório que você pode copiar para o computador do servidor. Para obter detalhes, consulte [criar um repositório de pacote local usando o miniCRAN](create-a-local-package-repository-using-minicran.md)

Este procedimento pressupõe que você preparou a todos os pacotes que você precisa, em formato compactado e está pronto para copiá-los para o servidor.

1. Copie o pacote compactado arquivo ou para vários pacotes, o repositório completo que contém todos os pacotes compactados formato, para um local que o servidor possa acessar.

2. Abra a pasta no servidor em que as ferramentas do R para a instância estão instaladas. Por exemplo, se você estiver usando o prompt de comando do Windows em um sistema com o SQL Server 2016 R Services, alterne para `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Clique com botão direito em RGui ou RTerm e selecione **executar como administrador**.

4. Execute o comando de R `install.packages` e especifique o pacote ou o nome do repositório e o local dos arquivos compactados.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Este comando extrai o pacote R `mynewpackage` de seu arquivo compactado local, supondo que você salvou a cópia no diretório `C:\Temp\Downloaded packages`e instala o pacote no computador local. Se o pacote tiver quaisquer dependências, o instalador verifica se os pacotes existentes na biblioteca. Se você tiver criado um repositório que inclui as dependências, o instalador instala os pacotes necessários.

    Se os pacotes necessários não estão presentes na biblioteca de instância e não podem ser encontrados nos arquivos compactados, a instalação do pacote de destino falhará.

## <a name="see-also"></a>Confira também

+ [Instalar os novos pacotes R](install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)
