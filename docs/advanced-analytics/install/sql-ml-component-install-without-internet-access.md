---
title: Instalar a linguagem R e os componentes do Python sem acesso à Internet
description: Offline ou desconectado Machine Learning configuração de R e Python na instância de SQL Server isolada por trás de um firewall de rede.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ddeea99addae3229575ca581f344332587e85981
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715820"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>Instalar SQL Server R e Python do Machine Learning em computadores sem acesso à Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Por padrão, os instaladores se conectam aos sites de download da Microsoft para obter os componentes necessários e atualizados para o aprendizado de máquina no SQL Server. Se as restrições de firewall impedirem que o instalador atinja esses sites, você poderá usar um dispositivo conectado à Internet para baixar arquivos, transferir arquivos para um servidor offline e, em seguida, executar a instalação.

A análise no banco de dados consiste em uma instância do mecanismo de banco de dados, além de componentes adicionais para a integração do R e do Python, dependendo da versão do SQL Server. 

+ SQL Server 2017 e posterior inclui R e Python 
+ SQL Server 2016 é somente R.

Em um servidor isolado, o Machine Learning e os recursos específicos de linguagem R/Python são adicionados por meio de arquivos CAB. 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="sql-server-2017-offline-install"></a>Instalação offline do SQL Server 2017

Para instalar SQL Server Serviços de Machine Learning (R e Python) em um servidor isolado, comece baixando a versão inicial do SQL Server e os arquivos CAB correspondentes para o suporte de R e Python. Mesmo que você planeje atualizar imediatamente o servidor para usar a atualização cumulativa mais recente, uma versão inicial deve ser instalada primeiro.

> [!Note]
> SQL Server 2017 não tem Service Packs. É a primeira versão do SQL Server usar a versão inicial como a única linha de base, com manutenção apenas por meio de atualizações cumulativas. 

### <a name="1---download-2017-cabs"></a>1-baixar 2017 CABs

Em um computador que tenha uma conexão com a Internet, baixe os arquivos CAB fornecendo os recursos de R e Python para a versão inicial e a mídia de instalação do SQL Server 2017. 

Versão  |Link de download  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2-obter mídia de instalação do SQL Server 2017

