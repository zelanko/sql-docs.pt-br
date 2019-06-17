---
title: Instalar a linguagem R e componentes do Python sem acesso à internet - aprendizagem de máquina do SQL Server
description: Offline ou desconectada Machine Learning R e Python instalação na instância isolada do SQL Server atrás de um firewall de rede.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: da9676f029bb917adf15690b6870583fb0465fc4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65836211"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>Instalar o R e Python de aprendizado em computadores sem acesso à internet de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Por padrão, instaladores de se conectar a sites de download da Microsoft para obter necessárias e os componentes atualizados para o aprendizado de máquina no SQL Server. Se as restrições de firewall impedirem que o instalador do alcance esses sites, você pode usar um dispositivo conectado à internet para baixar arquivos, transferir arquivos para um servidor offline e, em seguida, execute a instalação.

Análise no banco de dados consistem na instância do mecanismo de banco de dados, além de componentes adicionais para a integração de R e Python, dependendo da versão do SQL Server. 

+ SQL Server 2017 inclui o R e Python 
+ SQL Server 2016 é somente para R.

Em um servidor isolado, os recursos específicos do idioma de R/Python e aprendizado de máquina são adicionados por meio de arquivos CAB. 

## <a name="sql-server-2017-offline-install"></a>Instalação offline do SQL Server 2017

Para instalar o SQL Server 2017 serviços Machine Learning (R e Python) em um servidor isolado, começar baixando a versão inicial do SQL Server e os arquivos CAB correspondentes para R e Python oferecem suporte. Mesmo se você planeja atualizar imediatamente o servidor para usar a atualização cumulativa mais recente, uma versão inicial deve ser instalada primeiro.

> [!Note]
> SQL Server 2017 não tem pacotes de serviço. É a primeira versão do SQL Server para usar a versão inicial como a única linha de base, com a manutenção por meio de atualizações cumulativas somente. 

### <a name="1---download-2017-cabs"></a>1 - Baixar CABs de 2017

Em um computador com uma conexão de internet, baixe os arquivos CAB fornecendo recursos de R e Python para a versão inicial e a mídia de instalação do SQL Server 2017. 

Versão  |Link de download  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2 - obter a mídia de instalação do SQL Server 2017

