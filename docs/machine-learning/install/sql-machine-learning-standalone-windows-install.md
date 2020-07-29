---
title: Instalar o Machine Learning Server (autônomo)
description: Configure um servidor autônomo de aprendizado de máquina para Python e R. Um servidor autônomo como instalado pela Instalação do SQL Server é funcionalmente equivalente às versões sem marca SQL do Microsoft Machine Learning Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/03/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 15280d88b2219587ee63b15e8e98421be2734fab
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85885942"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Instalar o R Server (autônomo) ou o Machine Learning Server (autônomo) usando a instalação do SQL Server
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
A Instalação do SQL Server inclui uma opção de **recurso compartilhado** para instalar um servidor de aprendizado de máquina autônomo executado fora do SQL Server. Ele é chamado **Machine Learning Server (autônomo)** e inclui R e Python. 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
A Instalação do SQL Server inclui uma opção de **recurso compartilhado** para instalar um servidor de aprendizado de máquina autônomo executado fora do SQL Server. No SQL Server 2016, esse recurso é chamado **Microsoft R Server (autônomo)** .  
::: moniker-end

Um servidor autônomo como instalado pela Instalação do SQL Server é funcionalmente equivalente às versões sem marca SQL do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), compatível com os mesmos casos de uso e cenários, incluindo:

+ Execução remota, alternando entre sessões locais e remotas no mesmo console
+ Operacionalização com nós da Web e nós de computação
+ Implantação de serviço Web: a capacidade de empacotar o script R e Python nos serviços Web
+ Coleção completa de bibliotecas de funções R e Python

Como um servidor independente dissociado do SQL Server, o ambiente R e Python é configurado, protegido e acessado usando o sistema operacional subjacente e as ferramentas fornecidas no servidor autônomo, não no SQL Server.

Como um suplemento para o SQL Server, um servidor autônomo será útil se você precisar desenvolver soluções de aprendizado de máquina de alto desempenho que possam usar contextos de computação remota para toda a gama de plataformas de dados compatíveis. Você pode alternar a execução do servidor local para um Machine Learning Server remoto em um cluster Spark ou em outra instância do SQL Server.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

Se você tiver instalado uma versão anterior, como o SQL Server 2016 R Server (autônomo) ou o Microsoft R Server, desinstale a instalação existente antes de continuar.

Como regra geral, recomendamos que você trate as instalações que reconhecem instâncias de mecanismo de banco de dados e servidor autônomo como mutuamente exclusivas para evitar a contenção de recursos, mas se você tiver recursos suficientes, não haverá proibição de instalá-los no mesmo computador físico.

Você só pode ter um servidor autônomo no computador: SQL Server Machine Learning Server (autônomo) ou SQL Server R Server (autônomo). Desinstale uma versão antes de adicionar uma nova.

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>Instalar o requisito de patch 

