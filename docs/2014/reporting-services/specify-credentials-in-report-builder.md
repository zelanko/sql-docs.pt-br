---
title: Especificar credenciais no Construtor de Relatórios | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7412ce68-aece-41c0-8c37-76a0e54b6b53
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 432b41216418cd1ad1bae70557c95a589f5e78dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101140"
---
# <a name="specify-credentials-in-report-builder"></a>Especificar as credenciais no Construtor de Relatórios
  As credenciais autenticam o usuário que está tentando recuperar dados de uma fonte de dados. O proprietário da fonte de dados determina o tipo de credenciais que devem ser usadas. Por exemplo, um administrador de banco de dados pode especificar que o usuário deve fornecer um nome de usuário do Windows e uma senha.  
  
 Em uma definição de relatório, cada definição de fonte de dados especifica um nome, uma cadeia de conexão, se a segurança integrada deve ser usada e qual prompt exibir se credenciais forem exigidas, mas não forem especificadas. As credenciais não são salvas na definição de relatório. Após a publicação de um relatório no servidor de relatório, as fontes de dados podem ser gerenciadas independentemente a partir da definição do relatório. Os proprietários de fontes de dados podem especificar credenciais para fontes de dados inseridas e compartilhadas no servidor de relatório.  
  
> [!NOTE]  
>  O administrador do servidor de relatório deve conceder a um usuário as permissões adequadas para navegar pelo servidor de relatório e selecionar fontes de dados compartilhadas ou modelos ou para abrir ou salvar relatórios. Para obter mais informações, consulte [instalar, desinstalar e Construtor de relatórios suporte](../../2014/reporting-services/install-uninstall-and-report-builder-support.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-when-credentials-are-used"></a>Compreendendo quando as credenciais são usadas  
 No Construtor de Relatórios, as credenciais são usadas, em geral, quando você se conecta a um servidor de relatório ou a tarefas relacionadas a dados, tais como criar uma fonte de dados inserida, executar uma consulta de conjunto de dados ou visualizar um relatório. As credenciais não são armazenadas no relatório. Elas são gerenciadas separadamente no servidor de relatório ou no cliente local. A lista a seguir descreve os tipos de credenciais que talvez precisem ser fornecidos, o local em que são armazenados e como são usados:  
  
-   As credenciais do servidor de relatório inseridas na [Caixa de diálogo Logon do Reporting Services &#40;Construtor de Relatórios&#41;](report-builder/reporting-services-login-dialog-box-report-builder.md).  
  
     Quando você salvar, publicar ou navegar em um servidor de relatório ou site do SharePoint pela primeira vez, talvez seja necessário inserir suas credenciais. As credenciais inseridas são usadas até a sessão do Construtor de Relatórios terminar. Se você optar por salvar as credenciais, elas serão armazenadas com segurança nas configurações de usuário de seu computador. Nas sessões subsequentes do Construtor de Relatórios, as credenciais salvas são usadas para se conectar ao mesmo servidor de relatório ou site do SharePoint. O administrador do servidor de relatório ou do SharePoint especifica o tipo de credencial a ser usado.  
  
-   As credenciais de fonte de dados inseridas na página [Caixa de diálogo Propriedades da Fonte de Dados, Credenciais &#40;Construtor de Relatórios&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md) de uma fonte de dados inserida.  
  
     Essas credenciais são usadas pelo servidor de relatório para fazer uma conexão de dados com a fonte de dados externa. Para alguns tipos de fontes de dados, as credenciais podem ser armazenadas com segurança no servidor de relatório. Essas credenciais permitem ao outros usuários executar o relatório sem fornecer credenciais para a conexão de dados subjacente.  
  
-   As credenciais de fonte de dados inseridas em [Caixa de diálogo Inserir Credenciais da Fonte de Dados &#40;Construtor de Relatórios&#41;](report-data/enter-data-source-credentials-dialog-box-report-builder.md) ao executar uma consulta de conjunto de dados, atualizar campos de conjuntos de dados ou visualizar o relatório.  
  
     Essas credenciais são usadas para fazer uma conexão de dados do Construtor de Relatórios com a fonte de dados ou visualizar um relatório configurado para solicitar credenciais. As credenciais que você insere nessa caixa de diálogo não são armazenadas no servidor de relatório e não estão disponível para uso de outros usuários. O Construtor de Relatórios armazena em cache as credenciais durante a sessão de edição de relatório de forma que você não precise inseri-las toda vez que executar a consulta ou visualizar o relatório.  
  
     Para fontes de dados compartilhadas, use a opção **Salvar minha senha** para salvar as credenciais localmente nas configurações de usuário de seu computador. O Construtor de Relatórios usa as credenciais salvas toda vez que uma conexão é feita com a fonte de dados externa correspondente.  
  
 Para obter mais informações, consulte [Caixa de diálogo Propriedades de Fonte de Dados, Geral &#40;Construtor de Relatórios&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md) e [Visualizando relatórios no Construtor de Relatórios](report-builder/previewing-reports-in-report-builder.md).  
  
## <a name="types-of-credentials"></a>Tipos de credenciais  
 O tipo de credenciais ao qual uma fonte de dados oferece suporte é especificado pelo proprietário da fonte de dados. Por exemplo, para acessar um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , talvez seja necessário fornecer um nome de usuário e uma senha de logon do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para acessar uma fonte de dados diferente, talvez seja necessário fornecer um nome de usuário e uma senha de logon do Windows. Algumas fontes de dados não requerem credenciais.  
  
### <a name="options-for-specifying-credentials"></a>Opções para especificar credenciais  
 As seguintes opções estão disponíveis para especificar credenciais para uma fonte de dados:  
  
-   Usar o usuário atual do Windows (também conhecido como segurança integrada).  
  
-   Usar um nome de usuário e senha armazenados.  
  
-   Solicitar credenciais ao usuário.  
  
-   Nenhuma credencial é necessária.  
  
### <a name="windows-integrated-security"></a>Segurança integrada do Windows  
 Quando você seleciona **Usar a autenticação do Windows (segurança integrada)**, o token de segurança do usuário atual é passado para a fonte de dados. Nesse caso, não é solicitado que o usuário digite um nome de usuário ou senha. Essa opção normalmente requer que os recursos de delegação estejam habilitados. Se os recursos não estiverem habilitados, você só poderá usar essa opção para acessar uma fonte de dados que esteja localizada no mesmo computador.  
  
### <a name="user-name-and-password-login"></a>Logon de nome de usuário e senha  
 Quando você seleciona **Usar este nome de usuário e senha**, um nome de usuário e senha devem ser fornecidos para acessar a fonte de dados. Para um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , as credenciais talvez sejam de um logon de banco de dados. As credenciais são passadas para a fonte de dados para autenticação.  
  
### <a name="prompted-credentials"></a>Credenciais solicitadas  
 Quando você especifica credenciais solicitadas, cada usuário que acessa o relatório deve digitar um nome de usuário e senha para recuperar os dados. Essa opção é recomendada para relatórios que contêm dados confidenciais. As credenciais solicitadas podem ser para uma conta do Windows ou para um logon de banco de dados. Se o servidor de banco de dados não reconhecer as credenciais fornecidas, ou se o usuário especificado não tiver recebido permissão para recuperar os dados, haverá falha na conexão.  
  
### <a name="no-credentials"></a>Nenhuma credencial  
 Não são necessárias credenciais para esta fonte de dados. Para executar o relatório no servidor de relatório, a conta de execução autônoma deve estar configurada. Para obter mais informações, consulte [Configurar a conta de execução autônoma &#40;SSRS Configuration Manager&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) na [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] documentação do nos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [manuais online](https://go.microsoft.com/fwlink/?linkid=121312)do.  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar, desinstalar e Construtor de Relatórios suporte](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)   
 [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Construtor de Relatórios caixa de diálogo opções, configurações &#40;Construtor de Relatórios&#41;](report-builder/set-default-options-for-report-builder.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Adicionar e verificar uma conexão de dados ou uma fonte de dados &#40;Construtor de Relatórios e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
  
