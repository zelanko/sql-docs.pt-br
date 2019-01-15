---
title: Utilitário de Execução de Pacotes (dtexecui) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dtexecui.setvalues.f1
- sql13.dts.dtexecui.reporting.f1
- sql13.dts.dtexecui.datasources.f1
- sql13.dts.dtexecui.commandfiles.f1
- sql13.dts.dtexecui.logging.f1
- sql13.dts.dtexecui.general.f1
- sql13.dts.dtexecui.verification.f1
- sql13.dts.dtexecui.executionoptions.f1
- sql13.dts.dtexecui.commandline.f1
- sql13.dts.dtexecui.configuration.f1
helpviewer_keywords:
- DTExecUI utility
ms.assetid: 3d71df39-126b-4c8e-bd77-128bbd5b0887
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb2f54dde0e73733a4fd129c2d2a4d081942af52
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132246"
---
# <a name="execute-package-utility-dtexecui"></a>Utilitário de Execução de Pacotes (dtexecui)
  Use o **Utilitário do Pacote de Execução** para executar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O utilitário executa pacotes que estão armazenados em um dos três locais: o banco de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o Repositório de pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] e o sistema de arquivos Essa interface do usuário, que pode ser aberta no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou digitando **dtexecui** em um prompt de comando, é uma alternativa à execução de pacotes por meio da ferramenta de prompt de comando **DTExec** .  
  
 Os pacotes são executados no mesmo processo que o utilitário **dtexecui.exe** . Como esse utilitário é uma ferramenta de 32 bits, os pacotes são executados por meio do **dtexecui.exe** em um ambiente de 64 bits no Windows on Win32 (WOW). Ao desenvolver e testar comandos por meio do utilitário dtexecui.exe em um computador de 64 bits, será necessário testar os comandos no modo de 64 bits com a versão de 64 bits do **dtexec.exe** antes de implantar ou agendar os comandos em um servidor de produção.  
  
 O **Utilitário de Execução de Pacotes** é uma interface gráfica do usuário da ferramenta de prompt de comando do **DTExec** . A interface do usuário facilita a configuração de opções e monta automaticamente a linha de comando que é passada para a ferramenta de prompt de comando **DTExec** ao executar o pacote a partir das opções especificadas.  
  
 O **Utilitário de Execução de Pacotes** também pode ser usado para montar as linhas de comando que você usa ao executar o **DTExec** diretamente.  
  
### <a name="to-open-execute-package-utility-in-sql-server-management-studio"></a>Para abrir o utilitário Executar Pacote no SQL Server Management Studio  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Exibir** , clique em **Pesquisador de Objetos**.  
  
2.  No Pesquisador de Objetos, clique em **Conectar**e em **Integration Services**.  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , digite o nome do servidor na lista **Nome do servidor** e clique em **Conectar**.  
  
4.  Expanda a pasta e as subpastas do **Pacote Armazenado**, clique com o botão direito do mouse no pacote a ser executado e, em seguida, clique em **Executar Pacote**.  
  
### <a name="to-open-the-execute-package-utility-at-the-command-prompt"></a>Para abrir o utilitário Executar Pacote no prompt de comando  
  
-   Em uma janela do prompt de comando, execute **dtexecui**.  
  
 As seções a seguir descrevem páginas da caixa de diálogo **Utilitário de Execução de Pacotes** .  
  
## <a name="general-page"></a>Página Geral  
 Use a página **Geral** da caixa de diálogo **Utilitário de Execução de Pacotes** para especificar um nome e um local para o pacote.  
  
 O Utilitário do Pacote de Execução (dtexecui.exe) sempre executa um pacote no computador local, mesmo que ele tenha sido salvo em um computador remoto. Se o pacote remoto usar arquivos de configuração que também tenham sido salvos no servidor remoto, pode ser que o Utilitário do Pacote de Execução não localize as configurações e ocorra uma falha no pacote. Para evitar esse problema, as configurações devem ser consultadas usando um nome do compartilhamento UNC (Convenção de Nomenclatura Universal) como \\\myserver\myfile.  
  
