---
title: Instalar sem acesso à Internet
description: Instalar Python e R para aprendizado de máquina do SQL Server em computadores isolados atrás de um firewall de rede.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 29beb747952451f11762132726a204ada903a24e
ms.sourcegitcommit: 11691bfa8ec0dd6f14cc9cd3d1f62273f6eee885
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074479"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>Instalar Python e R para aprendizado de máquina do SQL Server em computadores sem acesso à Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Por padrão, os instaladores conectam-se aos sites de download da Microsoft para obter os componentes necessários e atualizados para aprendizado de máquina no SQL Server. Se as restrições de firewall impedirem o instalador de acessar esses sites, você poderá usar um dispositivo conectado à Internet para baixar os arquivos, transferir os arquivos para um servidor offline e executar a instalação.

A análise no banco de dados consiste em uma instância do mecanismo de banco de dados, mais os componentes adicionais para a integração do R e do Python, dependendo da versão do SQL Server. 

+ O SQL Server 2019 inclui R, Python e Java
+ O SQL Server 2017 inclui R e Python
+ O SQL Server 2016 é somente R

Em um servidor isolado, machine learning e recursos específicos da linguagem R/Python são adicionados por meio de arquivos CAB. 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
## <a name="sql-server-2019-offline-install"></a>Instalação offline do SQL Server 2019

Para instalar os Serviços de Machine Learning do SQL Server (R e Python) em um servidor isolado, comece baixando a versão inicial do SQL Server e os arquivos CAB correspondentes para suporte a R e Python. Mesmo que você planeje atualizar imediatamente o servidor para usar a atualização cumulativa mais recente, uma versão inicial deverá ser instalada primeiro.

> [!Note]
> O SQL Server 2019 não tem service packs. A versão inicial é a única linha de base, com manutenção apenas por meio de atualizações cumulativas.

### <a name="1---download-2019-cabs"></a>1 – Baixar CABs 2019

Em um computador com conexão com a Internet, baixe os arquivos CAB fornecendo os recursos R e Python para a versão inicial e a mídia de instalação do SQL Server 2019.

