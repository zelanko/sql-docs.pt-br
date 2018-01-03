---
title: "Instale o aprendizado de máquina servidor autônomo ou R Server autônomo | Microsoft Docs"
ms.custom: 
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: "35"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: d69755716ae84ed280f8af9c62a85dc861f66d75
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone"></a>Instalar o servidor de aprendizado de máquina (autônomo) ou R Server (autônomo)

Instalação do SQL Server inclui a opção para instalar uma servidor que executa fora do SQL Server de aprendizado de máquina. Essa opção pode ser útil se você precisa desenvolver soluções de aprendizado de máquina de alto desempenho que pode usar contextos de computação remota, ou que podem ser implantados em várias plataformas, inclusive:
  
  + Uma instância do SQL Server 2016 ou 2017 do SQL Server onde o aprendizado de máquina está habilitado
  + Uma instância do servidor de R ou servidor de aprendizado de máquina em um cluster Hadoop ou Spark
  + R Server ou servidor de aprendizado de máquina no Linux

Este artigo descreve como usar a instalação do SQL Server para instalar a versão autônoma do servidor de aprendizado de máquina ou Microsoft R Server. Se você tiver um Enterprise Edition ou Software Assurance, instalando o servidor de aprendizado de máquina autônomo é gratuito.

+ [Instalar o R Server](#bkmk_installRServer) -usa a instalação do SQL Server 2016
+ [Instalar o servidor de aprendizado de máquina](#bkmk_installMLServer) -usa a instalação do SQL Server 2017
+ [Atualizar uma instância existente do Microsoft R Server](#bkmk_upgrade)
+ [Ajude-me a decidir o que instalar](#bkmk_tips)

##  <a name="bkmk_installMLServer"></a>Instalar o servidor (autônomo) de aprendizado de máquina

Este recurso requer uma licença de empresa ou equivalente para **SQL Server 2017**.

Se você instalou uma versão anterior do Microsoft R Server, recomendamos que você desinstalá-lo primeiro.

Se o computador não tiver acesso à Internet, você deve baixar os instaladores de componente com antecedência. Para obter mais informações, consulte [instalação de componentes de aprendizado de máquina sem acesso à internet](./installing-ml-components-without-internet-access.md).

1. Execute a instalação do SQL Server 2017.

2. Clique o **instalação** guia e selecione **instalação novo servidor de aprendizado de máquina (autônomo)**.
    
     ![Instalar o aprendizado de máquina servidor autônomo](media/2017setup-installation-page-mlsvr.png "Iniciar instalação do aprendizado de máquina servidor autônomo")

3. Depois que a verificação de regras for concluída, aceite os termos de licenciamento do SQL Server e selecione uma nova instalação.

4. No **seleção de recursos** página, os seguintes opções já devem estar selecionadas:

    - Server (autônomo) de aprendizado de máquina da Microsoft

    - R e Python é selecionado por padrão. Você pode desmarcar qualquer idioma, mas é recomendável que você instale pelo menos um dos idiomas com suporte.

     ![Instalar o aprendizado de máquina servidor autônomo](media/2017setup-features-page-mlsvr-rpy.png "Iniciar instalação do aprendizado de máquina servidor autônomo")
    
    Todas as outras opções devem ser ignoradas. 
    
    > [!NOTE]
    > Evitar a instalação de **recursos compartilhados** se o computador já tiver instalado para análise do SQL Server no banco de dados de serviços de aprendizado de máquina. Isso cria bibliotecas duplicadas.
    > 
    > Além disso, enquanto os scripts de R ou Python em execução no SQL Server são gerenciadas pelo SQL Server, assim como para não entrar em conflito com a memória usada por outros serviços do mecanismo de banco de dados, o servidor de aprendizado de máquina autônomo não possui essas restrições e pode interferir com outras operações de banco de dados . Por fim, o acesso remoto por meio da sessão RDP, que é geralmente usado para operacionalização, geralmente está bloqueado por administradores de banco de dados.
    > 
    > Por esses motivos, geralmente recomendamos que você instale o servidor de aprendizado de máquina (autônomo) em um computador separado dos serviços de aprendizado de máquina do SQL Server.

5.  Aceite os termos de licença para baixar e instalar a componentes de aprendizado de máquina. Se você instalar ambas as linguagens, um contrato de licença separado é necessário para o Microsoft R e Python.
    
     ![Contrato de licença do Python](media/2017setup-python-license.png "contrato de licença do Python")
    
    A instalação desses componentes, e todos os pré-requisitos que possam exigir, pode levar algum tempo. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**.

6.  Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.

Para obter mais informações sobre a instalação automatizada ou off-line, consulte [instalar o Microsoft R Server da linha de comando](../../advanced-analytics/r/install-microsoft-r-server-from-the-command-line.md).

##  <a name="bkmk_installRServer"></a> Instalar o Microsoft R Server (Autônomo)

Este recurso requer uma licença de empresa ou equivalente para **SQL Server 2016**.

Se você tiver instalado qualquer versão anterior do ferramentas da Revolution Analytics ou pacotes, você deve desinstalá-los primeiro. Consulte [atualizando de uma versão mais antiga do Microsoft R Server](#bkmk_Uninstall).

1. Execute a instalação do SQL Server 2016. É recomendável que você instale o Service Pack 1 ou posterior.

2. Sobre o **instalação** , clique em **instalação de novo R Server (autônomo)**.
    
     ![Iniciar a instalação do R Server autônomo](media/2016-setup-installation-rsvr.png "iniciar a instalação do R Server autônomo")
    
3.  Na página **Seleção de recurso** , a seguinte opção já deve estar selecionada:
    
    **R Server (Autônomo)**  
    
    ![Recurso seleções para R Server autônomo](media/2016setup-rserver-features.png "seleções para R Server autônomo de recurso")
    
    Todas as outras opções devem ser ignoradas. 
    
    > [!NOTE]
    > Evitar a instalação de **recursos compartilhados** se você estiver executando a instalação em um computador onde R Services já foi instalado para análise do SQL Server no banco de dados. Isso cria bibliotecas duplicadas.
    > 
    > Enquanto os scripts de R em execução no SQL Server são gerenciados pelo SQL Server, assim como para não entrar em conflito com a memória usada por outros serviços do mecanismo de banco de dados, o R Server autônomo não possui essas restrições e pode interferir com outras operações de banco de dados.
    > 
    > Geralmente, é recomendável que você instale o servidor de aprendizado de máquina (autônomo) em um computador separado dos serviços de aprendizado de máquina do SQL Server.

4.  Aceite os termos de licença para baixar e instalar o Microsoft R Open. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**.
    
    A instalação desses componentes, e todos os pré-requisitos que possam exigir, pode levar algum tempo.
    
5.  Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.

## <a name="bkmk_upgrade"></a>Atualizar uma instância existente do servidor de R

Se você instalou uma versão anterior do Microsoft R Server (autônomo), você pode atualizar a instância para usar versões mais recentes dos componentes de R. A atualização também altera a política de suporte para usar a diretiva moderno do ciclo de vida de Software de suporte. Isso permite que a instância a ser atualizada com mais frequência, em uma agenda diferente de versões do SQL Server.

1. Baixe o instalador de baseados em Windows separado dos locais listados aqui: 

    + [Instalar o servidor para Windows de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [Instalar o R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

2. Execute o instalador e siga as instruções. Na página onde você pode selecionar os recursos a serem instalados, selecione cada instância do servidor de R que você deseja atualizar.

## <a name ="bkmk_tips"></a>Acompanhamento e dicas de instalação

Esta seção fornece informações adicionais relacionadas à instalação.

### <a name="which-version-should-i-install"></a>Qual versão devo instalar?

+ **Microsoft R Server** foi oferecida pela primeira vez como parte do SQL Server 2016 e oferece suporte a linguagem R. A última versão do Microsoft R Server foi 9.0.1.

+ **Servidor de aprendizado de máquina do Microsoft** é a versão mais recente, que foi lançada com o SQL Server 2017 e muitas atualizações de recursos, incluindo suporte para Python. Atualização cumulativa 1 para SQL Server 2017 foi liberado, o que inclui a versão 9.2.1.24 do servidor de aprendizado de máquina. Recomendamos essa atualização, se você quiser que as APIs de Python mais recente.

+ **Atualização in loco**: a instalação requer uma licença do SQL Server e atualizações normalmente são alinhadas com a cadência de lançamento do SQL Server. Isso garante que suas ferramentas de desenvolvimento estejam em sincronia com a versão em execução no contexto de computação do SQL Server. No entanto, você pode usar o instalador separado baseado no Windows para obter as atualizações mais frequentes, sob a política de suporte do ciclo de vida do Software moderno. Você também pode usar esse instalador para atualizar uma instância do SQL Server 2016 ou 2017 do SQL Server.

### <a name="default-installation-folders"></a>Pastas de instalação padrão

Quando você instala o R Server ou servidor de aprendizado de máquina usando a instalação do SQL Server, as bibliotecas de R são instaladas em uma pasta associada com a versão do SQL Server que você usou para a instalação. Nessa pasta, você também encontrará dados de exemplo, a documentação para os pacotes de base de R e a documentação das ferramentas de R e tempo de execução.

No entanto, se você instalar usando o Windows installer separado ou se você atualizar usando o Windows installer separado, bibliotecas de R são instaladas em uma pasta diferente.

Apenas para referência, se você instalou uma instância do SQL Server com serviços de R (no banco de dados) ou serviços de aprendizado de máquina (no banco de dados), e essa instância está no mesmo computador, as ferramentas e bibliotecas de R são instaladas por padrão em uma pasta diferente.

A tabela a seguir lista os caminhos para cada instalação.

|Versão| Método de instalação | Pasta padrão|
|----|----|----|
|R Server (Autônomo) |Assistente de instalação do SQL Server 2016|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Autônomo) |Instalador autônomo do Windows|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Servidor do Machine Learning (Autônomo) |  Assistente de instalação do SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Servidor do Machine Learning (Autônomo) |  Instalador autônomo do Windows |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services (no Banco de Dados) |Assistente de instalação do SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Serviços de Machine Learning (No Banco de Dados) |Assistente de instalação do SQL Server 2017|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES` ou `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

### <a name="development-tools"></a>Ferramentas de desenvolvimento

Um IDE de desenvolvimento não é instalado como parte da instalação. Ferramentas adicionais não são necessárias, como as ferramentas padrão estão incluídas que pode ser fornecida com uma distribuição de R ou Python.

É recomendável que você tente a nova versão do [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]. Visual Studio oferece suporte tanto R e Python, bem como ferramentas de desenvolvimento de banco de dados, a conectividade com o SQL Server e ferramentas de BI. No entanto, você pode usar qualquer ambiente de desenvolvimento preferencial, incluindo RStudio.

## <a name="troubleshooting"></a>Solução de problemas

Esta seção lista alguns problemas comuns que devem ser considerados ao instalar o servidor de aprendizado de máquina ou R.

### <a name="incompatible-version-of-r-client-and-r-server"></a>Versão incompatível do Cliente do R e R Server

Se você instala o cliente do Microsoft R e usá-lo para executar R em um contexto de computação do SQL Server remoto, você poderá receber um erro como este:

*Você está executando a versão 9.0.0 do cliente do Microsoft R no seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

No SQL Server 2016, era necessário que a versão do R que estava em execução no SQL Server R Services ser exatamente o mesmo que as bibliotecas de cliente do Microsoft R. Esse requisito foi removido em versões posteriores. No entanto, é recomendável que você sempre obter as versões mais recentes do que os componentes de aprendizado de máquina e instale todos os service packs. 

Se você tiver uma versão anterior do Microsoft R Server e precisa garantir a compatibilidade com o cliente do Microsoft R 9.0.0, instalar as atualizações que estão descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262).

### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Instalando o Microsoft R Server em uma instância do SQL Server instalada no Windows Core

Na versão RTM do SQL Server 2016, houve um problema conhecido ao adicionar o Microsoft R Server para uma instância de edição do Windows Server Core. Esse problema foi corrigido.

Se você encontrar esse problema, você pode aplicar a correção descrita no [KB3164398](https://support.microsoft.com/kb/3164398) para adicionar o recurso de R para a instância existente no Windows Server Core.   Para obter mais informações, consulte [Não é possível instalar o Microsoft R Server (Autônomo) em um sistema operacional Windows Server Core](https://support.microsoft.com/kb/3168691).

###  <a name="bkmk_Uninstall"></a>Atualizando de uma versão mais antiga do Microsoft R Server

Se você tiver instalado uma versão de pré-lançamento do Microsoft R Server, será necessário desinstalá-la antes de atualizar para uma versão mais nova.

**Para desinstalar o R Server (Autônomo)**

1.  No **Painel de Controle**, clique em **Adicionar/Remover Programas**e selecione `Microsoft SQL Server 2016 <version number>`.

2.  Na caixa de diálogo com opções para **Adicionar**, **Reparar**ou **Remover** componentes, selecione **Remover**.
  
3.  Na página **Selecionar Recursos** em **Recursos Compartilhados**, selecione **R Server (Autônomo)**. Clique em **Avançar**e em **Concluir** para desinstalar apenas os componentes selecionados.

### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>A instalação falha com o erro “Apenas um único produto do Revolution Enterprise pode ser instalado por vez”.

Você poderá receber esse erro se tiver uma instalação mais antiga dos produtos da Revolution Analytics ou uma versão de pré-lançamento do SQL Server R Services. É necessário desinstalar todas as versões anteriores antes de instalar uma versão mais nova do Microsoft R Server. Não há suporte para a instalação lado a lado com outras versões das ferramentas do Revolution Enterprise.

No entanto, há suporte para instalações lado a lado ao usar um R Server Autônomo com o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ou o SQL Server 2016.

### <a name="unable-to-uninstall-older-components"></a>Não é possível desinstalar os componentes mais antigos

Se você tiver problemas ao remover uma versão mais antiga, talvez será necessário editar o Registro para remover as chaves relacionadas.

> [!IMPORTANT]
> Esse problema se aplicará somente se você tiver instalado uma versão de pré-lançamento do Microsoft R Server ou uma versão CTP do SQL Server 2016 R Services.
  
1. Abra o Registro do Windows e localize esta chave: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.
2. Exclua as seguintes entradas, se houver, e se a chave contiver apenas o valor `sEstimatedSize2`:
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (para o 8.0.2)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (para o 8.0.1)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (para o 8.0.0)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (para o 7.5.0)
  
## <a name="see-also"></a>Consulte também

[Servidor do Machine Learning (autônomo)](../../advanced-analytics/r/r-server-standalone.md)