### <a name="static-options"></a>Opções estáticas  
 **Origem do pacote**  
 Especifique o local do pacote a ser executado usando as seguintes opções:  
  
|||  
|-|-|  
|Valor|Descrição|  
|**SQL Server**|Selecione esta opção quando o pacote estiver no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifique uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e forneça um nome de usuário e senha para a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cada nome de usuário e senha adiciona as opções de **/USER** _nome de usuário_ e **/PASSWORD** _senha_ options to the comme prompt.|  
|**Sistema de arquivos**|Selecione esta opção quando o pacote estiver no sistema de arquivos.|  
|**Armazenamento de Pacotes SSIS**|Selecione esta opção quando o pacote estiver no Armazenamento de Pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] .|  
  
 Cada uma dessas seleções apresenta o seguinte conjunto de opções.  
  
 **Executar**  
 Clique para executar o pacote.  
  
 **Fechar**  
 Clique para fechar a caixa de diálogo **Utilitário do Pacote de Execução** .  
  
### <a name="dynamic-options"></a>Opções dinâmicas  
  
#### <a name="package-source--sql-server"></a>Origem do pacote = SQL Server  
 **Servidor**  
 Digite o nome do servidor onde o pacote está ou selecione um servidor da lista.  
  
 **Fazer login no servidor**  
 Especifique se o pacote deve usar a Autenticação do Windows ou a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para estabelecer conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A Autenticação do Windows é recomendada para obter melhor segurança. Com a Autenticação do Windows você não precisa especificar um nome de usuário e senha.  
  
 **Usar Autenticação do Windows**  
 Selecione esta opção para usar a Autenticação do Windows e fazer logon usando uma conta de usuário do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Usar Autenticação do SQL Server**  
 Selecione esta opção para usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando um usuário se conecta com um nome de logon e senha especificados em uma conexão não confiável, o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] efetua a autenticação verificando se foi definida uma conta de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se a senha especificada corresponde a uma senha registrada previamente. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não localizar a conta de login, ocorrerá uma falha na autenticação e o usuário receberá uma mensagem de erro.  
  
> [!IMPORTANT]  
>  Quando possível, use a Autenticação do Windows.  
  
 **Pacote**  
 Digite o nome do pacote ou clique no botão de reticências **(…)** para localizar um pacote usando a caixa de diálogo **Selecionar um Pacote do SSIS**.  
  
#### <a name="package-source--file-system"></a>Origem do pacote = Sistema de arquivos  
 **Pacote**  
 Digite o nome do pacote ou clique no botão de reticências **(…)** para localizar um pacote usando a caixa de diálogo Abrir. Por padrão, a caixa de diálogo lista somente os arquivos com a extensão .dtsx.  
  
#### <a name="package-source--ssis-package-store"></a>Origem do pacote = Armazenamento de Pacotes SSIS  
 **Servidor**  
 Digite o nome do computador onde o pacote está ou selecione um computador da lista.  
  
 **Fazer login no servidor**  
 Especifique se o pacote deve usar a Autenticação do Microsoft Windows para estabelecer conexão com a origem do pacote. A Autenticação do Windows é recomendada para obter melhor segurança. Com a Autenticação do Windows você não precisa especificar um nome de usuário e senha.  
  
 **Usar Autenticação do Windows**  
 Selecione esta opção para usar a Autenticação do Windows e efetuar login usando uma conta de usuário do Microsoft Windows.  
  
 **Usar Autenticação do SQL Server**  
 Esta opção não estará disponível quando você executar um pacote armazenado no **Repositório de Pacotes SSIS**.  
  
 **Pacote**  
 Digite o nome do pacote ou clique no botão de reticências **(…)** para localizar um pacote usando a caixa de diálogo **Selecionar um Pacote do SSIS**.  
  