1. Em um computador que tenha uma conexão com a Internet, baixe o [SQL Server programa de instalação 2017](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Clique duas vezes em instalação e escolha o tipo de instalação **baixar mídia** . Com essa opção, a instalação cria um arquivo local. ISO (ou. cab) que contém a mídia de instalação.

   ![Escolher o tipo de instalação de mídia de download](media/offline-download-tile.png "Baixar mídia")

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="sql-server-2016-offline-install"></a>Instalação offline do SQL Server 2016

SQL Server análise no banco de dados 2016 é somente R, com apenas dois arquivos CAB para pacotes de produtos e a distribuição da Microsoft do R de software livre, respectivamente. Comece instalando qualquer uma destas versões: RTM, SP 1, SP 2. Quando uma instalação básica está em vigor, as atualizações cumulativas podem ser aplicadas como uma próxima etapa.

Em um computador que tenha uma conexão com a Internet, baixe os arquivos CAB usados pela instalação para instalar a análise no banco de dados no SQL Server 2016. 

### <a name="1---download-2016-cabs"></a>1-baixar 2016 CABs

Versão  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2-obter mídia de instalação do SQL Server 2016

Você pode instalar SQL Server 2016 RTM, SP 1 ou SP 2 como sua primeira instalação no computador de destino. Qualquer uma dessas versões pode aceitar uma atualização cumulativa.

Uma maneira de obter um arquivo. ISO contendo a mídia de instalação é por meio de [Visual Studio dev Essentials](https://visualstudio.microsoft.com/dev-essentials/). Entre e use o link **downloads** para localizar a versão SQL Server 2016 que você deseja instalar. O download está na forma de um arquivo. ISO, que pode ser copiado para o computador de destino para uma instalação offline.

::: moniker-end

## <a name="transfer-files"></a>Transferir arquivos

Copie a mídia de instalação do SQL Server (. ISO ou. cab) e os arquivos CAB de análise no banco de dados para o computador de destino. Coloque os arquivos CAB e o arquivo de mídia de instalação na mesma pasta no computador de destino, como a pasta% TEMP * do usuário de instalação.

A pasta% TEMP% é necessária para arquivos CAB do Python. Para o R, você pode usar% TEMP% ou definir o parâmetro myrcachedirectory para o caminho do CAB.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
A captura de tela a seguir mostra SQL Server arquivos CAB e ISO. 

![Lista de arquivos a serem transferidos](media/offline-file-list.png "Lista de arquivos")
::: moniker-end

## <a name="run-setup"></a>Executar a instalação

Quando você executa SQL Server configuração em um computador desconectado da Internet, a instalação adiciona uma página de **instalação offline** ao Assistente para que você possa especificar o local dos arquivos CAB copiados na etapa anterior.

1. Para iniciar a instalação, clique duas vezes no arquivo. ISO ou. cab para acessar a mídia de instalação. Você deve ver o arquivo **Setup. exe** .

2. Clique com o botão direito do mouse em **Setup. exe** e execute como administrador.

3. Quando o assistente de instalação exibir a página de licenciamento para componentes R ou Python de software livre, clique em **aceitar**. A aceitação dos termos de licenciamento permite que você prossiga para a próxima etapa.

4. Quando você chegar à página de **instalação offline** , em **caminho de instalação**, especifique a pasta que contém os arquivos CAB que você copiou anteriormente.

   ![Página de assistente para seleção de pasta cab](media/screenshot-sql-offline-cab-page.png "Pasta cab")

5. Continue seguindo os prompts na tela para concluir a instalação.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>Aplicar atualizações cumulativas

Recomendamos que você aplique a atualização cumulativa mais recente aos componentes do mecanismo de banco de dados e do Machine Learning. As atualizações cumulativas são instaladas por meio do programa de instalação. 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
1. Comece com uma instância de linha de base. Você só pode aplicar atualizações cumulativas a instalações existentes da versão inicial do SQL Server.

2. Em um dispositivo conectado à Internet, vá para a lista atualização cumulativa da sua versão do SQL Server:

  + [Atualizações do SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. Comece com uma instância de linha de base. Você só pode aplicar atualizações cumulativas a instalações existentes da versão inicial do SQL Server 2016, SQL Server 2016 SP 1 ou SQL Server 2016 SP 2.

2. Em um dispositivo conectado à Internet, vá para a lista atualização cumulativa da sua versão do SQL Server:

  + [Atualizações do SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)
::: moniker-end

3. Selecione a atualização cumulativa mais recente para baixar o executável.

4. Obter arquivos CAB correspondentes para R e Python. Para links de download, consulte [downloads do CAB para atualizações cumulativas em SQL Server instâncias de análise no banco de dados](sql-ml-cab-downloads.md).

5. Transfira todos os arquivos, executáveis e arquivos CAB para a mesma pasta no computador offline.

6. Execute a instalação. Aceite os termos de licenciamento e, na página seleção de recursos, examine os recursos para os quais as atualizações cumulativas são aplicadas. Você deve ver todos os recursos instalados para a instância atual, incluindo os recursos do Machine Learning.

    ![Selecionar recursos na árvore de recursos](media/cumulative-update-feature-selection.png "lista de recursos")

5. Continue com o assistente, aceitando os termos de licenciamento para distribuições de R e Python. Durante a instalação, será solicitado que você escolha o local da pasta que contém os arquivos CAB atualizados.

## <a name="set-environment-variables"></a>Definir variáveis de ambiente

Somente para a integração de recursos do R, você deve definir a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel Math Kernel Library (MKL).

1. No painel de controle, clique em sistema e**sistema** >  **de segurança** > **configurações** > avançadas do sistema**variáveis de ambiente**.

2. Crie uma nova variável de usuário ou de sistema. 

  + Definir nome da variável como`MKL_CBWR`
  + Defina o valor da variável como`AUTO`

Esta etapa requer uma reinicialização do servidor. Se você estiver prestes a habilitar a execução de script, poderá manter a reinicialização até que todo o trabalho de configuração seja concluído.

## <a name="post-install-configuration"></a>Configuração de pós-instalação

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Após a conclusão da instalação, reinicie o serviço e configure o servidor para habilitar a execução do script:

+ [Habilitar a execução de script externo](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)

Uma instalação offline inicial do SQL Server Serviços de Machine Learning requer a mesma configuração que uma instalação online:

+ [Verificar instalação](sql-machine-learning-services-windows-install.md#verify-installation)
+ [Configuração adicional, conforme necessário](sql-machine-learning-services-windows-install.md#additional-configuration)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Após a conclusão da instalação, reinicie o serviço e configure o servidor para habilitar a execução do script:

+ [Habilitar a execução de script externo](sql-r-services-windows-install.md#bkmk_enableFeature)

Uma instalação offline inicial do SQL Server R Services requer a mesma configuração que uma instalação online:

+ [Verificar instalação](sql-r-services-windows-install.md#verify-installation)
+ [Configuração adicional, conforme necessário](sql-r-services-windows-install.md#bkmk_FollowUp)
::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para verificar o status da instalação da instância e corrigir problemas comuns, consulte [relatórios personalizados para SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Para obter ajuda com mensagens ou entradas de log desconhecidas, consulte [perguntas frequentes sobre atualização e instalação-serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).
