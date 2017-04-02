---
title: "Registrar um SPN (Nome da Entidade de Servi&#231;o) para um servidor de relat&#243;rio | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dda91d4f-77cc-4898-ad03-810ece5f8e74
caps.latest.revision: 7
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 7
---
# Registrar um SPN (Nome da Entidade de Servi&#231;o) para um servidor de relat&#243;rio
  Se estiver implantando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em uma rede que use o protocolo Kerberos para autenticação mútua, você deverá criar um SPN (Nome da Entidade de Serviço) para o serviço Servidor de Relatório se configurá-lo para execução como uma conta de usuário do domínio.  
  
## Sobre SPNs  
 Um SPN é um identificador exclusivo para um serviço em uma rede que usa autenticação Kerberos. Consiste em uma classe de serviço, um nome de host e uma porta. Em uma rede que usa autenticação Kerberos, deve ser registrado um SPN para o servidor em uma conta interna do computador (como NetworkService ou LocalSystem) ou uma conta de usuário. Os SPNs são automaticamente registrados para contas internas. Entretanto, quando executar um serviço em uma conta de usuário do domínio, você deverá registrar manualmente o SPN para a conta que deseja usar.  
  
 Para criar um SPN, você pode usar o utilitário de linha de comando **SetSPN**. Para obter mais informações, consulte o seguinte:  
  
-   [Setspn](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx) (http://technet.microsoft.com/library/cc731241(WS.10).aspx).  
  
-   [SPNs (Nomes da Entidade de Serviço) e Sintaxe SetSPN(Setspn.exe)](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).  
  
 Você deve ser um administrador de domínio para executar o utilitário no controlador de domínio.  
  
## Sintaxe  
 A sintaxe de comando para usar o utilitário SetSPN e criar um SPN para o servidor de relatório se assemelha ao seguinte:  
  
```  
Setspn -s http/<computername>.<domainname>:<port> <domain-user-account>  
```  
  
 **SetSPN** está disponível no Windows Server. O argumento de **-s** adiciona um SPN depois de não validar nenhuma duplicata. **OBSERVAÇÃO: -s** está disponível no Windows Server a partir do Windows Server 2008.  
  
 **HTTP** é a classe de serviço. O serviço Web Servidor de Relatórios é executado em HTTP.SYS. Uma criação por produto de um SPN para HTTP significa que todos os aplicativos Web no mesmo computador que são executados em HTTP.SYS (incluindo aplicativos hospedados no IIS) receberão tíquetes com base na conta de usuário do domínio. Se esses serviços forem executados em uma conta diferente, ocorrerá falha nas solicitações de autenticação. Para evitar esse problema, configure todos os aplicativos HTTP para que sejam executados na mesma conta ou considere a criação de cabeçalhos de host para cada aplicativo e, depois, a criação de SPNs separados para cada cabeçalho de host. Quando você configura cabeçalhos de host, é necessário fazer alterações de DNS, independentemente da configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Os valores especificados para \<*nomedocomputador*>, \<*nomededomínio*> e \<*porta*> identificam o endereço de rede exclusivo do computador que hospeda o servidor de relatório. Pode ser um nome de host local ou um nome de domínio totalmente qualificado (FQDN). Se você tiver somente um domínio e estiver usando a porta 80, poderá omitir \<*nomededomínio*> e \<*porta*> de sua linha de comando. \<*conta-do-usuário-do-domínio*> é a conta de usuário sob a qual o serviço Servidor de Relatório executa e na qual o SPN deve ser registrado.  
  
## Registrar um SPN para a conta de usuário do domínio  
  
#### Para registrar um SPN para um serviço Servidor de Relatório que esteja em execução como um usuário do domínio  
  
1.  Instale o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e configure o serviço Servidor de Relatório para ser executado como uma conta de usuário do domínio. Observe que os usuários não poderão se conectar ao servidor de relatório até que você conclua as etapas a seguir.  
  
2.  Faça logon no controlador de domínio como administrador de domínio.  
  
3.  Abra uma janela do prompt de comando.  
  
4.  Copie o seguinte comando, substituindo os valores de espaço reservado por valores reais que sejam válidos para sua rede:  
  
    ```  
    Setspn -s http/<computer-name>.<domain-name>:<port> <domain-user-account>  
    ```  
  
     Por exemplo: `Setspn -s http/MyReportServer.MyDomain.com:80 MyDomainUser`  
  
5.  Execute o comando.  
  
6.  Abra o arquivo **RsReportServer.config** e localize a seção `<AuthenticationTypes>`.  
  
7.  Adicione `<RSWindowsNegotiate/>` como a primeira entrada desta seção para habilitar NTLM.  
  
## Consulte também  
 [Configurar uma conta de serviço &#40;SSRS Configuration Manager&#41;](../Topic/Configure%20a%20Service%20Account%20\(SSRS%20Configuration%20Manager\).md)   
 [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Gerenciar um servidor de relatórios de modo nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  