## <a name="configurations-page"></a>Página Configurações  
 Use a página **Configurações** da caixa de diálogo **Utilitário de Execução de Pacotes** para selecionar os arquivos de configuração a serem carregados no momento da execução e para especificar a ordem em que serão carregados.  
  
### <a name="options"></a>Opções  
 **Arquivos de configuração**  
 Estes arquivos listam as configurações que o pacote usa. Cada arquivo de configuração adiciona uma opção **/CONFIGFILE filename** ao prompt de comando.  
  
 **Teclas de direção**  
 Selecione um arquivo de configuração na lista e use as teclas de direção à direita para alterar a ordem de carregamento. As configurações são carregadas em ordem a partir do início da lista.  
  
> [!NOTE]  
>  Caso várias configurações modifiquem a mesma propriedade, a última configuração carregada será usada.  
  
 **Adicionar**  
 Clique para adicionar configurações usando a caixa de diálogo **Abrir** . Por padrão, a caixa de diálogo lista somente os arquivos com a extensão .dtsconfig.  
  
 **Remover**  
 Selecione um arquivo de configuração na lista e clique em **Remover**.  
  
 **Executar**  
 Clique para executar o pacote.  
  
 **Fechar**  
 Clique para fechar a caixa de diálogo **Utilitário do Pacote de Execução** .  
  
## <a name="command-files-page"></a>Página Arquivos de Comando  
 Use a página **Arquivos de Comando** da caixa de diálogo **Utilitário de Execução de Pacotes** para selecionar os arquivos de comando a serem carregados no momento da execução.  
  
### <a name="options"></a>Opções  
 **Command files**  
 Lista os arquivos de comando que o pacote usa. Um pacote pode usar vários arquivos para definir as opções de linha de comando.  
  
 **Teclas de direção**  
 Selecione um arquivo de comando na lista e use as teclas de seta para a direita para alterar a ordem de carregamento. Os arquivos de comando são carregados em ordem a partir do início da lista.  
  
 **Adicionar**  
 Clique para adicionar um arquivo de comando, usando a caixa de diálogo **Abrir** .  
  
 **Remover**  
 Selecione um arquivo de comandos na caixa de texto e remova-o usando o botão **Remover** .  
  
 **Executar**  
 Clique para executar o pacote.  
  
 **Fechar**  
 Clique para fechar a caixa de diálogo **Utilitário do Pacote de Execução** .  
  
## <a name="connection-managers-page"></a>Página Gerenciadores de Conexões  
 Use a página **Gerenciadores de Conexões** da caixa de diálogo do **Utilitário de Execução de Pacotes** para editar as cadeias de conexão dos gerenciadores de conexões usados pelo pacote.  
  
### <a name="options"></a>Opções  
 **Gerenciador de Conexões**  
 Marque a caixa de seleção para que a coluna **Cadeia de Conexão** possa ser editada.  
  
 **Descrição**  
 Exiba uma descrição para cada gerenciador de conexões. As descrições não podem ser editadas.  
  
 **Cadeia de Conexão**  
 Edite a cadeia de caracteres de conexão para um gerenciador de conexões. Este campo só permitirá edições quando a caixa de seleção **Gerenciador de Conexões** estiver marcada.  
  
 **Executar**  
 Clique para executar o pacote.  
  
 **Fechar**  
 Clique para fechar a caixa de diálogo **Utilitário do Pacote de Execução** .  
  
## <a name="execution-options-page"></a>Página Opções de Execução  
 Use a página **Opções de Execução** da caixa de diálogo **Utilitário de Execução de Pacotes** para especificar as opções de tempo de execução do pacote.  
  
