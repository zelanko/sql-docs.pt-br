---
title: Instalar o R Server ou o Machine Learning Server (autônomo) usando a instalação do SQL Server
description: Configure um servidor de aprendizado de máquina autônomo sem reconhecimento de instância para desenvolvimento de R e Python usando RevoScaleR, revoscalepy, MicrosoftML e outros pacotes.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 94ca7b3646b9005e11b3ee4968cbfaaa65d42264
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715842"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Instalar Machine Learning Server (autônomo) ou R Server (autônomo) usando a instalação do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server configuração inclui uma opção de **recurso compartilhado** para instalar um servidor de aprendizado de máquina autônomo sem reconhecimento de instância que é executado fora do SQL Server. Ele é chamado de **Machine Learning Server (autônomo)** e inclui R e Python. 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server configuração inclui uma opção de **recurso compartilhado** para instalar um servidor de aprendizado de máquina autônomo sem reconhecimento de instância que é executado fora do SQL Server. No SQL Server 2016, esse recurso é chamado **de R Server (autônomo)** .  
::: moniker-end

Um servidor autônomo como instalado pelo SQL Server configuração é funcionalmente equivalente às versões sem marca SQL do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), dando suporte aos mesmos casos de uso e cenários, incluindo:

+ Execução remota, alternando entre sessões locais e remotas no mesmo console
+ Operacionalização com nós da Web e nós de computação
+ Implantação de serviço Web: a capacidade de empacotar o script R e Python nos serviços Web
+ Coleção completa de bibliotecas de funções R e Python

Como um servidor independente dissociado do SQL Server, o ambiente R e Python é configurado, protegido e acessado usando o sistema operacional subjacente e as ferramentas fornecidas no servidor autônomo, não SQL Server.

Como um suplemento para SQL Server, um servidor autônomo será útil se você precisar desenvolver soluções de aprendizado de máquina de alto desempenho que possam usar contextos de computação remota para toda a gama de plataformas de dados com suporte. Você pode alternar a execução do servidor local para um Machine Learning Server remoto em um cluster Spark ou em outra instância do SQL Server.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>Lista de verificação de pré-instalação

Se você instalou uma versão anterior, como SQL Server servidor R 2016 (autônomo) ou Microsoft R Server, desinstale a instalação existente antes de continuar.

Como regra geral, recomendamos que você trate instalações autônomas de servidor e banco de dados que reconhecem a instância como mutuamente exclusivas para evitar a contenção de recursos, mas se você tiver recursos suficientes, não haverá proibição de instalá-los no mesmo computador físico.

Você só pode ter um servidor autônomo no computador: seja SQL Server Machine Learning Server (autônomo) ou SQL Server R Server (autônomo). Certifique-se de desinstalar uma versão antes de adicionar uma nova.

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>Instalar requisito de patch 