Versão  |Link de download  |
---------|---------------|
Microsoft R Open        | [SRO_3.5.2.125_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085686) |
Servidor R da Microsoft      | [SRS_9.4.7.32_1033.cab](https://go.microsoft.com/fwlink/?linkid=2100159) |
Microsoft Python Open   | [SPO_4.5.12.120_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085793) |
Microsoft Python Server | [SPS_9.4.7.32_1033.cab](https://go.microsoft.com/fwlink/?linkid=2100160) |

> [!NOTE]
> O recurso Java está incluído com a mídia de instalação do SQL Server e não requer um arquivo CAB separado.

###  <a name="2---get-sql-server-2019-installation-media"></a>2 – Obter mídia de instalação do SQL Server 2019

1. Em um computador com conexão com a Internet, baixe o [programa de instalação do SQL Server 2019](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Clique duas vezes em instalação e escolha o tipo de instalação **Baixar Mídia**. Com essa opção, a instalação cria um arquivo local .iso (ou .cab) que contém a mídia de instalação.

   ![Escolher o tipo de instalação de mídia de download](media/2019offline-download-tile.png "Baixar mídia")

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
## <a name="sql-server-2017-offline-install"></a>Instalação offline do SQL Server 2017

Para instalar os Serviços de Machine Learning do SQL Server (R e Python) em um servidor isolado, comece baixando a versão inicial do SQL Server e os arquivos CAB correspondentes para suporte a R e Python. Mesmo que você planeje atualizar imediatamente o servidor para usar a atualização cumulativa mais recente, uma versão inicial deverá ser instalada primeiro.

> [!Note]
> O SQL Server 2017 não tem service packs. É a primeira versão do SQL Server a usar a versão inicial como a única linha de base, com manutenção apenas por meio de atualizações cumulativas. 

### <a name="1---download-2017-cabs"></a>1 – Baixar CABs 2017

Em um computador com conexão com a Internet, baixe os arquivos CAB fornecendo os recursos R e Python para a versão inicial e a mídia de instalação do SQL Server 2017. 

Versão  |Link de download  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Servidor R da Microsoft      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2 – Obter mídia de instalação do SQL Server 2017

1. Em um computador com conexão com a Internet, baixe o [programa de instalação do SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Clique duas vezes em instalação e escolha o tipo de instalação **Baixar Mídia**. Com essa opção, a instalação cria um arquivo local .iso (ou .cab) que contém a mídia de instalação.

   ![Escolher o tipo de instalação de mídia de download](media/offline-download-tile.png "Baixar mídia")

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="sql-server-2016-offline-install"></a>Instalação offline do SQL Server 2016

A análise no banco de dados do SQL Server 2016 é somente R, com apenas dois arquivos CAB para pacotes de produtos e a distribuição da Microsoft do R de software livre, respectivamente. Comece instalando qualquer uma destas versões: RTM, SP 1, SP 2. Quando há uma instalação básica em vigor, as atualizações cumulativas podem ser aplicadas como uma próxima etapa.

Em um computador com conexão com a Internet, baixe os arquivos CAB usados pela instalação para instalar a análise no banco de dados no SQL Server 2016. 

### <a name="1---download-2016-cabs"></a>1 – Baixar CABs 2016

Versão  | Microsoft R Open | Servidor R da Microsoft |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2 – Obter mídia de instalação do SQL Server 2016

Você pode instalar o SQL Server 2016 RTM, SP 1 ou SP 2 como sua primeira instalação no computador de destino. Qualquer uma dessas versões pode aceitar uma atualização cumulativa.

Uma maneira de obter um arquivo .iso contendo a mídia de instalação é por meio do [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/). Entre e use o link **Downloads** para localizar a versão do SQL Server 2016 que você deseja instalar. O download está na forma de um arquivo .iso, que pode ser copiado para o computador de destino para uma instalação offline.

::: moniker-end

## <a name="transfer-files"></a>Transferir arquivos

Copie a mídia de instalação do SQL Server (.iso ou .cab) e os arquivos CAB de análise no banco de dados para o computador de destino. Coloque os arquivos CAB e o arquivo de mídia de instalação na mesma pasta no computador de destino, como a pasta %TEMP% do usuário de instalação.

A pasta %TEMP% é necessária para arquivos CAB do Python. Para R, é possível usar %TEMP% ou definir o parâmetro `myrcachedirectory` para o caminho do CAB.

## <a name="run-setup"></a>Executar a instalação

Quando você executa a Instalação do SQL Server em um computador desconectado da Internet, a Instalação adiciona uma página de **Instalação offline** ao assistente para que você possa especificar a localização dos arquivos CAB copiados na etapa anterior.

1. Para começar a instalação, clique duas vezes no arquivo .iso ou .cab para acessar a mídia de instalação. Você deve ver o arquivo **setup.exe**.

2. Clique com o botão direito do mouse em **setup.exe** e execute como administrador.

3. Quando o assistente de instalação exibir a página de licenciamento para componentes R ou Python de software livre, clique em **Aceitar**. Aceitar os termos de licenciamento permite que você prossiga para a próxima etapa.

4. Quando chegar à página **Instalação offline**, em **Caminho de Instalação**, especifique a pasta que contém os arquivos CAB que você copiou anteriormente.

5. Continue seguindo os prompts na tela para concluir a instalação.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>Aplicar atualizações cumulativas

Recomendamos que você aplique a atualização cumulativa mais recente aos componentes do mecanismo de banco de dados e de aprendizado de máquina. As atualizações cumulativas são instaladas por meio do programa de instalação. 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
1. Comece com uma instância de linha de base. Você pode aplicar atualizações cumulativas apenas a instalações existentes da versão inicial do SQL Server.

2. Em um dispositivo conectado à Internet, acesse a lista de atualização cumulativa para sua versão do SQL Server:

   + Atualizações do SQL Server 2019 *(as atualizações ainda não estão disponíveis para 2019)*
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
1. Comece com uma instância de linha de base. Você pode aplicar atualizações cumulativas apenas a instalações existentes da versão inicial do SQL Server.

2. Em um dispositivo conectado à Internet, acesse a lista de atualização cumulativa para sua versão do SQL Server:

   + [Atualizações do SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. Comece com uma instância de linha de base. Você só pode aplicar atualizações cumulativas a instalações existentes da versão inicial do SQL Server 2016, do SQL Server 2016 SP 1 ou do SQL Server 2016 SP 2.

2. Em um dispositivo conectado à Internet, acesse a lista de atualização cumulativa para sua versão do SQL Server:

   + [Atualizações do SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)
::: moniker-end

3. Selecione a atualização cumulativa mais recente para baixar o executável.

4. Obtenha os arquivos CAB correspondentes para R e Python. Para links de download, confira [Downloads CAB para atualizações cumulativas em instâncias de análise no banco de dados do SQL Server](sql-ml-cab-downloads.md).

5. Transfira todos os arquivos, os arquivos executáveis e os arquivos CAB, para a mesma pasta no computador offline.

6. Execute a instalação. Aceite os termos de licenciamento e, na página seleção de recursos, examine os recursos para os quais as atualizações cumulativas são aplicadas. Você deve ver todos os recursos instalados para a instância atual, incluindo os recursos de aprendizado de máquina.

   ![Selecionar recursos na árvore de recursos](media/cumulative-update-feature-selection.png "lista de recursos")

5. Continue com o assistente, aceitando os termos de licenciamento para distribuições de R e Python. Durante a instalação, você deverá escolher a localização da pasta que contém os arquivos CAB atualizados.

## <a name="set-environment-variables"></a>Definir variáveis de ambiente

Somente para a integração de recursos do R, é necessário definir a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel MKL (Math Kernel Library).

1. No Painel de Controle, clique em **Sistema e Segurança** > **Sistema** > **Configurações Avançadas do Sistema** > **Variáveis de Ambiente**.

2. Crie uma variável de usuário ou do sistema. 

   + Defina o nome da variável como `MKL_CBWR`
   + Defina o valor da variável como `AUTO`

Esta etapa requer uma reinicialização do servidor. Se estiver prestes a habilitar a execução de script, você poderá manter a reinicialização até que todo o trabalho de configuração seja concluído.

## <a name="post-install-configuration"></a>Configuração de pós-instalação

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Depois de concluir a instalação, reinicie o serviço e configure o servidor para habilitar a execução do script:

+ [Habilitar a execução de script externo](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)

Uma instalação offline inicial dos Serviços de Machine Learning do SQL Server requer a mesma configuração que uma instalação online:

+ [Verificar a instalação](sql-machine-learning-services-windows-install.md#verify-installation)
+ [Configuração adicional conforme necessário](sql-machine-learning-services-windows-install.md#additional-configuration)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Depois de concluir a instalação, reinicie o serviço e configure o servidor para habilitar a execução do script:

+ [Habilitar a execução de script externo](sql-r-services-windows-install.md#bkmk_enableFeature)

Uma instalação offline inicial do SQL Server R Services requer a mesma configuração que uma instalação online:

+ [Verificar a instalação](sql-r-services-windows-install.md#verify-installation)
+ [Configuração adicional conforme necessário](sql-r-services-windows-install.md#bkmk_FollowUp)
::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para verificar o status da instalação da instância e corrigir problemas comuns, confira [Relatórios personalizados para o SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Para obter ajuda com mensagens ou entradas de log desconhecidas, confira [Perguntas frequentes sobre atualização e instalação – Serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).
