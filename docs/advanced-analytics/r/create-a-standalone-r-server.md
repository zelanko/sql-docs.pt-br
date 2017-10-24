---
title: "Criar um R Server Autônomo | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4f39a03ecf7b74e0e1305d692a71c28609c80bf0
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-standalone-r-server"></a>Criar um R Server Autônomo

Instalação do SQL Server inclui a opção para instalar uma servidor que executa fora do SQL Server de aprendizado de máquina. 

Essa opção pode ser útil se você precisa desenvolver soluções de R de alto desempenho no Windows e, em seguida, compartilhar as soluções em outras plataformas. Você também pode usar a opção de servidor para configurar um ambiente para criação de soluções de suporte para a execução nesses contextos de computação remota:
  
  + Uma instância do SQL Server que executa o R Services
  + Uma instância do R Server que usa um cluster Hadoop ou Spark
  + Análise de no banco de dados Teradata
  + R Server em execução no Linux 

Este tópico descreve as etapas de instalação na instalação do SQL Server para Microsoft R Server e o servidor de aprendizado de máquina do Microsoft.

## <a name="which-should-i-install"></a>Qual deve instalar?

**Microsoft R Server** foi oferecida pela primeira vez como parte do SQL Server 2016 e oferece suporte a linguagem R. A última versão do Microsoft R Server foi 9.0.1.
No SQL Server de 2017, R Server foi renomeado **Microsoft Server de aprendizado de máquina**, com suporte adicional para Python. A versão mais recente do Microsoft Server de aprendizado de máquina é 9.1.0.

Microsoft R Server e o servidor de aprendizado de máquina do Microsoft exigem Enterprise Edition.

