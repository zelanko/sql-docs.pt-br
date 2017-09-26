---
title: "Ajuda de F1 do Assistente de atualização de pacote SSIS | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.is.upgradewizard.ssisupgradewizard.f1
- sql13.is.upgradewizard.selectsourcelocation.f1
- sql13.is.upgradewizard.selectdestinationlocation.f1
- sql13.is.upgradewizard.selectpackagemgtoptions.f1
- sql13.is.upgradewizard.selectpackages.f1
- sql13.is.upgradewizard.completewizard.f1
- sql13.is.upgradewizard.upgradingpackage.f1
ms.assetid: 7fe886ff-1ea5-48d5-9d20-d5da36dd1cd7
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0e9c1eccc9a14c580ba733fc3c4f63e88db92d60
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="ssis-package-upgrade-wizard-f1-help"></a>Ajuda F1 do Assistente de Atualização de Pacotes SSIS
  Use o Assistente de atualização de pacote do SSIS para atualizar pacotes criados por versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para o formato de pacote para a versão atual do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 **Para executar o Assistente de Atualização de Pacotes SSIS**  
  
-   [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  

## <a name="ssis-upgrade-wizard"></a>Assistente de atualização do SSIS
  
### <a name="options"></a>Opções  
 **Não mostrar esta página novamente.**  
 Ignore a página inicial da próxima vez que abrir o assistente.  
 
## <a name="select-source-location-page"></a>Página de seleção de local de origem
 Use a página **Selecionar Local de Origem** para especificar a origem a partir da qual os pacotes serão atualizados.  
  
> [!NOTE]  
>  Essa página só está disponível quando o Assistente de Atualização de Pacotes do [!INCLUDE[ssIS](../includes/ssis-md.md)] é executado por meio do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou no prompt de comando.  
  
### <a name="static-options"></a>Opções estáticas  
 **Origem do pacote**  
 Selecione o local de armazenamento que contém os pacotes a serem atualizados. Os valores dessa opção estão relacionados na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Sistema de Arquivos**|Indica que os pacotes a serem atualizados estão em uma pasta no computador local.<br /><br /> Para que o assistente faça backup dos pacotes originais antes de atualizá-los, esses pacotes devem ser armazenados no sistema de arquivos. Para obter mais informações, consulte o tópico de instruções.|  
|**Armazenamento de Pacotes SSIS**|Indica que os pacotes a serem atualizados estão no armazenamento de pacotes. O repositório de pacotes consiste no conjunto de pastas do sistema de arquivos gerenciado pelo serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Gerenciamento de pacotes &#40;Serviço SSIS&#41;](../integration-services/service/package-management-ssis-service.md).<br /><br /> Selecione esse valor para exibir as opções dinâmicas de **Origem do pacote** correspondentes.|  
|**Microsoft SQL Server**|Indica que os pacotes a serem atualizados são de uma instância existente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Selecione esse valor para exibir as opções dinâmicas de **Origem do pacote** correspondentes.|  
  
 **Pasta**  
 Digite o nome de uma pasta que contém os pacotes que você quer atualizar ou clique em **Procurar** e localize a pasta.  
  
 **Procurar**  
 Navegue para localizar a pasta que contém os pacotes você deseja atualizar.  
  
### <a name="package-source-dynamic-options"></a>Opções dinâmicas de Origem do pacote  
  
#### <a name="package-source--ssis-package-store"></a>Origem do pacote = Repositório de Pacotes SSIS  
 **Servidor**  
 Digite o nome do servidor que tem os pacotes a serem atualizados ou selecione esse servidor na lista.  
  
#### <a name="package-source--microsoft-sql-server"></a>Origem do pacote = Microsoft SQL Server  
 **Servidor**  
 Digite o nome do servidor que tem os pacotes a serem atualizados ou selecione esse servidor na lista.  
  
 **Usar a autenticação do Windows**  
 Selecione para usar a Autenticação do Windows para estabelecer conexão com o servidor.  
  
 **Usar Autenticação do SQL Server**  
 Selecione para usar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para estabelecer conexão com o servidor. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , será preciso fornecer um nome de usuário e uma senha.  
  
 **Nome de usuário**  
 Digite o nome de usuário que a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usará para estabelecer conexão com o servidor.  
  
 **Senha**  
 Digite a senha que a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usará para estabelecer conexão com o servidor.  
 
## <a name="select-destination-location-page"></a>Página de seleção de local de destino
 Use a página **Selecionar Local de Destino** para especificar o destino no qual os pacotes atualizados serão salvos.  
  
> [!NOTE]  
>  Essa página só está disponível quando o Assistente de Atualização de Pacotes do [!INCLUDE[ssIS](../includes/ssis-md.md)] é executado por meio do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou no prompt de comando.  
 
### <a name="static-options"></a>Opções estáticas  
 **Salvar no local de origem**  
 Salve os pacotes atualizados ao mesmo local especificado na página **Selecionar Local de Origem** do assistente.  
  
 Se os pacotes originais estiverem armazenados no sistema de arquivos e você desejar que o assistente faça backup desses pacotes, selecione a opção **Salvar no local de origem** . Para obter mais informações, consulte [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
 **Selecionar novo local de destino**  
 Salve os pacotes atualizados no local de destino especificado nesta página.  
  
 **Origem do pacote**  
 Especifique onde os pacotes de atualização serão armazenados. Os valores dessa opção estão relacionados na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Sistema de Arquivos**|Indica que os pacotes atualizados serão salvos em uma pasta no computador local.|  
|**Armazenamento de Pacotes SSIS**|Indica que os pacotes atualizados serão salvos no armazenamento de pacotes do Integration Services. O repositório de pacotes consiste no conjunto de pastas do sistema de arquivos gerenciado pelo serviço do Integration Services. Para obter mais informações, consulte [Gerenciamento de pacotes &#40;Serviço SSIS&#41;](../integration-services/service/package-management-ssis-service.md).<br /><br /> Selecione esse valor para exibir as opções dinâmicas de **Origem do pacote** correspondentes.|  
|**Microsoft SQL Server**|Indica que os pacotes atualizados serão salvos em uma instância existente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Selecione esse valor para exibir as opções dinâmicas de **Origem do pacote** correspondentes.|  
  
 **Pasta**  
 Digite o nome de uma pasta na qual os pacotes atualizados serão salvos ou clique em **Procurar** e localize a pasta.  
  
 **Procurar**  
 Procure para localizar a pasta na qual os pacotes atualizados serão salvos.  
  
### <a name="package-source-dynamic-options"></a>Opções dinâmicas de Origem do pacote  
  
#### <a name="package-source--ssis-package-store"></a>Origem do pacote = Repositório de Pacotes SSIS  
 **Servidor**  
 Digite o nome do servidor onde os pacotes de atualização serão salvos ou selecione um servidor na lista.  
  
#### <a name="package-source--microsoft-sql-server"></a>Origem do pacote = Microsoft SQL Server  
 **Servidor**  
 Digite o nome do servidor onde os pacotes de atualização serão salvos ou selecione esse servidor na lista.  
  
 **Usar a autenticação do Windows**  
 Selecione para usar a Autenticação do Windows para estabelecer conexão com o servidor.  
  
 **Usar Autenticação do SQL Server**  
 Selecione para usar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para estabelecer conexão com o servidor. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , será preciso fornecer um nome de usuário e uma senha.  
  
 **Nome de usuário**  
 Digite o nome de usuário a ser usado quando a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] for usada para estabelecer conexão com o servidor.  
  
 **Senha**  
 Digite a senha a ser usada quando a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] for usada para estabelecer conexão com o servidor.  
 
## <a name="select-package-management-options-page"></a>Página Selecione as opções de gerenciamento de pacote
  Use a página **Selecionar Opções de Gerenciamento de Pacote** para especificar opções para atualizar pacotes.  
  
 **Para executar o Assistente de Atualização de Pacotes SSIS**  
  
-   [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
### <a name="options"></a>Opções  
 **Atualizar cadeias de conexão para usar novos nomes de provedor**  
 Atualize as cadeias de conexão para usar os nomes dos seguintes provedores da versão atual do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   Provedor OLE DB para[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 O Assistente de Atualização de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] só atualiza cadeias de conexão armazenadas em gerenciadores de conexões. O assistente não atualiza cadeias de conexão construídas dinamicamente com a linguagem de expressão do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ou o código de uma tarefa Script.  
  
 **Validar pacotes de atualização**  
 Valide os pacotes de atualização e salve só os pacotes aprovados na validação.  
  
 Se você não selecionar essa opção, o assistente não validará pacotes de atualização. Portanto, o assistente salvará todos os pacotes de atualização, independentemente de sua validez. O assistente salva os pacotes de atualização no destino especificado na página **Selecionar Local de Destino** do assistente.  
  
 A validação prolonga o processo de atualização. Recomendamos que você não selecione essa opção para pacotes grandes que provavelmente serão atualizados com êxito.  
  
 **Criar novas IDs de pacote**  
 Crie novas IDs para os pacotes de atualização.  
  
 **Continuar o processo de atualização quando uma atualização de pacote falhar**  
 Especifique que o Assistente de Atualização de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] deve continuar atualizando os pacotes restantes quando não for possível atualizar um pacote.  
  
 **Conflitos de nome de pacote**  
 Especifique como o assistente deve manipular pacotes que têm o mesmo nome. Os valores dessa opção estão relacionados na tabela a seguir.  
  
 **Substituir arquivos existentes do pacote**  
 Substitui o pacote existente pelo pacote de atualização do mesmo nome.  
  
 **Adicionar sufixos numéricos para atualizar nomes de pacote**  
 Adiciona um sufixo numérico ao nome do pacote de atualização.  
  
 **Não atualizar pacotes**  
 Interrompe a atualização dos pacotes e exibe um erro quando o assistente é concluído.  
  
 Essas opções não estão disponíveis quando a opção **Salvar no local de origem** é selecionada na página **Selecionar Local de Destino** do assistente.  
  
 **Ignorar configurações**  
 Não carrega configurações de pacotes durante a atualização de pacotes. A seleção dessa opção reduz o tempo necessário para atualizar o pacote.  
  
 **Backup dos pacotes originais**  
 Configure o assistente para fazer backup dos pacotes originais em uma pasta **SSISBackupFolder** . O assistente cria a pasta **SSISBackupFolder** como uma subpasta da pasta que contém os pacotes originais e os pacotes atualizados.  
  
> [!NOTE]  
>  Essa opção só está disponível quando você especifica que os pacotes originais e os pacotes atualizados estão armazenados no sistema de arquivos e na mesma pasta.  

## <a name="select-packages-page"></a>Selecione a página pacotes
  Use a página **Selecionar Pacotes** para selecionar os pacotes a serem atualizados. Essa página lista os pacotes que estão armazenados no local especificado na página **Selecionar Local de Origem** do assistente.  
  
### <a name="options"></a>Opções  
 **Nome do pacote existente**  
 Selecione um ou mais pacotes para atualizar.  
  
 **Nome do pacote de atualização**  
 Forneça o nome do pacote de destino ou use o nome padrão que o assistente fornece.  
  
> [!NOTE]  
>  Você também pode alterar o nome do pacote de destino depois de atualizar o pacote. No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ou no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], abra o pacote atualizado e altere o nome de pacote.  
  
 **Senha**  
 Especifique a senha que é usada para descriptografar os pacotes de atualização selecionados.  
  
 **Aplicar à seleção**  
 Aplique a senha especificada para descriptografar os pacotes de atualização selecionados.  
 