### <a name="options"></a>Opções  
 **Falha de pacote com avisos de validação**  
 Indique se o pacote falha quando ocorre um aviso de validação.  
  
 **Validar pacote sem executar**  
 Indique se o pacote será apenas validado.  
  
 **Executáveis máximos simultâneos**  
 Indique se você deseja especificar o número máximo de executáveis que poderá ser executado simultaneamente no pacote. Depois que você marcar esta caixa de seleção, use a caixa de rotação para especificar o número máximo de executáveis.  
  
 **Ativar pontos de verificação do pacote**  
 Indique se deseja ativar os pontos de verificação do pacote.  
  
 **Arquivo de ponto de verificação**  
 Liste o arquivo de ponto de verificação que será usado pelo pacote se você ativar os pontos de verificação do pacote.  
  
 **Procurar**  
 Se você habilitar os pontos de verificação do pacote, clique no botão Procurar **(…)** para localizar o arquivo de ponto de verificação usando a caixa de diálogo **Abrir**. Se algum arquivo de ponto de verificação já tiver sido especificado, ele será substituído pelo arquivo selecionado.  
  
 **Substituir opções de reinicialização**  
 Indique se as opções de reinicialização serão substituídas se você ativar os pontos de verificação do pacote.  
  
 **Opção de reinicialização**  
 Selecione como os pontos de verificação serão usados ao substituir as opções de reinicialização.  
  
 **Execute (executar)**  
 Clique para executar o pacote.  
  
 **Fechar**  
 Clique para fechar a caixa de diálogo **Utilitário do Pacote de Execução** .  
  
## <a name="reporting-page"></a>Página Relatório  
 Use a página **Relatório** da caixa de diálogo **Utilitário de Execução de Pacotes** para especificar eventos e informações sobre o pacote a ser registrado no console quando o pacote é executado.  
  
### <a name="options"></a>Opções  
 **Eventos do console**  
 Indique os eventos e os tipos de mensagens a serem relatados.  
  
 **Nenhuma**  
 Selecione para não gerar relatórios.  
  
 **Erros**  
 Selecione para informar mensagens de erro.  
  
 **Warnings**  
 Selecione para informar mensagens de aviso.  
  
 **Eventos personalizados**  
 Selecione para informar mensagens de eventos personalizados.  
  
 **Eventos de Pipeline**  
 Selecione para informar mensagens de eventos de fluxo de dados.  
  
 **Informações**  
 Selecione para informar mensagens de informações.  
  
 **Verbose**  
 Selecione para usar relatório verboso.  
  
 **Log de console**  
 Especifique as informações que deseja gravar no log quando o evento selecionado ocorrer.  
  
 **Nome**  
 Selecione para informar o nome da pessoa que criou o pacote.  
  
 **Computer**  
 Selecione para informar o nome do computador em que o pacote está sendo executado.  
  
 **Operador**  
 Selecione para informar o nome da pessoa que iniciou o pacote.  
  
 **Nome de origem**  
 Selecione para informar o nome do pacote.  
  
 **GUID de Origem**  
 Selecione para informar a GUID do pacote.  
  
 **GUID de Execução**  
 Selecione para informar a GUID da instância de execução do pacote.  
  
 **Mensagem**  
 Selecione para informar mensagens.  
  
 **Hora de início e Hora de término**  
 Selecione para informar quando o pacote começou e quando terminou.  
  
 **Executar**  
 Clique para executar o pacote.  
  
 **Fechar**  
 Clique para fechar a caixa de diálogo **Utilitário do Pacote de Execução** .  
  
## <a name="logging-page"></a>Página Log  
 Use a página **Log** da caixa de diálogo **Utilitário de Execução de Pacotes** para que os provedores de log sejam disponibilizados para o pacote no momento da execução. Forneça o tipo de provedor de log e a cadeia de conexão do pacote para estabelecer conexão com o log. Cada entrada de provedor de log adiciona uma opção **/LOGGER**_classid_ ao prompt de comando.  
  