Somente para o SQL Server 2016: A Microsoft identificou um problema com a versão específica dos binários do Runtime Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server. Se essa atualização para os binários do Runtime de VC não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções em [Notas de Versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de runtime do VC.  
::: moniker-end

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o assistente de instalação.

2. Clique na guia **Instalação** e selecione **Nova instalação do Machine Learning Server (autônomo)** .
    
   ::: moniker-end
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![Instalar o Machine Learning Server Autônomo](media/2017setup-installation-page-mlsvr.png "Iniciar a instalação do Machine Learning Server (Autônomo)")
   ::: moniker-end
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![Instalar o Machine Learning Server Autônomo](media/2019setup-installation-page-mlsvr.png "Iniciar a instalação do Machine Learning Server (Autônomo)")
   ::: moniker-end
   ::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

3. Após a conclusão da verificação de regras, aceite os termos de licenciamento do SQL Server e selecione uma nova instalação.

4. Na página **Seleção de recurso**, a seguinte opção já deve estar selecionada:

    - **Microsoft Machine Learning Server (Autônomo)**

    - O **R** e o **Python** são selecionados por padrão. Você pode anular a seleção de qualquer uma das linguagens, mas recomendamos que você instale pelo menos uma das linguagens compatíveis.

   ::: moniker-end
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![Escolha os recursos de R ou Python](media/2017setup-features-page-mlsvr-rpy.png "Iniciar a instalação do Machine Learning Server (Autônomo)")
   ::: moniker-end
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![Escolha os recursos de R ou Python](media/2019setup-features-page-mlsvr-rpy.png "Iniciar a instalação do Machine Learning Server (Autônomo)")
   ::: moniker-end
   ::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
    
   Todas as outras opções devem ser ignoradas. 
    
   > [!NOTE]
   > Evite instalar os **Recursos compartilhados** se o computador já tiver Serviços de Machine Learning instalados para análise no banco de dados do SQL Server. Isso cria bibliotecas duplicadas.
   > 
   > Além disso, enquanto os scripts de R ou Python em execução no SQL Server são gerenciados pelo SQL Server para que não entrem em conflito com a memória usada por outros serviços de mecanismo de banco de dados, o Machine Learning Server autônomo não tem essas restrições e pode interferir com outras operações de banco de dados. Por fim, o acesso remoto via sessão RDP, que geralmente é usado para operacionalização, normalmente é bloqueado por administradores de banco de dados.
   > 
   > Por esses motivos, geralmente recomendamos que você instale o Machine Learning Server (autônomo) em um computador separado dos Serviços de Machine Learning do SQL Server.

5. Aceite os termos de licença para baixar e instalar o as distribuições de linguagem base. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**. 

6. Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o assistente de instalação.

2. Na guia **Instalação**, clique na **instalação Novo Microsoft R Server (Autônomo)** .
    
   ![Iniciar a instalação do Microsoft R Server Autônomo](media/2016-setup-installation-rsvr.png "Iniciar a instalação do Microsoft R Server Autônomo")

3. Após a conclusão da verificação de regras, aceite os termos de licenciamento do SQL Server e selecione uma nova instalação.

4. Na página **Seleção de recurso** , a seguinte opção já deve estar selecionada:
    
   - **R Server (Autônomo)**  
    
   ![Seleções de recursos para o Microsoft R Server Autônomo](media/2016setup-rserver-features.png "Seleções de recursos para o Microsoft R Server Autônomo")
    
   Todas as outras opções devem ser ignoradas. 
    
   > [!NOTE]
   > Evite instalar os **Recursos compartilhados** se estiver usando um computador que já tem o R Services instalado para análise no banco de dados do SQL Server. Isso cria bibliotecas duplicadas.
   > 
   > Enquanto os scripts de R em execução no SQL Server são gerenciados pelo SQL Server para que não entrem em conflito com a memória usada por outros serviços de mecanismo de banco de dados, o Microsoft R Server autônomo não tem essas restrições e pode interferir com outras operações de banco de dados.
   > 
   > Geralmente, recomendamos que você instale o Microsoft R Server (Autônomo) em um computador separado do SQL Server R Services (no banco de dados).

5. Aceite os termos de licença para baixar e instalar o as distribuições de linguagem base. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**. 

6. Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.
::: moniker-end

## <a name="set-environment-variables"></a>Definir variáveis de ambiente

Somente para a integração de recursos do R, é necessário definir a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel MKL (Math Kernel Library).

1. No Painel de Controle, clique em **Sistema e Segurança** > **Sistema** > **Configurações Avançadas do Sistema** > **Variáveis de Ambiente**.

2. Crie uma variável de usuário ou do sistema. 

  + Defina o nome da variável como `MKL_CBWR`
  + Defina o valor da variável como `AUTO`

3. Reinicie o servidor.

<a name="install-path"></a>

### <a name="default-installation-folders"></a>Pastas de instalação padrão

Para desenvolvimento de R e Python, é comum ter várias versões no mesmo computador. Conforme instalada pela instalação do SQL Server, a distribuição base é instalada em uma pasta associada à versão do SQL Server usada para a instalação.

A tabela a seguir lista os caminhos para distribuições de R e Python criadas por instaladores da Microsoft. Para fins de integridade, a tabela inclui caminhos gerados pela instalação do SQL Server, bem como o instalador autônomo do Microsoft Machine Learning Server.

|Versão| Método de instalação | Pasta padrão|
|----|----|----|
|SQL Server 2019 Machine Learning Server (Autônomo) |  Assistente de instalação do SQL Server 2019 |`C:\Program Files\Microsoft SQL Server\150\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\150\PYTHON_SERVER`|
|SQL Server 2017 Machine Learning Server (Autônomo) |  Assistente de instalação do SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (Autônomo) |  Instalador autônomo do Windows |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|Serviços de Machine Learning do SQL Server (no banco de dados) |Assistente de instalação do SQL Server 2019, com a opção de linguagem R|`C:\Program Files\Microsoft SQL Server\MSSQL15.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL15.<instance_name>\PYTHON_SERVICES` |
|Serviços de Machine Learning do SQL Server (no banco de dados) |Assistente de instalação do SQL Server 2017, com a opção de linguagem R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (Autônomo) |  Assistente de instalação do SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (no banco de dados) |Assistente de instalação do SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar atualizações

Recomendamos que você aplique a atualização cumulativa mais recente aos componentes do mecanismo de banco de dados e de aprendizado de máquina. As atualizações cumulativas são instaladas por meio do programa de instalação. 

Em dispositivos conectados à Internet, você pode baixar um executável de extração automática. A aplicação de uma atualização para o mecanismo de banco de dados recebe automaticamente as atualizações cumulativas para os recursos existentes do R e do Python. 

Em servidores desconectados, são necessárias etapas adicionais. Você deve obter a atualização cumulativa para o mecanismo de banco de dados, bem como os arquivos CAB para recursos de aprendizado de máquina. Todos os arquivos devem ser transferidos para o servidor isolado e aplicados manualmente.

1. Comece com uma instância de linha de base. Você só pode aplicar atualizações cumulativas a instalações existentes:

  + Machine Learning Server (Autônomo) da versão inicial do SQL Server 2019
  + Machine Learning Server (Autônomo) da versão inicial do SQL Server 2017
  + Microsoft R Server (Autônomo) da versão inicial do SQL Server 2016, SQL Server 2016 SP 1 ou SQL Server 2016 SP 2

2. Feche todas as sessões de R ou Python abertas e interrompa os processos que ainda estiverem em execução no sistema.

3. Se você habilitou a operacionalização para executar como nós da Web e nós de computação para implantações de serviço Web, faça backup do arquivo **AppSettings.json** como uma precaução. Aplicar o SQL Server 2017 CU13 ou posterior revisa esse arquivo, portanto, você pode querer uma cópia de backup para preservar a versão original.

4. Em um computador conectado à Internet, baixe a atualização cumulativa mais recente para sua versão em [Atualizações mais recentes para Microsoft SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/latest-updates-for-microsoft-sql-server).

5. Baixe a atualização cumulativa mais recente. É um arquivo executável.

6. Em um dispositivo conectado à Internet, clique duas vezes em .exe para executar a instalação e percorra o assistente para aceitar os termos de licenciamento, examine os recursos afetados e monitore o progresso até a conclusão.

7. Em um servidor sem conectividade com a Internet:

   + Obtenha os arquivos CAB correspondentes para R e Python. Para links de download, confira [Downloads CAB para atualizações cumulativas em instâncias de análise no banco de dados do SQL Server](sql-ml-cab-downloads.md).

   + Transfira todos os arquivos, os arquivos executáveis principais e os arquivos CAB para uma pasta no computador offline.

   + Clique duas vezes em .exe para executar a instalação. Ao instalar uma atualização cumulativa em um servidor sem conectividade com a Internet, você será solicitado a selecionar a localização dos arquivos .cab para R e Python.

8. Após a instalação, em um servidor para o qual você habilitou a implantação com nós da Web e nós de computação, edite **AppSettings.json**, adicionando uma entrada "MMLResourcePath" diretamente em "MMLNativePath". Por exemplo:

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [Execute o utilitário CLI do administrador](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch) para reiniciar os nós de computação e Web. Para etapas e sintaxe, confira [Monitorar, iniciar e interromper os nós Web e de computação](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start).

## <a name="development-tools"></a>Ferramentas de desenvolvimento

Uma IDE de desenvolvimento não é instalada como parte da instalação. Para obter mais informações sobre como configurar um ambiente de desenvolvimento, confira [Configurar ferramentas de R](../r/set-up-a-data-science-client.md) e [Configurar ferramentas do Python](../python/setup-python-client-tools-sql.md).

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Início Rápido: Executar o R no T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Os desenvolvedores do Python podem aprender a usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial do Python: Prever o aluguel de esquis com regressão linear nos Serviços de Machine Learning do SQL Server](../tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Tutorial do Python: Categorizar clientes que usam cluster K-means com Serviços de Machine Learning do SQL Server](../tutorials/python-clustering-model.md)
::: moniker-end