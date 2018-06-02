---
title: Instalar novos pacotes de R nos serviços de aprendizado de máquina do SQL Server | Microsoft Docs
description: Adicionar novos pacotes de R para SQL Server 2016 R Services ou serviços do aprendizado de máquina 2017 SQL Server (no banco de dados)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8f7b0ee2b623f6a208a92823948bf0295bae33f6
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707494"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Use gerenciadores de pacotes de R para instalar pacotes de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Você pode usar ferramentas padrão de R para instalar novos pacotes em uma instância do SQL Server 2016 ou SQL Server de 2017, fornecendo o computador tem uma porta aberta 80 e ter direitos de administrador.

> [!IMPORTANT] 
> Certifique-se de instalar os pacotes para a biblioteca padrão que está associada com a instância atual. Nunca instale pacotes em um diretório de usuário.

Este procedimento usa RGui, mas você pode usar o RTerm ou qualquer outra R ferramenta de linha que dá suporte ao acesso com privilégios elevados.

## <a name="install-a-package-using-rgui"></a>Instalar um pacote usando RGui

1. [Determinar o local da biblioteca de instância](installing-and-managing-r-packages.md). Navegue até a pasta onde as ferramentas de R estão instaladas. Por exemplo, o caminho padrão para uma instância do SQL Server 2017 padrão é da seguinte maneira: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. RGui.exe e selecione **executar como administrador**. Se você não tiver as permissões necessárias, contate o administrador de banco de dados e fornecer uma lista dos pacotes que você precisa.

1. Na linha de comando, se você souber o nome do pacote, você pode digitar: `install.packages("the_package-name")` aspas duplas são necessárias para o nome do pacote.

1. Quando for solicitado para um site de espelhamento, selecione qualquer local que é conveniente para seu local.

Se o pacote de destino depender de outros pacotes, o instalador de R automaticamente baixa as dependências e as instala para você.

Se você tiver várias instâncias do SQL Server, como instâncias de lado a lado do SQL Server 2016 R Services e SQL Server 2017 Machine Learning Services, execute a instalação separadamente para cada instância se você quiser usar o pacote em ambos os contextos. Pacotes não podem ser compartilhados entre instâncias.

## <a name = "bkmk_offlineInstall"></a> Instalação offline usando ferramentas de R

Se o servidor não tiver acesso à internet, etapas adicionais são necessárias para preparar os pacotes. Para instalar pacotes de R em um servidor que não tem acesso à internet, você deve:

+ Analise as dependências com antecedência.
+ Baixe o pacote de destino para um computador com acesso à Internet.
+ Baixe os pacotes necessários no mesmo computador e colocar todos os pacotes em um arquivo único pacote.
+ Compacte o arquivo se ele não ainda estiver em formato compactado.
+ Copie o arquivo de pacote para um local no servidor.
+ Instale o pacote de destino, especificando o arquivo como origem.

> [!IMPORTANT] 
>  Certifique-se de que você analisar todas as dependências e baixar **todos os** pacotes necessários **antes de** iniciando a instalação. É recomendável [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para esse processo. Este pacote de R usa uma lista de pacotes que você deseja instalar, analisa as dependências e obtém todos os arquivos compactados para você. miniCRAN, em seguida, cria um único repositório que você pode copiar para o computador do servidor. Para obter detalhes, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md)

Este procedimento pressupõe que você preparou todos os pacotes que você precisa, em formato compactado e está pronto para copiá-los para o servidor.

1. Copie o pacote compactado arquivo ou de vários pacotes, o repositório completo que contém todos os pacotes no compactado formato para um local que o servidor possa acessar.

2. Abra a pasta no servidor onde as ferramentas de R para a instância são instaladas. Por exemplo, se você estiver usando o prompt de comando do Windows em um sistema com o SQL Server 2016 R Services, alternar para `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Clique com botão direito em RGui ou RTerm e selecione **executar como administrador**.

4. Execute o comando de R `install.packages` e especifique o pacote ou o nome do repositório e o local dos arquivos compactados.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Esse comando extrai o pacote R `mynewpackage` de seu arquivo compactado local, supondo que você salvou a cópia no diretório `C:\Temp\Downloaded packages`e instala o pacote no computador local. Se o pacote tiver quaisquer dependências, o instalador verifica se os pacotes existentes na biblioteca. Se você tiver criado um repositório que inclui as dependências, o instalador instalará os pacotes necessários também.

    Se os pacotes necessários não estão presentes na biblioteca de instância e não podem ser encontrados em arquivos compactados, a instalação do pacote de destino falha.

## <a name="see-also"></a>Confira também

+ [Instalar os novos pacotes R](install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)