### <a name="options"></a>Opções  
 **Provedor de Log**  
 Selecione um provedor de log da lista.  
  
 **Cadeia de Caracteres de Configuração**  
 Selecione o nome do gerenciador de conexões do pacote que aponta para o local do log ou digite a cadeia de caracteres de conexão para estabelecer conexão com o provedor de log.  
  
 **Remover**  
 Selecione um provedor de log e clique para removê-lo.  
  
 **Executar**  
 Clique para executar o pacote.  
  
 **Fechar**  
 Clique para fechar a caixa de diálogo **Utilitário do Pacote de Execução** .  
  
## <a name="set-values-page"></a>Página Definir Valores  
 Use a página **Definir Valores** da caixa de diálogo **Utilitário de Execução de Pacotes** para definir os valores de propriedade, executáveis, conexões, variáveis e provedores de log dos pacotes digitando os caminhos e os valores das propriedades. Cada entrada de caminho adiciona uma opção **/SET**_propertypath;value_ ao prompt de comando.  
  
### <a name="options"></a>Opções  
 **Caminho da propriedade**  
 Digite o caminho da propriedade. A sintaxe do caminho usa uma barra invertida (\\) para indicar que o item a seguir é um contêiner, usa um ponto (.) para indicar que o item a seguir é uma propriedade e usa colchetes para indicar um membro da coleção. O membro pode ser identificado pelo índice ou pelo nome. Por exemplo, o caminho da propriedade de uma variável de pacote é \Package.Variables[MyVariable].Value.  
  
 **Value**  
 Digite o valor da propriedade.  
  
 **Remover**  
 Selecione o caminho da propriedade e clique para removê-lo.  
  
 **Executar**  
 Clique para executar o pacote.  
  
 **Fechar**  
 Clique para fechar a caixa de diálogo **Utilitário do Pacote de Execução** .  
  
## <a name="verification-page"></a>Página Verificação  
 Use a página **Verificação** da caixa de diálogo **Executar Pacote** para definir os critérios de verificação do pacote.  
  
### <a name="options"></a>Opções  
 **Executar apenas pacotes assinados**  
 Selecione para executar apenas os pacotes que foram assinados.  
  
 **Verificar construção de pacote**  
 Selecione para verificar a construção do pacote.  
  
 Compilação  
 Especifique o número de compilação (build) sequencial associado à criação.  
  
 **Verificar ID do pacote**  
 Selecione para verificar a ID do pacote.  
  
 ID do Pacote  
 Especifique o número de identificação do pacote.  
  
 **Verificar ID da versão**  
 Selecione para verificar a ID da versão.  
  
 ID da Versão  
 Especifique o número de identificação da versão.  
  
 **Executar**  
 Clique para executar o pacote.  
  
 **Fechar**  
 Clique para fechar a caixa de diálogo **Utilitário do Pacote de Execução** .  
  
## <a name="command-line-page"></a>Página Linha de Comando  
 Use o nó **Linha de Comando** da caixa de diálogo **Utilitário de Execução de Pacotes** para editar a linha de comando que foi gerada pelas opções criadas por vários diálogos.  
  
### <a name="options"></a>Opções  
 **Restaurar as opções originais**  
 Clique para restaurar a linha de comando para seu estado original. Use esta opção se tiver feito modificações usando a opção **Editar a linha de comando manualmente** e quiser restaurar as opções originais da linha de comando.  
  
 **Editar a linha de comando manualmente**  
 Clique para editar a linha de comando na caixa de texto **Linha de comando** .  
  
 **Command line**  
 Exibe a linha de comando atual. Se você selecionou a opção para editar a linha de comando manualmente, ela será editável.  
  
 **Executar**  
 Clique para executar o pacote.  
  
 **Fechar**  
 Clique para fechar a caixa de diálogo **Utilitário do Pacote de Execução** .  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário dtexec](../../integration-services/packages/dtexec-utility.md)  
  
  