Somente para o SQL Server 2016: A Microsoft identificou um problema com a versão específica dos binários do Tempo de Execução Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções em [Notas de Versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de tempo de execução do VC.  
::: moniker-end

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o assistente de instalação.

2. Clique na guia **instalação** e selecione **nova instalação Machine Learning Server (autônoma)** .
    
     ![Instalar Machine Learning Server autônomos](media/2017setup-installation-page-mlsvr.png "Iniciar a instalação do Machine Learning Server autônomo")

3. Após a conclusão da verificação de regras, aceite SQL Server termos de licenciamento e selecione uma nova instalação.

4. Na página **seleção de recursos** , as seguintes opções já devem estar selecionadas:

    - Microsoft Machine Learning Server (autônomo)

    - R e Python são selecionados por padrão. Você pode desmarcar qualquer um dos idiomas, mas recomendamos que você instale pelo menos um dos idiomas com suporte.

     ![Escolha os recursos de R ou Python](media/2017setup-features-page-mlsvr-rpy.png "Iniciar a instalação do Machine Learning Server autônomo")
    
    Todas as outras opções devem ser ignoradas. 
    
    > [!NOTE]
    > Evite instalar os **recursos compartilhados** se o computador já tiver serviços de Machine Learning instalado para SQL Server análise no banco de dados. Isso cria bibliotecas duplicadas.
    > 
    > Além disso, enquanto os scripts R ou Python em execução no SQL Server são gerenciados pelo SQL Server para que não entrem em conflito com a memória usada por outros serviços de mecanismo de banco de dados, o servidor de Machine Learning autônomo não tem essas restrições e pode interferir com outras operações de banco de dados . Por fim, o acesso remoto via sessão RDP, que geralmente é usado para operacionalização, normalmente é bloqueado por administradores de banco de dados.
    > 
    > Por esses motivos, geralmente recomendamos que você instale Machine Learning Server (autônomo) em um computador separado do SQL Server Serviços de Machine Learning.

5.  Aceite os termos de licença para baixar e instalar as distribuições de idioma base. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**. 

     ![Contrato de licença do Python](media/2017setup-python-license.png "Contrato de licença do Python")

6.  Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.

Quando a instalação for concluída, consulte [relatórios personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md) para obter ajuda com erros ou avisos, consulte [perguntas frequentes sobre atualização e instalação-serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o assistente de instalação.

2. Na guia **instalação** , clique em **nova instalação do R Server (autônomo)** .
    
     ![Iniciar a instalação do R Server autônomo](media/2016-setup-installation-rsvr.png "Iniciar a instalação do R Server autônomo")

3. Após a conclusão da verificação de regras, aceite SQL Server termos de licenciamento e selecione uma nova instalação.

4.  Na página **Seleção de recurso** , a seguinte opção já deve estar selecionada:
    
    **R Server (Autônomo)**  
    
    ![Seleções de recursos para o servidor R autônomo](media/2016setup-rserver-features.png "Seleções de recursos para o servidor R autônomo")
    
    Todas as outras opções devem ser ignoradas. 
    
    > [!NOTE]
    > Evite instalar os **recursos compartilhados** se estiver executando a instalação em um computador em que o R Services já foi instalado para SQL Server análise no banco de dados. Isso cria bibliotecas duplicadas.
    > 
    > Enquanto os scripts R em execução no SQL Server são gerenciados pelo SQL Server para que não entrem em conflito com a memória usada por outros serviços de mecanismo de banco de dados, o R Server autônomo não tem essas restrições e pode interferir em outras operações de banco de dados.
    > 
    > Geralmente, recomendamos que você instale o R Server (autônomo) em um computador separado do SQL Server R Services (no banco de dados).

5.  Aceite os termos de licença para baixar e instalar as distribuições de idioma base. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**. 

6.  Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.

Quando a instalação for concluída, consulte [relatórios personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md) para obter ajuda com erros ou avisos, consulte [perguntas frequentes sobre atualização e instalação-serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

## <a name="set-environment-variables"></a>Definir variáveis de ambiente

Somente para a integração de recursos do R, você deve definir a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel Math Kernel Library (MKL).

1. No painel de controle, clique em sistema e**sistema** >  **de segurança** > **configurações** > avançadas do sistema**variáveis de ambiente**.

2. Crie uma nova variável de usuário ou de sistema. 

  + Definir nome da variável como`MKL_CBWR`
  + Defina o valor da variável como`AUTO`

3. Reinicie o servidor.

<a name="install-path"></a>

### <a name="default-installation-folders"></a>Pastas de instalação padrão

Para o desenvolvimento de R e Python, é comum ter várias versões no mesmo computador. Conforme instalado pela instalação do SQL Server, a distribuição básica é instalada em uma pasta associada à versão do SQL Server que você usou para a instalação.

A tabela a seguir lista os caminhos para distribuições de R e Python criadas por instaladores da Microsoft. Para fins de integridade, a tabela inclui caminhos gerados pela instalação do SQL Server, bem como o instalador autônomo para Microsoft Machine Learning Server.

|Version| Método de instalação | Pasta padrão|
|----|----|----|
|SQL Server 2017 Machine Learning Server (autônomo) |  Assistente de instalação do SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (autônomo) |  Instalador autônomo do Windows |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server Serviços de Machine Learning (no banco de dados) |Assistente de instalação do SQL Server 2017, com a opção de linguagem R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server servidor R 2016 (autônomo) |  Assistente de instalação do SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (no banco de dados) |Assistente de instalação do SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar atualizações

Recomendamos que você aplique a atualização cumulativa mais recente aos componentes do mecanismo de banco de dados e do Machine Learning. As atualizações cumulativas são instaladas por meio do programa de instalação. 

Em dispositivos conectados à Internet, você pode baixar um executável de extração automática. A aplicação de uma atualização para o mecanismo de banco de dados recebe automaticamente as atualizações cumulativas para os recursos existentes do R e do Python. 

Em servidores desconectados, são necessárias etapas adicionais. Você deve obter a atualização cumulativa para o mecanismo de banco de dados, bem como os arquivos CAB para recursos de aprendizado de máquina. Todos os arquivos devem ser transferidos para o servidor isolado e aplicados manualmente.

1. Comece com uma instância de linha de base. Você só pode aplicar atualizações cumulativas a instalações existentes:

  + Machine Learning Server (autônomo) da versão inicial do SQL Server 2017
  + R Server (autônomo) da versão inicial do SQL Server 2016, SQL Server 2016 SP 1 ou SQL Server 2016 SP 2

2. Feche todas as sessões de R ou Python abertas e interrompa os processos que ainda estiverem em execução no sistema.

3. Se você tiver habilitado a operacionalização para executar como nós da Web e nós de computação para implantações de serviço Web, faça backup do arquivo **appSettings. JSON** como uma precaução. Aplicar SQL Server 2017 CU13 ou posterior revisa esse arquivo, portanto, você pode querer uma cópia de backup para preservar a versão original.

4. Em um dispositivo conectado à Internet, clique no link atualização cumulativa para sua versão do SQL Server.

  + [Atualizações do SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [Atualizações do SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

5. Baixe a atualização cumulativa mais recente. É um arquivo executável.

6. Em um dispositivo conectado à Internet, clique duas vezes em. exe para executar a instalação e percorra o assistente para aceitar os termos de licenciamento, examine os recursos afetados e monitore o progresso até a conclusão.

7. Em um servidor sem conectividade com a Internet:

   + Obter arquivos CAB correspondentes para R e Python. Para links de download, consulte [downloads do CAB para atualizações cumulativas em SQL Server instâncias de análise no banco de dados](sql-ml-cab-downloads.md).

   + Transfira todos os arquivos, os arquivos executáveis principais e CAB, para uma pasta no computador offline.

   + Clique duas vezes em. exe para executar a instalação. Ao instalar uma atualização de acumulação em um servidor sem conectividade com a Internet, você será solicitado a selecionar o local dos arquivos. cab para R e Python.

8. Após a instalação, em um servidor para o qual você habilitou a operacionalização com nós da Web e nós de computação, edite **appSettings. JSON**, adicionando uma entrada "MMLResourcePath", diretamente em "MMLNativePath":

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [Execute o utilitário CLI do administrador](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch) para reiniciar os nós de computação e da Web. Para obter as etapas e a sintaxe, consulte [monitorar, iniciar e parar nós da Web e de computação](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start).

## <a name="development-tools"></a>Ferramentas de desenvolvimento

Um IDE de desenvolvimento não é instalado como parte da instalação do. Para obter mais informações sobre como configurar um ambiente de desenvolvimento, consulte [Configurar ferramentas de R](../r/set-up-a-data-science-client.md) e [Configurar ferramentas Python](../python/setup-python-client-tools-sql.md).

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores de R podem começar com alguns exemplos simples e aprender as noções básicas de como o R funciona com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise no banco de dados para desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Os desenvolvedores de Python podem aprender a usar o Python com SQL Server seguindo estes tutoriais:

+ [Tutorial: Executar o Python no T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise no banco de dados para desenvolvedores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

Para exibir exemplos de aprendizado de máquina que se baseiam em cenários do mundo real, consulte [tutoriais do Machine Learning](../tutorials/machine-learning-services-tutorials.md).
