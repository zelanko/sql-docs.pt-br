---
title: Instalar novos pacotes de R nos serviços de aprendizado de máquina do SQL Server | Microsoft Docs
description: Adicionar novos pacotes de R para SQL Server 2016 R Services ou serviços do aprendizado de máquina 2017 SQL Server (no banco de dados)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 20ef7181c5ab8c0494f73b205dddcdf1ac0a620e
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="install-new-r-packages-on-sql-server"></a>Instalar novos pacotes de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como instalar novos pacotes de R em uma instância do SQL Server onde o aprendizado de máquina está habilitado. Há vários métodos para instalar novos pacotes de R, dependendo de qual versão do SQL Server que você tem e se o servidor tem uma conexão de internet. As seguintes abordagens para nova instalação de pacote são possíveis.

| Abordagem                           | Permissões  | Remoto/Local |
|------------------------------------|---------------------------|-------|
| [Use gerenciadores de pacotes de R convencionais](#bkmk_rInstall)  | Admin | Local |
| [Usar RevoScaleR](use-revoscaler-to-manage-r-packages.md) | Admin | Local |
| [Usar o T-SQL (criar biblioteca externa)](install-r-packages-tsql.md) | Administrador de funções de banco de dados posteriormente, a instalação | both 
| [Use um miniCRAN para criar um repositório local](create-a-local-package-repository-using-minicran.md) | Administrador de funções de banco de dados posteriormente, a instalação | both |

## <a name="bkmk_rInstall"></a> Instalar pacotes de R em uma conexão de Internet

Você pode usar ferramentas padrão de R para instalar novos pacotes em uma instância do SQL Server 2016 ou SQL Server de 2017, fornecendo o computador tem uma porta aberta 80 e ter direitos de administrador.

> [!IMPORTANT] 
> Certifique-se de instalar os pacotes para a biblioteca padrão que está associada com a instância atual. Nunca instale pacotes em um diretório de usuário.

Este procedimento usa RGui, mas você pode usar o RTerm ou qualquer outra R ferramenta de linha que dá suporte ao acesso com privilégios elevados.

### <a name="install-a-package-using-rgui"></a>Instalar um pacote usando RGui

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
> > Certifique-se de que você analisar todas as dependências e baixar **todos os** pacotes necessários **antes de** iniciando a instalação. É recomendável [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para esse processo. Este pacote de R usa uma lista de pacotes que você deseja instalar, analisa as dependências e obtém todos os arquivos compactados para você. miniCRAN, em seguida, cria um único repositório que você pode copiar para o computador do servidor.
> 
> Para obter detalhes, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md)

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

## <a name="tips-for-package-installation"></a>Dicas para a instalação do pacote

Esta seção fornece dicas variadas e perguntas comuns relacionadas à instalação do pacote de R no SQL Server.

###  <a name="packageVersion"></a> Obter a versão correta do pacote e o formato

Há várias origens de pacotes de R, como o CRAN e Bioconductor. O site oficial da linguagem R (<https://www.r-project.org/>) lista vários desses recursos. Muitos pacotes são publicados no GitHub, onde é possível obter o código-fonte. Por fim, talvez tenha recebido pacotes R desenvolvidos por alguém de sua empresa, ou você tiver um pacote personalizado que você tenha escrito.

Independentemente da origem, antes de tentar instalar o pacote, verifique se você obteve o formato binário para a plataforma Windows. 

### <a name="bkmk_zipPreparation"></a> Baixe o pacote como um arquivo compactado

Para instalação em um servidor sem acesso à internet, você deve baixar uma cópia do pacote no formato de um arquivo compactado para instalação offline. **Não descompacte o pacote.**

Por exemplo, o procedimento a seguir descreve agora para obter a versão correta do [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) pacote da Bioconductor, supondo que o computador tem acesso à internet.

1.  Na lista **Arquivos de Pacote** , localize a versão **Binário do Windows** .

2.  Clique no link para o. Arquivo ZIP e selecione **Salvar destino como**.

3.  Navegue até a pasta local onde os pacotes compactados são armazenados e clique em **salvar**.

    Esse processo cria uma cópia local do pacote. 

4. Se você receber um erro de download, tente um site diferente do espelho.

5. Depois que o arquivo de pacote foi baixado, você pode instalar o pacote ou copiar o pacote compactado em um servidor que não tenha acesso à internet.

> [!TIP]
> Se por engano, você instalar o pacote em vez de baixar os binários, uma cópia do arquivo compactado baixado também serão salvos em seu computador. Observe as mensagens de status que o pacote for instalado, para determinar o local do arquivo. Você pode copiar o arquivo compactado para o servidor que não tem acesso à internet.
> 
> No entanto, quando você obter pacotes usando esse método, as dependências não são incluídas. 

### <a name="bkmk_packageDependencies"></a> Obter pacotes necessários

Pacotes de R com frequência dependem de vários pacotes, alguns dos quais podem não estar disponíveis na biblioteca R padrão usada pela instância. Às vezes, um pacote exige uma versão diferente de um pacote dependente que já está instalado.

Se você precisar instalar vários pacotes, ou para garantir que todas as pessoas em sua organização obtém o tipo correto de pacote e versão, é recomendável que você use o [miniCRAN](https://mran.microsoft.com/package/miniCRAN) pacote para analisar a cadeia de dependência completa. minicRAN cria um repositório local que pode ser compartilhado entre vários usuários ou computadores. Para obter mais informações, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md).


### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>Saber qual biblioteca que você está instalando e quais pacotes já estão instalados.

Se você modificou anteriormente o ambiente R no computador, antes de instalar qualquer coisa, pausar um momento e certifique-se de que a variável de ambiente R `.libPath` usa apenas um caminho.

Esse caminho deve apontar para a pasta R_SERVICES para a instância. Para obter mais informações, incluindo como determinar quais pacotes já estão instalados, consulte [pacotes R instalados com o SQL Server](installing-and-managing-r-packages.md).

### <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Instalação lado a lado com Standalone R ou servidores de Python

Se você instalou o servidor SQL Server 2017 Microsoft Machine Learning (autônomo) ou o servidor do SQL Server 2016 R (autônomo) além de análise no banco de dados (serviços de aprendizado de máquina do SQL Server 2017 e SQL Server 2016 R Services), o computador tem separar as instalações do R para cada um, com as duplicatas de todas as bibliotecas e ferramentas de R.

Pacotes que estão instalados para a biblioteca R_SERVER são usados somente por um servidor autônomo e não podem ser acessados por uma instância do SQL Server (no banco de dados). Use sempre o `R_SERVICES` biblioteca ao instalar os pacotes que você deseja usar no banco de dados no SQL Server.
