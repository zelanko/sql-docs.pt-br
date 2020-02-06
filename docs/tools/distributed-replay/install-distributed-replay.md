---
title: Instalar o Distributed Replay
titleSuffix: SQL Server Distributed Replay
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ea1171da-f50e-4f16-bedc-5e468a46477f
author: MikeRayMSFT
ms.author: mikeray
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 4679b1f2ca6de3a358528a7ef24af8f118aa5f45
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74992175"
---
# <a name="install-distributed-replay"></a>Instalar o Distributed Replay

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Você pode instalar o Distributed Replay de uma destas três maneiras:  
  
-   [Instalar o Distributed Replay por meio do Assistente de Instalação](#bkmk_wizard)  
  
-   [Instalar o Distributed Replay usando o prompt de comando](#bkmk_command_prompt)  
  
-   [Instalar o Distributed Replay usando um arquivo de configuração](#bkmk_configuration_file)  
  
##  <a name="bkmk_wizard"></a> Instalar o Distributed Replay por meio do Assistente de Instalação  
 Instale os recursos do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay com o Assistente de Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Ao planejar onde instalar os recursos, considere o seguinte:  
  
-   Você pode instalar a ferramenta de administração no mesmo computador que o controlador do Distributed Replay ou em computadores diferentes.  
  
-   Pode haver apenas um controlador em cada ambiente do Distributed Replay.  
  
-   Você pode instalar o serviço de cliente em até 16 computadores (físicos ou virtuais).  
  
-   Apenas uma instância do serviço de cliente pode ser instalada no computador do controlador do Distributed Replay. Se o ambiente do seu Distributed Replay tiver mais de um cliente, não é recomendável instalar o serviço de cliente no mesmo computador que o controlador. Fazer assim pode reduzir a velocidade global de Distributed Replay.  
  
-   Para cenários de teste de desempenho, não é recomendável instalar a ferramenta de administração, o serviço de controlador do Distributed Replay ou serviço de cliente na instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A instalação de todos esses recursos no servidor de destino deve ser limitada a testes funcionais de compatibilidade de aplicativos.  
  
-   Depois da instalação, o serviço de controlador, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller, deve estar em execução antes de você iniciar o serviço de cliente do Distributed Replay nos clientes.  
  
> [!NOTE]  
>  Para remover ou alterar os recursos do Distributed Replay, use a janela **Programas e Recursos** do Windows no **Painel de Controle**. Selecione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] na janela **Desinstalar ou alterar um programa** e clique em **Remover** para abrir o Assistente de Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Na página **Selecionar Recursos** , marque os recursos do Distributed Replay que você deseja remover.  
  
 **Pré-requisitos:**  
  
-   Verifique se os computadores que você deseja usar atendem aos requisitos descritos no tópico [Requisitos do Distributed Replay](../../tools/distributed-replay/distributed-replay-requirements.md).  
  
-   Antes de começar este procedimento, você cria as contas de usuário de domínio com as quais os serviços de controlador e de cliente serão executados. É recomendável que essas contas não sejam membros do grupo Administradores do Windows. Para obter mais informações, veja a seção Contas de usuário e serviço no tópico [Segurança do Distributed Replay](../../tools/distributed-replay/distributed-replay-security.md) .  
  
    > [!NOTE]  
    >  É possível usar contas de usuários locais se você estiver executando a ferramenta de administração, o serviço de controlador e o serviço de cliente no mesmo computador.  
  
 **Locais de instalação:**  
  
 Supondo que você use os locais de arquivo padrão e uma instalação padrão, o diretório base estará localizado em C:\Arquivos de Programas\Microsoft SQL Server. Dentro dele, os binários e assemblies são instalados nos seguintes locais:  
  
-   Em um sistema de 32 bits:  
  
     [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Ferramentas  
  
     \- OU -  
  
     \<Diretório de Recursos Compartilhados>\Tools\\(diretório de recursos compartilhados alternativo fornecido pelo usuário)  
  
-   Em um sistema de 64 bits:  
  
     C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86)\130\Tools  
  
     \- OU -  
  
     \<Diretório de Recursos Compartilhados (x86)>\Tools\\(diretório de recursos compartilhados [x86] alternativo fornecido pelo usuário)  
  
#### <a name="to-install-distributed-replay-features"></a>Para instalar recursos do Distributed Replay  
  
1.  Para iniciar a instalação de qualquer um dos recursos do Distributed Replay, inicie o Assistente de Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
2.  A página **Regras de Suporte à Instalação** identifica problemas que podem ocorrer ao instalar os arquivos de suporte da Instalação do SQL Server. Você deve corrigir qualquer falha de suporte à Instalação antes de continuá-la.  
  
3.  Na página **Chave do Produto (Product Key)** , selecione um botão de opção para indicar se você está instalando uma edição gratuita do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou uma versão de produção do produto que tem uma chave de PID. Para obter mais informações, consulte [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
4.  Na página **Termos de Licença** , leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições da licença. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  Na página **Arquivos de Suporte à Instalação** , clique em **Instalar** para instalar ou atualizar os arquivos de Suporte à Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
6.  Na página **Função de Instalação**, selecione **Instalação de Recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** e clique em **Avançar** para continuar para a página **Seleção de Recursos**.  
  
7.  Na página **Seleção de Recursos** , configure quais recursos você deseja instalar.  
  
    -   Para instalar a ferramenta de administração, selecione **Ferramentas de Gerenciamento – Básicas**.  
  
    -   Para instalar o serviço do controlador, selecione **Distributed Replay Controller**.  
  
    -   Para instalar o serviço do cliente, selecione **Distributed Replay Client**.  
  
     **Importante**: Quando você configura o controlador Distributed Replay, pode especificar uma ou mais contas de usuário que serão usadas para executar os serviços de cliente do Distributed Replay. Esta é a lista das contas com suporte:  
  
    -   Conta de usuário do domínio  
  
    -   Conta de usuário local criada pelo usuário  
  
    -   Administrador  
  
    -   Conta virtual e MSA (Conta de Serviço Gerenciada)  
  
    -   Serviços de rede, serviços locais e sistema  
  
     Não são aceitas contas de grupo (local ou domínio) e outras contas internas (como Todos).  
  
8.  Opcionalmente, clique no botão de reticências (...) para alterar o caminho do diretório de recursos compartilhados.  
  
    1.  Em computadores de 32 bits, o caminho de instalação padrão é **C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
    2.  Em computadores de 64 bits, o caminho de instalação padrão é **C:\Arquivos de Programas (x86)\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
9. Quando tiver terminado, clique em **Avançar**.  
  
10. Na página **Regras de Instalação** , a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida sua configuração de computador. Quando o processo de validação for concluído, clique em **Avançar**.  
  
11. A página **Requisitos de Espaço em Disco** calcula o espaço em disco necessário para os recursos especificados. Em seguida, ele compara o espaço necessário com o espaço em disco disponível.  
  
12. Na página **Relatório de Erros** , especifique as informações que deseja enviar à [!INCLUDE[msCoName](../../includes/msconame-md.md)] para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, a opção de relatório de erros está habilitada.  
  
13. Na página **Regras de Configuração da Instalação** , o Verificador de Configuração do Sistema executará mais um conjunto de regras para validar a configuração do seu computador com os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você especificou.  
  
14. Na página **Pronto para Instalar o Programa** , clique em **Instalar**.  
  
    > [!IMPORTANT]  
    >  Depois de instalar o Distributed Replay, crie regras de firewall no controlador e nos computadores cliente e conceda permissões a cada computador cliente no servidor de destino. Para obter mais informações, veja [Concluir as etapas de pós-instalação](../../tools/distributed-replay/complete-the-post-installation-steps.md).  
  
### <a name="net-framework-security"></a>Segurança do .NET Framework  
 Você deve ter permissões administrativas para instalar qualquer recurso do Distributed Replay. Apenas um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenha permissões sysadmin pode adicionar as contas de serviço de cliente à função de servidor sysadmin do servidor de teste. Para obter mais informações sobre as considerações de segurança do Distributed Replay, veja [Segurança do Distributed Replay](../../tools/distributed-replay/distributed-replay-security.md).  
  
##  <a name="bkmk_command_prompt"></a> Instalar o Distributed Replay a partir do prompt de comando  
 A instalação de uma nova instância do Distributed Replay no prompt de comando permite especificar os recursos a serem instalados e como eles devem ser configurados. A instalação do prompt de comando dá suporte à instalação, reparo, atualização e desinstalação dos componentes do Distributed Replay. Quando a instalação é feita via prompt de comando, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao modo silencioso completo usando o parâmetro /Q.  
  
> [!NOTE]  
>  Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.  
  
### <a name="installation-parameters"></a>Parâmetros de instalação  
 A lista de recursos de nível superior inclui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e Ferramentas. O recurso Ferramentas instalará as Ferramentas de Gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e outros componentes compartilhados. Para instalar os componentes do Distributed Replay, especifique os seguintes parâmetros:  
  
|Componente|Parâmetro|  
|---------------|---------------|  
|Distributed Replay Controller|**DREPLAY_CTLR**|  
|Distributed Replay Client|**DREPLAY_CLT**|  
|Ferramenta de administração|**Ferramentas**|  
  
> [!IMPORTANT]  
>  Depois de instalar o Distributed Replay, crie regras de firewall no controlador e nos computadores cliente e conceda permissões a cada computador cliente no servidor de destino. Para obter mais informações, veja [Concluir as etapas de pós-instalação](../../tools/distributed-replay/complete-the-post-installation-steps.md).  
  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para a instalação.  
  
|Parâmetro|DESCRIÇÃO|Valores com suporte|  
|---------------|-----------------|----------------------|  
|/CTLRSVCACCOUNT<br /><br /> **Opcional**|Conta de serviço para o serviço do controlador do Distributed Replay Utility.|Verifica a conta e a senha|  
|/CTLRSVCPASSWORD<br /><br /> **Opcional**|Senha da conta de serviço do controlador do Distributed Replay Controller.|Verifica a conta e a senha|  
|/CTLRSTARTUPTYPE<br /><br /> **Opcional**|Tipo de inicialização do serviço do controlador do Distributed Replay.|Automático<br /><br /> Desabilitado<br /><br /> Manual|  
|/CTLRUSERS<br /><br /> **Opcional**|Especifique os usuários que têm permissões para o serviço do Distributed Replay Controller.|Conjunto de cadeias de contas de usuário que usam " " (espaço) para delimitador<br /><br /> **Importante**: quando você configura o serviço do controlador Distributed Replay, é possível especificar uma ou mais contas de usuário que serão usadas para executar os serviços de cliente do Distributed Replay. Esta é a lista das contas com suporte:<br /><br /> Conta de usuário do domínio<br /><br /> Conta de usuário local criada pelo usuário<br /><br /> Administrador<br /><br /> Administrador<br /><br /> Conta virtual e MSA (Conta de Serviço Gerenciada)<br /><br /> Serviços de rede, serviços locais e sistema<br /><br /> <br /><br /> Observação: não são aceitas contas de grupo (local ou domínio) e outras contas internas (como Todos).|  
|/CLTSVCACCOUNT<br /><br /> **Opcional**|Conta de serviço para o serviço do cliente do Distributed Replay.|Verifica a conta e a senha|  
|/CLTSVCPASSWORD<br /><br /> **Opcional**|Senha da conta de serviço do cliente Distributed Replay.|Verifica a conta e a senha|  
|/CLTSTARTUPTYPE<br /><br /> **Opcional**|Tipo de inicialização do serviço do cliente Distributed Replay.|Automático<br /><br /> Desabilitado<br /><br /> Manual|  
|/CLTCTLRNAME<br /><br /> **Opcional**|O nome do computador com o qual o cliente se comunica para o serviço do controlador do Distributed Replay.||  
|/CLTWORKINGDIR<br /><br /> **Opcional**|O diretório de trabalho para o serviço do cliente do Distributed Replay.|Caminho válido|  
|/CLTRESULTDIR<br /><br /> **Opcional**|O diretório de resultado para o serviço do cliente do Distributed Replay.|Caminho válido|  
  
### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 **Para instalar o componente do Distributed Replay Controller**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CTLR /IAcceptSQLServerLicenseTerms /CTLRUSERS="domain\user1" "domain\user2" /CTLRSVCACCOUNT="domain\svcuser" /CTLRSVCPASSWORD="password" /CTLRSTARTUPTYPE=Automatic  
```  
  
 **Para instalar o componente do cliente Distributed Replay**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CLT /IAcceptSQLServerLicenseTerms /CLTSVCACCOUNT="domain\svcuser" /CLTSVCPASSWORD="password" /CLTSTARTUPTYPE=Automatic /CLTCTLRNAME=ControllerMachineName /CLTWORKINGDIR="C:\WorkingDir" /CLTRESULTDIR="C:\ResultDir  
```  
  
##  <a name="bkmk_configuration_file"></a> Instalar o Distributed Replay usando um arquivo de configuração  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece a capacidade de gerar um arquivo de configuração baseado na entrada do usuário e nos padrões do sistema. Se você especificar que deseja instalar as ferramentas de Gerenciamento, poderá usar o arquivo de configuração para implantar os três componentes de Distributed Replay (Ferramenta de Administração, Distributed Replay Controller e Distributed Replay Client). Há suporte para a Instalação, reparo e desinstalação dos componentes do Distributed Replay.  
  
 A Instalação dá suporte ao uso do arquivo de configuração apenas por meio da linha de comando. A ordem de processamento dos parâmetros ao usar o arquivo de configuração é descrita a seguir:  
  
-   O arquivo de configuração substitui os padrões em um pacote  
  
-   Os valores da linha de comando substituem os valores do arquivo de configuração  
  
 Para obter mais informações sobre como usar um arquivo de configuração, veja [Instalar o SQL Server 2016 usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
> [!IMPORTANT]  
>  Depois de instalar o Distributed Replay, crie regras de firewall no controlador e nos computadores cliente e conceda permissões a cada computador cliente no servidor de destino. Para obter mais informações, veja [Concluir as etapas de pós-instalação](../../tools/distributed-replay/complete-the-post-installation-steps.md).  
  
#### <a name="to-generate-a-configuration-file"></a>Para gerar um arquivo de configuração  
  
1.  Siga o Assistente de Instalação até a página **Pronto para Instalar** . O caminho para o arquivo de configuração é especificado na página **Pronto para Instalar** na seção do caminho do arquivo de configuração.  
  
2.  Cancele a instalação sem realmente concluí-la para gerar o arquivo INI.  
  
#### <a name="to-install-distributed-replay-using-the-configuration-file"></a>Para instalar o Distributed Replay usando o arquivo de configuração  
  
-   Execute a instalação no prompt de comando e forneça o ConfigurationFile.ini por meio do parâmetro ConfigurationFile.  
  
 **Sintaxe de exemplo**  
  
 O seguinte é um exemplo de como especificar o arquivo de configuração no prompt de comando:  
  
```  
Setup.exe /CTLRSVCPASSWORD="ctlrsvcpswd" /CLTSVCPASSWORD="cltsvcpswd" / ConfigurationFile=ConfigurationFile.INI\  
```  
  
> [!NOTE]  
>  Você deve especificar as duas senhas na linha de comando, porque não é possível configurá-las no arquivo de configuração.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Distributed Replay Requirements](../../tools/distributed-replay/distributed-replay-requirements.md)   
 [Opções de linha de comando da ferramenta de administração &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [Configurar o Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
