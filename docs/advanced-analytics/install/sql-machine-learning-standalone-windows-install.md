---
title: Instalar o R Server ou Machine Learning Server (autônomo) usando a instalação do SQL Server | Microsoft Docs
description: Configure um servidor de aprendizado de máquina sem reconhecimento de instância autônoma para o desenvolvimento de R e Python usando o RevoScaleR, revoscalepy, MicrosoftML e outros pacotes.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7cf5cf2d78900c5bbd7607666afecc64aa98267f
ms.sourcegitcommit: e4e9f02b5c14f3bb66e19dec98f38c012275b92c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2018
ms.locfileid: "43118544"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Instalar o R Server (autônomo) usando a instalação do SQL Server ou Machine Learning Server (autônomo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Instalação do SQL Server inclui um **recurso compartilhado** opção para instalar uma instância insensíveis, servidor autônomo de aprendizado de máquina que é executado fora do SQL Server. No SQL Server 2016, esse recurso é chamado **R Server (autônomo)**. No SQL Server 2017, ele é chamado **Machine Learning Server (autônomo)** e inclui o R e Python. 

Um servidor autônomo como instalado pela instalação do SQL Server é funcionalmente equivalente às versões do SQL sem marca [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), que dão suporte aos mesmos casos de uso e cenários, incluindo a execução remota operacionalização e os serviços web e a coleção completa de funções de RevoScaleR e revoscalepy.

Como um servidor independente dissociado do SQL Server, o ambiente de R e Python está configurado, protegido e acessados usando as ferramentas fornecidas no servidor autônomo, não o SQL Server e o sistema operacional subjacente.

Como um suplemento do SQL Server, um servidor autônomo é útil se você precisa para desenvolver o alto desempenho aprendizado de máquina soluções que podem usar remote contextos de computação, alternância de forma intercambiável entre o servidor local e um servidor de aprendizado de máquina remota um Spark do cluster ou em outro SQL Server da instância.
  

## <a name="bkmk_prereqs"> </a> Lista de verificação de pré-instalação

Se você instalou uma versão anterior, como o SQL Server 2016 R Server (autônomo) ou Microsoft R Server, desinstale a instalação existente antes de continuar.

Como regra geral, é recomendável que você trate servidor autônomo e o banco de dados engine reconhecimento de instância instalações como mutuamente exclusivas para evitar a contenção de recursos, mas se você tiver recursos suficientes, não há proibição instalando-os sobre o mesmo computador físico.

Você só pode ter um servidor autônomo no computador: SQL Server 2017 Machine Learning Server ou SQL Server 2016 R Server (autônomo). Você deve desinstalar manualmente uma versão antes de instalar uma versão diferente.

::: moniker range="=sql-server-2016"
 ###  <a name="bkmk_ga_instalpatch"></a> Instalar o requisito de patch 

Para apenas para o SQL Server 2016: a Microsoft identificou um problema com a versão específica dos binários do Microsoft VC + + 2013 Runtime que são instalados como um pré-requisito pelo SQL Server. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções em [Notas de Versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de tempo de execução do VC.  
::: moniker-end

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o Assistente de instalação.

2. Clique o **instalação** guia e, em seguida, selecione **instalação do novo Machine Learning Server (autônomo)**.
    
     ![Instale o Machine Learning Server autônomo](media/2017setup-installation-page-mlsvr.png "Iniciar instalação do Machine Learning Server autônomo")

3. Depois que a verificação de regras for concluída, aceite os termos de licenciamento do SQL Server e selecione uma nova instalação.

4. No **seleção de recursos** página, as seguintes opções já devem estar selecionadas:

    - Microsoft Machine Learning Server (autônomo)

    - R e Python é selecionadas por padrão. Você pode cancelar a seleção de qualquer uma dessas linguagens, mas é recomendável que você instale pelo menos um dos idiomas com suporte.

     ![Instale o Machine Learning Server autônomo](media/2017setup-features-page-mlsvr-rpy.png "Iniciar instalação do Machine Learning Server autônomo")
    
    Todas as outras opções devem ser ignoradas. 
    
    > [!NOTE]
    > Evite instalar o **recursos compartilhados** se o computador já tiver instalado para análise do SQL Server no banco de dados de serviços do Machine Learning. Isso cria bibliotecas duplicadas.
    > 
    > Além disso, ao passo que os scripts do R ou Python em execução no SQL Server são gerenciados pelo SQL Server, então, como não entrar em conflito com a memória usada por outros serviços do mecanismo de banco de dados, o servidor de aprendizado de máquina autônomo não possui tais restrições e pode interferir com outras operações de banco de dados . Por fim, o acesso remoto por meio da sessão RDP, que é geralmente usado para operacionalização, geralmente é bloqueado por administradores de banco de dados.
    > 
    > Por esses motivos, geralmente recomendamos que você instale o Machine Learning Server (autônomo) em um computador separado dos serviços do SQL Server Machine Learning.

5.  Aceite os termos de licença para baixar e instalar o idioma base distribuições. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**. 

     ![Contrato de licença do Python](media/2017setup-python-license.png "contrato de licença do Python")

6.  Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.

Quando a instalação for concluída, consulte [relatórios personalizados para o SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md) para obter ajuda com erros ou avisos, consulte [atualização e instalação perguntas Frequentes - serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o Assistente de instalação.

2. Sobre o **instalação** , clique em **instalação do novo R Server (autônomo)**.
    
     ![Inicie a instalação do R Server autônomo](media/2016-setup-installation-rsvr.png "iniciar a instalação do R Server autônomo")

3. Depois que a verificação de regras for concluída, aceite os termos de licenciamento do SQL Server e selecione uma nova instalação.

4.  Na página **Seleção de recurso** , a seguinte opção já deve estar selecionada:
    
    **R Server (Autônomo)**  
    
    ![Seleções para R Server autônomo de recurso](media/2016setup-rserver-features.png "seleções para R Server autônomo de recurso")
    
    Todas as outras opções devem ser ignoradas. 
    
    > [!NOTE]
    > Evite instalar o **recursos compartilhados** se você estiver executando a instalação em um computador em que R Services já tiver sido instalado para análise do SQL Server no banco de dados. Isso cria bibliotecas duplicadas.
    > 
    > Enquanto os scripts de R em execução no SQL Server são gerenciados pelo SQL Server, então, como não entrar em conflito com a memória usada por outros serviços do mecanismo de banco de dados, o R Server autônomo não possui essas restrições e pode interferir com outras operações de banco de dados.
    > 
    > Geralmente, recomendamos que você instale o Microsoft R Server (autônomo) em um computador separado do SQL Server R Services (no banco de dados).

5.  Aceite os termos de licença para baixar e instalar o idioma base distribuições. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**. 

6.  Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.

Quando a instalação for concluída, consulte [relatórios personalizados para o SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md) para obter ajuda com erros ou avisos, consulte [atualização e instalação perguntas Frequentes - serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

### <a name="default-installation-folders"></a>Pastas de instalação padrão

Para o desenvolvimento de R e Python, é comum ter várias versões no mesmo computador. Como instalado pela instalação do SQL Server, a distribuição de base é instalada em uma pasta associada à versão do SQL Server que você usou para a instalação.

A tabela a seguir lista os caminhos para as distribuições do R e Python criados pelos instaladores da Microsoft. Para fins de integridade, a tabela inclui caminhos gerados pelo programa de instalação do SQL Server, bem como o instalador autônomo para o Microsoft Machine Learning Server.

|Versão| Método de instalação | Pasta padrão|
|----|----|----|
|SQL Server 2017 Machine Learning Server (autônomo) |  Assistente de instalação do SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (autônomo) |  O instalador autônomo do Windows |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|Serviços de Machine Learning do SQL Server 2017 (no banco de dados) |Assistente de instalação do SQL Server 2017, com a opção de linguagem R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (autônomo) |  Assistente de instalação do SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (no banco de dados) |Assistente de instalação do SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

## <a name="development-tools"></a>Ferramentas de desenvolvimento

Um IDE de desenvolvimento não está instalado como parte da instalação. Para obter mais informações sobre como configurar um ambiente de desenvolvimento, consulte [configurar ferramentas do R](../r/set-up-a-data-science-client.md) e [configurar ferramentas Python](../python/setup-python-client-tools-sql.md).

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise de no banco de dados para os desenvolvedores do R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Os desenvolvedores de Python podem aprender como usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial: Executar o Python no T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise de no banco de dados para desenvolvedores do Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).
