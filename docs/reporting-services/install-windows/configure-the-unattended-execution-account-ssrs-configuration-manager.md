---
title: Configurar a conta de execução autônoma (Gerenciador de Configurações) | Microsoft Docs
description: O Reporting Services fornece uma conta especial que é usada para o processamento autônomo de relatórios e para enviar solicitações de conexão pela rede.
ms.date: 12/04/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.custom: seo-lt-2019, seo-mmd-2019
ms.topic: conceptual
helpviewer_keywords:
- no credentials option [Reporting Services]
- security [Reporting Services], unattended report processing
- unattended report processing [Reporting Services]
- credentials [Reporting Services]
- external data sources [Reporting Services]
- accounts [Reporting Services]
- reports [Reporting Services], processing
ms.assetid: 4e50733e-bd8c-4bf6-8379-98b1531bb9ca
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b09992c53a680e19bd5676e8944b2ddab8358296
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74866313"
---
# <a name="configure-the-unattended-execution-account-ssrs-configuration-manager"></a>Configurar a conta de execução autônoma (Gerenciador de configurações do SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece uma conta especial que é usada para o processamento autônomo de relatórios e para enviar solicitações de conexão pela rede. A conta é usada das seguintes maneiras:  
  
-   Enviar solicitações de conexão pela rede para relatórios que usam autenticação do banco de dados ou conexão a fontes de dados de relatórios externos que não requeiram ou utilizem autenticação. Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).

-   Recuperar arquivos de imagem externos usados no relatório. Se desejar usar um arquivo de imagem e ele não puder ser acessado com acesso Anônimo, você poderá configurar a conta de processamento autônomo de relatórios e conceder à conta a permissão para acessar o arquivo.  
  
 O termo processamento autônomo de relatórios se refere a qualquer processo de execução de relatório que seja disparado por um evento (um evento controlado por agenda ou um evento de atualização de dados) e não a uma solicitação de usuário. O servidor de relatório usa a conta de processamento autônomo de relatórios para fazer logon no computador que hospeda a fonte de dados externa. Essa conta é necessária porque as credenciais da conta de serviço do Servidor de Relatório nunca são usadas para conectar a outros computadores.  
  
> [!IMPORTANT]  
>  A configuração da conta é opcional. Entretanto, se não for configurada, suas opções de conexão a algumas fontes de dados ficarão limitadas e talvez você não possa recuperar arquivos de imagem a partir de computadores remotos. Se você configurar a conta, deverá mantê-la atualizada. Especificamente, se você permitir que uma senha expire ou se as informações da conta forem alteradas no Active Directory, será exibido o seguinte erro na próxima vez que um relatório for processado: "Falha de logon (rsLogonFailed) Falha de logon: nome de usuário desconhecido ou senha incorreta". A manutenção apropriada da conta de processamento autônomo de relatórios é essencial, mesmo se você nunca recuperar imagens externas ou enviar solicitações de conexão para computadores externos. Se você configurar a conta, mas depois descobrir que não a está usando, poderá excluí-la para evitar tarefas rotineiras de manutenção de conta.  
  
## <a name="how-to-configure-the-account"></a>Como configurar a conta  
 Você deve usar uma conta de usuário de domínio. Para que sirva à sua finalidade pretendida, essa conta deve ser diferente daquela usada para executar o serviço Servidor de Relatório. Certifique-se de usar uma conta que tenha permissões mínimas (acesso somente leitura com permissões de conexão de rede é suficiente) e acesso limitado apenas aos computadores que forneçam fontes de dados e recursos ao servidor de relatório.  
  
 Para especificar a conta, você pode usar a ferramenta de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou o utilitário **rsconfig** . A maneira mais fácil de configurar a conta de execução autônoma é executar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e especificar credenciais na página Conta de Execução.  
  
