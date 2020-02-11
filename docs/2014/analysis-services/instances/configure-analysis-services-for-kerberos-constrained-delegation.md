---
title: Configurar Analysis Services para delegação restrita de Kerberos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6d751477-6bf1-48b4-8833-5a631bbe7650
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cfceb6b2314f9e57d6d383312d9f9373f7df1621
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67832919"
---
# <a name="configure-analysis-services-for-kerberos-constrained-delegation"></a>Configurar a delegação restrita do Analysis Services para Kerberos)
  Ao configurar o Analysis Services para autenticação Kerberos, você provavelmente está mais interessado em obter um destes resultados ou ambos: fazer com que o Analysis Services represente uma identidade de usuário ao consultar dados ou fazer com que o Analysis Services delegue uma identidade de usuário a um serviço de nível inferior. Cada cenário tem requisitos de configuração ligeiramente diferentes. Nos dois cenários, é necessário que a verificação assegure que a configuração foi feita corretamente.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** é uma ferramenta de diagnóstico que ajuda a solucionar problemas de Kerberos relativos à conectividade com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
 Este tópico contém as seguintes seções:  
  
-   [Permitir que Analysis Services represente uma identidade de usuário](#bkmk_impersonate)  
  
-   [Configurar Analysis Services para delegação confiável](#bkmk_delegate)  
  
-   [Testar a identidade representada ou delegada](#bkmk_test)  
  
> [!NOTE]  
>  A delegação não será necessária se a conexão ao Analysis Services for um único salto, ou se sua solução usar credenciais armazenadas fornecidas pelo Serviço de Repositório Seguro do SharePoint ou pelo Reporting Services. Se todas as conexões forem conexões diretas do Excel para um banco de dados do Analysis Services ou se elas se basearem em credenciais armazenadas, você poderá usar o Kerberos (ou NTLM) sem precisar configurar a delegação restrita.  
>   
>  A delegação restrita de Kerberos será necessária se a identidade do usuário tiver que fluir em várias conexões de computador (conhecido como "salto duplo"). Quando o acesso a dados do Analysis Services for contingente na identidade de usuário, e a solicitação de conexão for proveniente de um serviço de delegação, use a lista de verificação da próxima seção para garantir que o Analysis Services possa representar o chamador original. Para obter mais informações sobre os fluxos de autenticação do Analysis Services, consulte [Autenticação do Microsoft BI e delegação da identidade](https://go.microsoft.com/fwlink/?LinkID=286576).  
>   
>  Como prática de segurança recomendada, a Microsoft sugere sempre a delegação restrita em vez da delegação irrestrita. A delegação irrestrita é um grande risco de segurança, pois permite que a identidade do serviço represente outro usuário em *qualquer* computador, serviço ou aplicativo downstream (em vez de apenas os serviços definidos explicitamente por meio da delegação restrita).  
  
##  <a name="bkmk_impersonate"></a>Permitir que Analysis Services represente uma identidade de usuário  
 Para permitir que os serviços de nível superior, como o Reporting Services, o IIS ou o SharePoint, representem uma identidade de usuário no Analysis Services, você deve configurar a delegação restrita de Kerberos para esses serviços. Nesse cenário, o Analysis Services representa o usuário atual que usa a identidade fornecida pelo serviço de delegação, retornando resultados com base na associação de função dessa identidade de usuário.  
  
|Tarefa|DESCRIÇÃO|  
|----------|-----------------|  
|Etapa 1: verificar se as contas são adequadas para delegação|Verifique se as contas usadas para executar os serviços têm as propriedades corretas no Active Directory. As contas de serviço do Active Directory não devem ser marcadas como contas confidenciais nem serem especificamente excluídas dos cenários de delegação. Para obter mais informações, consulte [Noções básicas sobre contas de usuário](https://go.microsoft.com/fwlink/?LinkId=235818).<br /><br /> ** \* Importante \* \* ** Em geral, todas as contas e os servidores devem pertencer ao mesmo domínio Active Directory ou a domínios confiáveis na mesma floresta. No entanto, como o Windows Server 2012 dá suporte à delegação além dos limites do domínio, você poderá configurar a delegação restrita do Kerberos além do limite de um domínio se o nível funcional do domínio for Windows Server 2012. Outra opção é configurar o Analysis Services para acesso HTTP e usar os métodos de autenticação do IIS na conexão do cliente. Para obter mais informações, consulte [Configurar o acesso HTTP ao Analysis Services no IIS &#40;(Serviços de Informações da Internet)&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md).|  
|Etapa 2: registrar o SPN|Antes de configurar a delegação restrita, você deve registrar um SPN (Nome da Entidade de Serviço) para a instância do Analysis Services. Você precisará do SPN do Analysis Services ao configurar a delegação restrita do Kerberos para serviços de camada intermediária. Consulte [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md) para obter instruções.<br /><br /> Um nome de entidade de serviço (SPN) especifica a identidade exclusiva de um serviço em um domínio configurado para autenticação Kerberos. As conexões de cliente que usam a segurança integrada requerem geralmente um SPN como parte da autenticação SSPI. A solicitação é encaminhada para um controlador de domínio do Active Directory, com o KDC concedendo um tíquete se o SPN apresentado pelo cliente tiver um registro SPN correspondente no Active Directory.|  
|Etapa 3: configurar a delegação restrita|Após a validação das contas que você deseja usar e do registro de SPNs para essas contas, a próxima etapa será configurar os serviços de nível superior, como o IIS, o Reporting Services ou os serviços Web do SharePoint para a delegação restrita, especificando o SPN do Analysis Services como o serviço específico para o qual a delegação é permitida.<br /><br /> Os serviços executados no SharePoint, como os Serviços do Excel ou o Reporting Services no modo do SharePoint, geralmente hospedam pastas de trabalho e relatórios que consomem dados multidimensionais ou de tabela do Analysis Services. Configurar a delegação restrita para esses serviços é uma tarefa de configuração comum, necessária para dar suporte à atualização de dados dos Serviços do Excel. Os links a seguir oferecem instruções para serviços do SharePoint, além de outros serviços que provavelmente apresentem uma solicitação de conexão de dados downstream para dados do Analysis Services:<br /><br /> [Delegação de identidade para os serviços do Excel (SharePoint server 2010)](https://go.microsoft.com/fwlink/?LinkId=299826) ou [como configurar os serviços do Excel no SharePoint Server 2010 para autenticação Kerberos](https://support.microsoft.com/kb/2466519)<br /><br /> [Delegação de identidade para serviços do PerformancePoint (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299827)<br /><br /> [Delegação de identidade para SQL Server Reporting Services (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299828)<br /><br /> Para o IIS 7.0, consulte [Configurar a autenticação do Windows (IIS 7.0)](https://technet.microsoft.com/library/cc754628\(v=ws.10\).aspx) ou [Como configurar o SQL Server 2008 Analysis Services e o SQL Server 2005 Analysis Services para usar a autenticação Kerberos](https://support.microsoft.com/kb/917409).|  
|Etapa 4: testar conexões|Ao testar, conecte-se de computadores remotos, em identidades diferentes, e consulte o Analysis Services usando os mesmos aplicativos que usuários empresariais. Você pode usar o SQL Server Profiler para monitorar a conexão. Você verá a identidade do usuário na solicitação. Para obter mais informações, consulte [Testar a identidade representada ou delegada](#bkmk_test) nesta seção.|  
  
##  <a name="bkmk_delegate"></a>Configurar Analysis Services para delegação confiável  
 A configuração do Analysis Services para delegação restrita de Kerberos permite que o serviço represente uma identidade de cliente em um serviço de nível inferior, como o mecanismo de banco de dados relacional, de modo que os dados possam ser consultados como se o cliente tivesse sido conectado diretamente.  
  
 Os cenários de delegação do Analysis Services limitam-se a modelos de tabela configurados para o modo `DirectQuery`. Esse é o único cenário em que o Analysis Services pode transmitir credenciais delegadas para outro serviço. Em todos os outros cenários, como os cenários do SharePoint mencionados na seção anterior, o Analysis Services está na extremidade de recebimento da cadeia de delegação. Para obter mais informações sobre o DirectQuery, consulte [Modo DirectQuery &#40;SSAS de Tabela&#41;](../tabular-models/directquery-mode-ssas-tabular.md).  
  
> [!NOTE]  
>  Um equívoco comum é o de que o armazenamento ROLAP, operações de processamento ou o acesso a partições remotas de alguma forma cria requisitos para a delegação restrita. Esse não é o caso. Todas essas operações são executadas diretamente pela conta de serviço (também conhecida como a conta de processamento), em seu próprio nome. A delegação não é obrigatória para essas operações no Analysis Services, pois as permissões para elas são concedidas diretamente para a conta de serviço (por exemplo, concedendo permissões db_datareader no banco de dados relacional para que o serviço possa processar os dados). Para obter mais informações sobre operações do servidor e permissões, consulte [Configurar contas de serviço &#40;Analysis Services&#41;](configure-service-accounts-analysis-services.md).  
  
 Esta seção explica como configurar o Analysis Services para delegação confiável. Ao concluir essa tarefa, o Analysis Services poderá passar credenciais delegadas para o SQL Server, em suporte ao modo DirectQuery usado em soluções de tabelas.  
  
 Antes de começar:  
  
-   Verifique se o Analysis Services foi iniciado.  
  
-   Verifique se o SPN registrado para o Analysis Services é válido. Para obter instruções, consulte [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md).  
  
 Quando esse dois pré-requisitos forem atendidos, continue com as etapas a seguir. Observe que você deve ser um administrador de domínio para configurar a delegação restrita.  
  
1.  Em Usuários e Computadores de Active Directory, localize a conta de serviço na qual o Analysis Services é executado. Clique com o botão direito do mouse na conta de serviço e escolha **Propriedades**.  
  
     Para fins ilustrativos, as seguintes captura de tela usam OlapSvc e SQLSvc para representar o Analysis Services e o SQL Server, respectivamente.  
  
     OlapSvc é a conta que será configurada para a delegação restrita ao SQLSvc. Quando você concluir essa tarefa, o OlapSvc terá permissão para passar credenciais delegadas em um tíquete de serviço para o SQLSvc, representando o chamador original ao solicitar dados.  
  
2.  Na guia delegação, selecione **Confiar neste usuário para delegação apenas aos serviços especificados**, seguido por **Usar apenas Kerberos**. Clique em **Adicionar** para especificar qual serviço do Analysis Services tem permissão para delegar credenciais.  
  
     A guia delegação só aparece quando a conta de usuário (OlapSvc) é atribuída a um serviço (Analysis Services) e o serviço tem um SPN registrado para ele. O registro de SPN requer que o serviço esteja em execução.  
  
     ![SSAS_Kerberos_1_AccountProperties](../media/ssas-kerberos-1-accountproperties.gif "SSAS_Kerberos_1_AccountProperties")  
  
3.  Na página Adicionar Serviços, clique em **Usuários ou Computadores**.  
  
     ![SSAS_Kerberos_2_](../media/ssas-kerberos-2.gif "SSAS_Kerberos_2_")  
  
4.  Na página Selecionar Usuários ou Computador, insira a conta usada para executar a instância do SQL Server que fornece dados aos bancos de dados modelo de tabela do Analysis Services. Clique em **OK** para aceitar a conta de serviço.  
  
     Se você não puder selecionar a conta desejada, verifique se o SQL Server está em execução e tem um SPN registrado para essa conta. Para obter mais informações sobre os SPNs do mecanismo de banco de dados, consulte [Register a Service Principal Name for Kerberos Connections](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
     ![SSAS_Kerberos_3_SelectUsers](../media/ssas-kerberos-3-selectusers.gif "SSAS_Kerberos_3_SelectUsers")  
  
5.  Agora, a instância do SQL Server deve aparecer em Adicionar Serviços. Qualquer serviço que também esteja usando essa conta também aparecerá na lista. Escolha a instância do SQL Server que você deseja usar. Clique em **OK** para aceitar a instância.  
  
     ![SSAS_Kerberos_4_](../media/ssas-kerberos-4.gif "SSAS_Kerberos_4_")  
  
6.  Agora, a página de propriedades da conta de serviço do Analysis Services deve ser semelhante à captura de tela a seguir. Clique em **OK** para salvar suas alterações.  
  
     ![SSAS_Kerberos_5_Finished](../media/ssas-kerberos-5-finished.gif "SSAS_Kerberos_5_Finished")  
  
7.  Verifique se a delegação foi feita com êxito conectando-se a partir de um computador cliente remoto, em uma identidade diferente, e consulte o modelo de tabela. Você verá a identidade do usuário na solicitação no SQL Server Profiler.  
  
##  <a name="bkmk_test"></a>Testar a identidade representada ou delegada  
 Use o SQL Server Profiler para monitorar a identidade do usuário que está consultando dados.  
  
1.  Inicie o **SQL Server Profiler** na instância do Analysis Services e, em seguida, inicie um novo rastreamento.  
  
2.  Em Seleção de Eventos, verifique se `Audit Login` e `Audit Logout` foram verificados na seção Auditoria de Segurança.  
  
3.  Conecte-se ao Analysis Services por meio de um serviço de aplicativo (como o SharePoint ou o Reporting Services) em um computador cliente remoto. O evento Logon da Auditoria mostrará a identidade do usuário que está se conectando ao Analysis Services.  
  
 Os testes completos requerem o uso de ferramentas de monitoramento de rede que podem capturar solicitações e respostas de Kerberos na rede. O utilitário Monitor de Rede (netmon.exe), filtrado para Kerberos, pode ser usado nessa tarefa. Para obter mais informações sobre como usar o Netmon 3.4 e outras ferramentas para testar a autenticação do Kerberos, consulte [Como configurar a autenticação Kerberos: configuração principal (SharePoint Server 2010)](https://technet.microsoft.com/library/gg502602\(v=office.14\).aspx).  
  
 Além disso, consulte [A caixa de diálogo mais confusa no Active Directory](https://www.itprotoday.com/active-directory/most-confusing-dialog-box-active-directory) para obter uma descrição completa de cada opção na guia Delegação da caixa de diálogo de propriedades do objeto do Active Directory. Este artigo também explica como usar o LDP para testar e interpretar os resultados dos testes.  
  
## <a name="see-also"></a>Consulte Também  
 [Autenticação do Microsoft BI e delegação de identidade](https://go.microsoft.com/fwlink/?LinkID=286576)   
 [Autenticação mútua usando Kerberos](https://go.microsoft.com/fwlink/?LinkId=299283)   
 [Conectar-se ao Analysis Services](connect-to-analysis-services.md)   
 [Registro de SPN para uma instância de Analysis Services](spn-registration-for-an-analysis-services-instance.md)   
 [Propriedades da cadeia de conexão &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)  
  
  
