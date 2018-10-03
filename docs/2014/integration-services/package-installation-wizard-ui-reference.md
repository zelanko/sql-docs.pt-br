---
title: Referência de interface do usuário do Assistente de instalação do pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.deploymentwizard.confirminstallation.f1
- sql12.dts.deploymentwizard.deploydtspackages.f1
- sql12.dts.deploymentwizard.selectinstfolder.f1
- sql12.dts.deploymentwizard.specifytargetsqlserver.f1
- sql12.dts.deploymentwizard.welcome.f1
- sql12.dts.deploymentwizard.finish.f1
- sql12.dts.deploymentwizard.configurepackages.f1
- sql12.dts.deploymentwizard.packagevalidation.f1
helpviewer_keywords:
- Package Installer Wizard
ms.assetid: 6fca44d9-5001-4644-bcf3-c2d10a674b97
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 000207f277cd0c54428cdc81b16027b7efa3aa3c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129626"
---
# <a name="package-installation-wizard-ui-reference"></a>Referência da interface do usuário do Assistente de Instalação de Pacotes
  Use o **Assistente de Instalação de Pacotes** para implantar um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , inclusive os pacotes e arquivos diversos contidos nele, bem como todas as dependências do pacote.  
  
 Antes de implantar pacotes, você pode criar configurações e implantá-las com os pacotes. O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa configurações para atualizar dinamicamente as propriedades de pacotes e objetos de pacote em tempo de execução. Por exemplo, a cadeia de conexão de uma conexão OLE DB pode ser definida dinamicamente em tempo de execução fornecendo-se uma configuração que mapeie um valor para uma propriedade que contenha a cadeia de conexão.  
  
 Você não pode executar o Assistente de Instalação de Pacotes enquanto não criar um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e um utilitário de implantação. Para obter mais informações, consulte [Implantar pacotes por meio do utilitário de implantação](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md).  
  
 As seções a seguir descrevem as páginas do assistente.  
  
## <a name="welcome-to-the-package-installation-wizard-page"></a>Bem-vindo à página Assistente de Instalação de Pacotes  
 Use o **Assistente de Instalação de Pacotes** para implantar um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para o qual você criou um utilitário de implantação de pacotes.  
  
 **Não mostrar esta página inicial novamente**  
 Selecione para ignorar a página inicial ao executar o assistente novamente.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
 **Concluir**  
 Pule para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
## <a name="configure-packages-page"></a>Configurar a página Pacotes  
 Use a página **Configurar Pacotes** para editar as configurações do pacote.  
  
### <a name="options"></a>Opções  
 **Arquivo de configuração**  
 Edite o conteúdo de um arquivo de configuração selecionando o arquivo na lista.  
  
 **Tópicos relacionados:** [Criar configurações do pacote](../../2014/integration-services/create-package-configurations.md)  
  
 **Caminho**  
 Exiba o caminho da propriedade a ser configurada.  
  
 **Tipo**  
 Exiba o tipo de dados da propriedade.  
  
 **Value**  
 Especifique o valor da configuração.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
 **Concluir**  
 Pule para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
## <a name="confirm-installation-page"></a>Página Confirmar Instalação  
 Use a página **Confirmar Instalação** para iniciar a instalação de pacotes, para exibir o status e para exibir as informações que serão usadas pelo assistente para instalar os arquivos a partir do projeto especificado.  
  
 **Próximo**  
 Instale os pacotes e suas dependências e vá para a próxima página do assistente quando instalação for concluída.  
  
 **Status**  
 Mostra o progresso da instalação do pacote.  
  
 **Concluir**  
 Vá para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
## <a name="deploy-ssis-packages-page"></a>Página Implantar Pacotes SSIS  
 Use a página **Implantar Pacotes do SSIS** para especificar onde os pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e suas dependências serão instalados.  
  
### <a name="options"></a>Opções  
 **Implantação do sistema de arquivos**  
 Distribua os pacotes e suas dependências em uma pasta especificada no sistema de arquivos.  
  
 **Implantação no SQL Server**  
 Implante os pacotes e suas dependências em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Use esta opção caso o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] compartilhe pacotes entre servidores. Todas as dependências do pacote são instaladas na pasta especificada no sistema de arquivos.  
  
 **Validar pacotes após a instalação**  
 Indique se é preciso validar os pacotes após a instalação.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
 **Concluir**  
 Pule para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
## <a name="packages-validation-page"></a>Página Validação de Pacotes  
 Use a página **Validação de Pacotes** para exibir o progresso e os resultados da validação do pacote.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
## <a name="select-installation-folder-page"></a>Página Selecionar Pasta de Instalação  
 Use a página **Selecionar Pasta de Instalação** para especificar a pasta do arquivo de sistemas na qual os pacotes e as dependências de pacotes serão instalados.  
  
### <a name="options"></a>Opções  
 **Pasta**  
 Especifique o caminho e a pasta nos quais o pacote e suas dependências serão copiados.  
  
 **Procurar**  
 Procure a pasta de destino usando a caixa de diálogo **Procurar Pasta** .  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
 **Concluir**  
 Pule para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
## <a name="specify-target-sql-server-page"></a>Página Especificar SQL Server de Destino  
 Use a página **Especificar SQL Server de Destino** para especificar as opções para implantar o pacote a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
### <a name="options"></a>Opções  
 **Nome do servidor**  
 Especifique o nome do servidor para o qual deseja implantar os pacotes.  
  
 **Usar Autenticação do Windows**  
 Especifique se será usada a Autenticação do Windows para efetuar login no servidor. A Autenticação do Windows é recomendada para obter melhor segurança.  
  
 **Usar Autenticação do SQL Server**  
 Especifique se o pacote deve usar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para fazer login no servidor. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , será preciso fornecer um nome de usuário e uma senha.  
  
 **Nome de usuário**  
 Especifique um nome de usuário.  
  
 **Senha**  
 Especifique uma senha.  
  
 **Caminho do pacote**  
 Especifique o nome da pasta lógica ou digite "/" para a pasta padrão.  
  
 Para selecionar a pasta na caixa de diálogo **Pacote do SSIS** , clique em procurar (...). Entretanto, a caixa de diálogo não fornece uma maneira para selecionar a pasta padrão. Se desejar usar a pasta padrão, digite "/" na caixa de texto.  
  
> [!NOTE]  
>  Se o caminho do pacote não for válido, a seguinte mensagem de erro será exibida: "Um ou mais argumentos são inválidos".  
  
 **Depender do armazenamento do servidor para criptografia**  
 Selecione esta opção para usar os recursos do [!INCLUDE[ssDE](../includes/ssde-md.md)] para ajudar a manter a segurança dos pacotes.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
 **Concluir**  
 Pule para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
## <a name="finish-the-package-installation-page"></a>Página Concluir o Assistente de Instalação de Pacotes  
 Use a página **Concluir o Assistente de Instalação de Pacotes** para exibir um resumo dos resultados da instalação do pacote. Esta página fornece detalhes como o nome do projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que foi implantado, os pacotes que foram instalados, os arquivos de configuração e o local da instalação.  
  
 **Concluir**  
 Para sair do assistente, clique em **Concluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Implantação de pacote &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