1. Em um computador com uma conexão de internet, baixe o [programa de instalação do SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Clique duas vezes no programa de instalação e escolha o **baixar mídia** tipo de instalação. Com essa opção, a instalação cria um arquivo. ISO (ou. cab) local que contém a mídia de instalação.

   ![Escolher tipo de instalação de mídia de download](media/offline-download-tile.png "baixar mídia")

## <a name="sql-server-2016-offline-install"></a>Instalação offline do SQL Server 2016

A análise no banco de dados do SQL Server 2016 é somente para R, com apenas dois CAB arquivos para os pacotes de produto e a distribuição da Microsoft do R de código-fonte aberto, respectivamente. Comece instalando qualquer uma dessas versões: RTM, SP 1, SP 2. Depois que uma instalação básica estiver em vigor, as atualizações cumulativas podem ser aplicadas como uma próxima etapa.

Em um computador com uma conexão de internet, baixe os arquivos CAB usados pela instalação para instalar a análise no banco de dados no SQL Server 2016. 

### <a name="1---download-2016-cabs"></a>1 - Baixar CABs de 2016

Versão  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2 - obter a mídia de instalação do SQL Server 2016

Você pode instalar o SQL Server 2016 RTM, SP 1 ou SP 2 como sua primeira instalação no computador de destino. Qualquer uma dessas versões pode aceitar uma atualização cumulativa.

Uma forma de obter um arquivo. ISO que contém a mídia de instalação é por meio [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/). Entrar e, em seguida, use o **Downloads** link para localizar a versão do SQL Server 2016 que você deseja instalar. O download está na forma de um arquivo. ISO, que pode ser copiado para o computador de destino para uma instalação offline.

## <a name="transfer-files"></a>Transferir arquivos

Copie a mídia de instalação do SQL Server (. ISO ou. cab) e arquivos de análise no banco de dados CAB para o computador de destino. Coloque os arquivos CAB e o arquivo de mídia de instalação na mesma pasta no computador de destino, como a pasta TEMP * % do usuário de instalação.

A pasta % TEMP % é necessária para os arquivos CAB do Python. Para R, você pode usar % TEMP % ou defina o parâmetro myrcachedirectory para o caminho do CAB.

Captura de tela a seguir mostra os arquivos CAB do SQL Server 2017 e ISO. Downloads do SQL Server 2016 uma aparência diferentes: nome do arquivo menos arquivos (nenhum Python) e a mídia de instalação é para 2016.

![Lista de arquivos a serem transferidos](media/offline-file-list.png "lista de arquivos")

## <a name="run-setup"></a>Executar a instalação

Quando você executa a instalação do SQL Server em um computador desconectado da internet, a instalação adiciona uma **instalação Offline** página ao Assistente para que você possa especificar o local dos arquivos CAB que você copiou na etapa anterior.

1. Para iniciar a instalação, clique duas vezes no arquivo. ISO ou. cab para acessar a mídia de instalação. Você deve ver a **setup.exe** arquivo.

2. Clique com botão direito **setup.exe** e executar como administrador.

3. Quando o Assistente de instalação exibe a página de licenciamento para componentes de R ou Python do código-fonte aberto, clique em **Accept**. Aceitação dos termos de licenciamento permite que você prossiga para a próxima etapa.

4. Quando chegar a **instalação Offline** página, na **instalar caminho**, especifique a pasta que contém os arquivos CAB que você copiou anteriormente.

   ![Página do Assistente para seleção de pasta do cab](media/screenshot-sql-offline-cab-page.png "pasta CAB")

5. Continuar a seguir as instruções na tela para concluir a instalação.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>Aplicar atualizações cumulativas

É recomendável que você aplique a atualização cumulativa mais recente para o mecanismo de banco de dados e componentes de aprendizado de máquina. As atualizações cumulativas são instaladas por meio do programa de instalação. 

1. Comece com uma instância de linha de base. Só é possível aplicar atualizações cumulativas para as instalações existentes do SQL Server:

  + Versão inicial do SQL Server 2017
  + Versão inicial do SQL Server 2016, SQL Server 2016 SP 1 ou SQL Server 2016 SP 2

2. Em um dispositivo conectado à internet, vá para a lista de atualização cumulativa para sua versão do SQL Server:

  + [Atualizações do SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [Atualizações do SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Selecione a atualização cumulativa mais recente para baixar o arquivo executável.

4. Obter os arquivos CAB correspondentes para R e Python. Para obter links de download, consulte [CAB baixa atualizações cumulativas na análise do SQL Server no banco de dados de instâncias](sql-ml-cab-downloads.md).

5. Transferência de todos os arquivos, executáveis e arquivos CAB, na mesma pasta no computador offline.

6. Execute a instalação. Aceite os termos de licenciamento e, na página de seleção de recursos, analise os recursos para os quais as atualizações cumulativas são aplicadas. Você deve ver todos os recursos instalados para a instância atual, incluindo recursos de aprendizado de máquina.

  ![Selecione os recursos na árvore de recursos](media/cumulative-update-feature-selection.png "lista de recursos")

5. Prossiga com o assistente, aceitando os termos de licenciamento para distribuições do R e Python. Durante a instalação, você precisará escolher o local da pasta que contém os arquivos CAB atualizados.

## <a name="set-environment-variables"></a>Configurar variáveis de ambiente

Para R integração de recursos somente, você deve definir a **MKL_CBWR** variável de ambiente [garantir uma saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) cálculos da Intel MKL Math Kernel Library ().

1. No painel de controle, clique em **sistema e segurança** > **sistema** > **configurações avançadas do sistema**  >   **Variáveis de ambiente**.

2. Crie uma nova variável de sistema ou usuário. 

  + Nome de variável de conjunto para `MKL_CBWR`
  + Defina o valor da variável como `AUTO`

Esta etapa requer uma reinicialização do servidor. Se você está prestes a habilitar a execução do script, você pode adiar a reinicialização até que todo o trabalho de configuração é feita.

## <a name="post-install-configuration"></a>Configuração de pós-instalação

Após a instalação for concluída, reinicie o serviço e, em seguida, configure o servidor para habilitar a execução do script:

+ [Habilitar a execução do script externo (SQL Server 2017)](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)
+ [Habilitar a execução do script externo (SQL Server 2016)](sql-r-services-windows-install.md#bkmk_enableFeature)

Uma instalação offline inicial dos serviços de aprendizado de máquina do SQL Server 2017 ou SQL Server 2016 R Services requer a mesma configuração de uma instalação online:

+ [Verificar a instalação do](sql-machine-learning-services-windows-install.md#verify-installation) (para SQL Server 2016, clique em [aqui](sql-r-services-windows-install.md#verify-installation)).
+ [Configuração adicional conforme necessário](sql-machine-learning-services-windows-install.md#additional-configuration) (para SQL Server 2016, clique em [aqui](sql-r-services-windows-install.md#bkmk_FollowUp)).

## <a name="next-steps"></a>Próximas etapas

Para verificar o status da instalação da instância e corrigir problemas comuns, consulte [relatórios personalizados para o SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Para obter ajuda com quaisquer mensagens desconhecidas ou de entradas de log, consulte [atualização e instalação perguntas Frequentes - serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).