1.  Inicie a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e conecte-se à instância do servidor de relatório que você deseja configurar. Para obter instruções, veja [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Na página Conta de Execução, selecione **Especificar uma conta de execução**.  
  
3.  Digite a conta e a senha, digite novamente a senha e clique em **Aplicar**.  
  
### <a name="using-rsconfig-utility"></a>Usando o utilitário RSCONFIG  
 Outra maneira de definir a conta é usar o utilitário **rsconfig** . Para especificar a conta, use o argumento **-e** do **rsconfig**. A especificação do argumento **-e** para **rsconfig** orienta o utilitário a gravar as informações da conta no arquivo de configuração. Não é necessário especificar um caminho para RSreportserver.config. Siga estas etapas para configurar a conta.  
  
1.  Crie ou selecione uma conta de domínio que tenha acesso a computadores e servidores que forneçam dados ou serviços a um servidor de relatório. Você deve usar uma conta que tenha permissões reduzidas (por exemplo, permissões somente leitura).  
  
2.  Abra um prompt de comando: No menu **Iniciar**, clique em **Executar**, digite **cmd** e, em seguida, clique em **OK**.  
  
3.  Digite o seguinte comando para configurar a conta em uma instância local do servidor de relatório:  
  
     **rsconfig -e -u\<domain/username> -p\<password>**  
  
 **rsconfig -e** dá suporte a argumentos adicionais. Para obter mais informações sobre a sintaxe e como exibir exemplos de comandos, consulte [Utilitário rsconfig &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md).
 
### <a name="how-account-information-is-stored"></a>Como as informações de conta são armazenadas  
 Quando você define a conta, as seguintes configurações são especificadas como valores criptografados no arquivo RSreportserver.config na instância local ou remota do servidor de relatório.  
  
```  
<UnattendedExecutionAccount>  
     <UserName></UserName>  
     <Password></Password>  
     <Domain></Domain>  
</UnattendedExecutionAccount>  
```  
  
 Depois de definir os valores, você não pode descriptografá-los para exibir os valores em texto sem-formatação. Se você digitar incorretamente os valores ou esquecer os valores que foram especificados, use a ferramenta de Configuração do Reporting Services ou execute **rsconfig -e** para iniciar novamente.  
  
## <a name="how-to-use-the-unattended-report-processing-account"></a>Como usar a conta de processamento autônomo de relatórios.  
 Para recuperar arquivos de imagem, o servidor de relatório usa automaticamente a conta e nenhuma ação específica é necessária de sua parte. Para usar a conta a fim de conectar-se a fontes de dados externas que forneçam dados para relatórios, você deve especificar uma opção **Tipo de Credencial** na página de propriedades da fonte de dados do relatório ou compartilhada:  
  
-   No [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] ou em um site do SharePoint, selecione a opção **Credenciais não são necessárias** .  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
 A conta de processamento autônomo de relatórios é usada principalmente para conectar-se a servidores externos, não como um logon para servidores de banco de dados. Para usar as credenciais de conta para fazer logon em um banco de dados, especifique as credenciais na cadeia de caracteres de conexão. Você poderá especificar **Integrated Security=SSPI** se o servidor de banco de dados der suporte à segurança integrada do Windows e se a conta usada para o processamento autônomo de relatórios tiver permissão para ler o banco de dados. Caso contrário, digite o nome do usuário e a senha na cadeia de conexão, onde ela aparecerá em texto não criptografado para qualquer usuário com permissão para editar propriedades da conexão da fonte de dados.  
  
 Embora você possa usar a conta de processamento autônomo de relatórios para recuperar dados depois que a conexão é estabelecida, isso não é recomendável. A conta deve ser usada em funções muito específicas. Se você usá-la para recuperar dados, estará distorcendo o fim a que ela se destina.  
  
## <a name="how-to-maintain-the-unattended-report-processing-account"></a>Como manter a conta de processamento autônomo de relatórios  
 Depois de definir a conta, você deve assegurar-se de que a conta e a senha sejam mantidas atualizadas. Você pode usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para atualizar os parâmetros de configuração que armazenam informações sobre essa conta.  
  
1.  Inicie a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e conecte-se à instância do servidor de relatório que você deseja configurar.  
  
2.  Na página Conta de Execução, verifique se **Especificar uma conta de execução** está selecionado.  
  
3.  Digite a nova conta ou senha, digite novamente a senha e clique em **Aplicar**.  
  
## <a name="how-to-delete-the-unattended-report-processing-account"></a>Como excluir a conta de processamento autônomo de relatórios  
 Se você não estiver usando a conta, poderá excluí-la para evitar tarefas rotineiras de manutenção de conta.  
  
1.  Inicie a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e conecte-se à instância do servidor de relatório que você deseja configurar.  
  
2.  Na página Conta de Execução, desmarque **Especificar uma conta de execução**.  
  
3.  Clique em **Aplicar**.  
  
 As informações da conta serão removidas do arquivo RSReportServer.config.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de Configurações do Reporting Services (modo nativo do SSRS).](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
  