+ [Instale o Microsoft R Server (autônomo) usando a instalação do SQL Server](#bkmk_installRServer)
+ [Instale o Microsoft Machine Learning Server (autônomo) usando a instalação do SQL Server](#bkmk_installRServer) 

  A instalação requer uma licença do SQL Server e as atualizações normalmente são alinhadas à cadência de lançamento do SQL Server. Isso garante que suas ferramentas de desenvolvimento estejam em sincronia com a versão em execução no contexto de computação do SQL Server.

+ [Instalar o R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

  Com essa opção, R Server está instalado usando a política de suporte do ciclo de vida modernos. Você também pode executar esse instalador após a instalação para atualizar uma instância do SQL Server 2016. No momento, você _não é possível_ suporte a Python usando essa opção de instalação. Para obter o Python, você deve instalar o servidor de aprendizado de máquina usando a instalação do SQL Server 2017.

##  <a name="bkmk_installRServer"></a>Como instalar o Microsoft Server (autônomo) de aprendizado de máquina
  
1. Se você instalou uma versão anterior do Microsoft R Server, recomendamos que você desinstalá-lo primeiro.

2. Execute a instalação do SQL Server 2017.
  
3. Clique o **instalação** guia e selecione **instalação novo servidor de aprendizado de máquina (autônomo)**.

4. Depois que a verificação de regras for concluída, aceite os termos de licenciamento do SQL Server e selecione uma nova instalação.

5. No **seleção de recursos** página, os seguintes opções já devem estar selecionadas:
    
    - Server (autônomo) de aprendizado de máquina da Microsoft
    
    - R e Python é selecionado por padrão.
    
    Todas as outras opções devem ser ignoradas.

6.  Aceite os termos de licença para baixar e instalar a componentes de aprendizado de máquina. Um contrato de licença separado é necessário para o Microsoft R Open e Python. 
    
    Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**. 
    
    A instalação desses componentes (e todos os pré-requisitos que possam exigir) pode levar algum tempo. 
    
    Se o computador não tiver acesso à Internet, você deve baixar os instaladores de componente com antecedência. Para obter mais informações, consulte [componentes de instalação ML sem acesso à Internet](./installing-ml-components-without-internet-access.md). 
    
7.  Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.


Para obter mais informações sobre a instalação automatizada ou offline, consulte [Instalar o Microsoft R Server por meio da linha de comando](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md).

###  <a name="bkmk_installRServer"></a> Instalar o Microsoft R Server (Autônomo)  

1. Se você instalou uma versão anterior do Microsoft R Server, ou qualquer versão das ferramentas da Revolution Analytics, você deve desinstalá-lo primeiro.  Consulte [Atualizando de uma versão anterior do Microsoft R Server](#bkmk_Uninstall).

2. Execute a instalação do SQL Server 2016. É recomendável que você instale o Service Pack 1 ou posterior.

3. Na guia **Instalação** , clique na instalação **Novo R Server (Autônomo)** .
    
     ![Opção de instalação do R Server Autônomo](media/rsql-rstandalonesetup.png "Opção de instalação do R Server Autônomo")
    
4.  Na página **Seleção de recurso** , a seguinte opção já deve estar selecionada:
    
    **R Server (Autônomo)**  
    
    Todas as outras opções devem ser ignoradas. Não instale o mecanismo de databae do SQL Server ou SQL Server R Services.
    
5.  Aceite os termos de licença para baixar e instalar o Microsoft R Open. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**. 
    
    A instalação desses componentes (e todos os pré-requisitos que possam exigir) pode levar algum tempo.
    
6.  Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.  


### <a name="upgrade-an-existing-r-server-to-901"></a>Atualizar um servidor existente do R para 9.0.1

Se você instalou uma versão anterior do Microsoft R Server (autônomo), você pode atualizar a instância para usar versões mais recentes dos componentes de R. A atualização também altera o servidor de política de suporte do ciclo de vida modernos. Isso permite que a instância a ser atualizada com mais frequência, em uma agenda diferente de versões do SQL Server.

1. Instale o Microsoft R Server (Autônomo), se ele ainda não tiver sido instalado.

2. Baixar o instalador baseado no Windows separado dos locais listado aqui: [executar Microsoft R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall).

3. Execute o instalador e siga [estas instruções](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download-r-server-installer).


### <a name="change-in-default-folder-for-r-packages"></a>Alterar pasta padrão para os pacotes de R

Quando você instalar usando a instalação do SQL Server, bibliotecas de R são instaladas em uma pasta associada com a versão do SQL Server que você usou para a instalação. Nesta pasta, você também localizará dados de exemplo, a documentação dos pacotes básicos do R e a documentação das ferramentas e do tempo de execução de R.

**R Server (Autônomo) com a instalação usando o SQL Server 2016**

`C:\Program Files\Microsoft SQL Server\130\R_SERVER`

**R Server (Autônomo) com a instalação usando o SQL Server 2017**

`C:\Program Files\Microsoft SQL Server\140\R_SERVER`

**Configuração usando o instalador autônomo do Windows**

No entanto, se você instalar usando o Windows installer separado ou se você atualizar usando o Windows installer separado, bibliotecas de R são movidas para a seguinte pasta R Server:

`C:\Program Files\Microsoft\R Server\R_SERVER`
      
**Em bancos de dados de serviços de instalação de R Servies ou aprendizado de máquina**

Se você instalou uma instância do SQL Server com serviços de R (no banco de dados) ou serviços de aprendizado de máquina (no banco de dados), e essa instância está no mesmo computador, as ferramentas e bibliotecas de R são instaladas por padrão em uma pasta diferente:

`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`

Não chame diretamente os utilitários ou pacotes de R associados à instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Se o servidor de R e R Services estão instalados no mesmo computador, quando você precisa executar RGui ou outras ferramentas, use as ferramentas de R e os pacotes instalados na pasta R_SERVER.


### <a name="development-tools"></a>Ferramentas de desenvolvimento

Um IDE de desenvolvimento não é instalado como parte da instalação. Ferramentas adicionais não são necessárias, como as ferramentas padrão estão incluídas que pode ser fornecida com uma distribuição de R ou Python.

É recomendável que você tente a nova versão do [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], como o Visual Studio oferece suporte a ferramentas de R e Python, bem como SQL Server e o BI. No entanto, você pode usar qualquer ambiente de desenvolvimento preferencial, incluindo RStudio.

## <a name="troubleshooting"></a>Solução de problemas  

### <a name="incompatible-version-of-r-client-and-r-server"></a>Versão incompatível do Cliente do R e R Server

Se você instalar a última versão do Cliente do Microsoft R e usá-la para executar o R no SQL Server usando um contexto de computação remota, poderá receber o seguinte erro:

*Você está executando a versão 9.0.0 do cliente do Microsoft R em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

Normalmente, a versão do R instalada com o SQL Server R Services é atualizada quando as versões de serviço são publicadas. Para garantir que você sempre tem as versões mais atualizadas dos componentes do R, instale todos os service packs. Para compatibilidade com o Cliente do Microsoft R 9.0.0, é necessário instalar as atualizações descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262). 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Instalando o Microsoft R Server em uma instância do SQL Server instalada no Windows Core

Na versão RTM do SQL Server 2016, houve um problema conhecido ao adicionar o Microsoft R Server para uma instância de edição do Windows Server Core. Esse problema foi corrigido.

Se você tiver esse problema, aplique a correção descrita no [KB3164398](https://support.microsoft.com/kb/3164398) para adicionar o recurso do R à instância existente no Windows Server Core.   Para obter mais informações, consulte [Não é possível instalar o Microsoft R Server (Autônomo) em um sistema operacional Windows Server Core](https://support.microsoft.com/kb/3168691).


###  <a name="bkmk_Uninstall"></a> Atualizando de uma versão anterior do Microsoft R Server

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

[Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)