## <a name="complete-the-wizard-page"></a>Página concluir o Assistente
  Use a página **Concluir o Assistente** para revisar e confirmar as opções de atualização de pacote que você selecionou. Esta é a última página do assistente que permite voltar e alterar as opções dessa sessão do assistente.  
  
### <a name="options"></a>Opções  
 **Resumo de opções**  
 Revise as opções de atualização que você selecionou no assistente. Para alterar qualquer opção, clique em **Voltar** para voltar a páginas anteriores do assistente.
 
## <a name="upgrading-the-packages-page"></a>Atualizando a página pacotes
  Use a página **Atualizando os Pacotes** para exibir o progresso da atualização de pacotes e para interromper o processo de atualização. O Assistente de Atualização de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] atualiza os pacotes selecionados um por um.  
  
### <a name="options"></a>Opções  
 **Painel de mensagens**  
 Exibe mensagens de progresso e informações de resumo durante o processo de atualização.  
  
 **Ação**  
 Exibe as ações na atualização.  
  
 **Status**  
 Exibe o resultado de cada ação.  
  
 **Mensagem**  
 Exibe as mensagens de erro que cada ação gera.  
  
 **Parar**  
 Pare a atualização do pacote.  
  
 **Relatório**  
 Selecione o que deseja fazer com o relatório que contém os resultados da atualização do pacote:  
  
-   Exiba o relatório online.  
  
-   Salve o relatório em um arquivo.  
  
-   Copie o relatório na área de transferência.  
  
-   Envie o relatório como uma mensagem de email.  

## <a name="view-upgraded-packages"></a>Exibir os pacotes atualizados
### <a name="view-upgraded-packages-that-were-saved-to-a-sql-server-database-or-to-the-package-store"></a>Exibir os pacotes atualizados que foram salvos em um banco de dados do SQL Server ou no armazenamento do pacote
  
No [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], em Pesquisador de Objetos, conecte-se à instância local do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]e expanda o nó **Pacotes Armazenados** para saber quais pacotes foram atualizados.  
  
### <a name="view-upgraded-packages-that-were-upgraded-from-sql-server-data-tools"></a>Exibir os pacotes atualizados que foram atualizados do SQL Server Data Tools  
  
No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], em Gerenciador de Soluções, abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e expanda o nó **Pacotes SSIS** para ver os pacotes atualizados.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar pacotes do Integration Services](../integration-services/install-windows/upgrade-integration-services-packages.md)  
  
  
