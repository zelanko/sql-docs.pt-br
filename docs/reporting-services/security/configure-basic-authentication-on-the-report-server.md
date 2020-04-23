---
title: Configurar a autenticação Básica no servidor de relatório | Microsoft Docs
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- Basic authentication
ms.assetid: 8faf2938-b71b-4e61-a172-46da2209ff55
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 18b08fdca61a423353f53406432791d758818ea0
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81625865"
---
# <a name="configure-basic-authentication-on-the-report-server"></a>Configurar autenticação básica no Servidor de Relatório
  Por padrão, o Reporting Services aceita solicitações que especificam a autenticação Negotiate e NTLM. Se a sua implantação inclui aplicativos cliente ou navegadores que usam autenticação Básica, adicione a autenticação Básica à lista de tipos suportados. Além disso, para usar o Construtor de Relatórios, você deve habilitar o acesso Anônimo aos arquivos do Construtor de Relatórios.  
  
 Para configurar a autenticação Básica no servidor de relatório, edite os elementos XML e os valores no arquivo RSReportServer.config. É possível copiar e colar os exemplos deste tópico para substituir os valores padrão.  
  
 Antes de habilitar a autenticação Básica, verifique se a sua infraestrutura de segurança dá suporte a ela. Na autenticação Básica, o serviço Web Servidor de Relatórios passará credenciais para a autoridade de segurança local. Se as credenciais especificarem uma conta de usuário local, o usuário será autenticado pela autoridade de segurança local no computador do servidor de relatório e o usuário obterá um token de segurança válido para recursos locais. As credenciais de contas de usuário de domínio são encaminhadas para um controlador de domínio e autenticadas por ele. A permissão resultante é válida para recursos de rede.  
  
 A criptografia de canal, como o protocolo TSL, anteriormente conhecido como protocolo SSL, será necessária se você quiser minimizar o risco de interceptação das credenciais durante o envio para um controlador de domínio da sua rede. Por si só, autenticação Básica transmite o nome do usuário em texto não criptografado e a senha na codificação em base 64. Quando adicionada, a criptografia de canal torna o pacote ilegível. Para obter mais informações, confira [Configurar conexões TLS em um servidor de relatório no modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).  
  
 Depois de habilitar a autenticação Básica, lembre-se que os usuários não podem selecionar a opção **Segurança integrada do Windows** ao definir as propriedades de conexão para uma fonte de dados externa que forneça dados a um relatório. A opção ficará indisponível nas páginas de propriedades da fonte de dados.  
  
> [!NOTE]  
>  As instruções a seguir são válidas para um servidor de relatório no modo nativo. Se o servidor de relatório for implantado no modo integrado do SharePoint, use as configurações de autenticação padrão que especificam a segurança integrada do Windows. O servidor de relatório usa recursos internos da extensão padrão da Autenticação do Windows para dar suporte ao servidor de relatório no modo integrado do SharePoint.  
  
### <a name="to-configure-a-report-server-to-use-basic-authentication"></a>Para configurar um servidor de relatório para usar a autenticação Básica  
  
1.  Abra o RSReportServer.config em um editor de texto.  
  
     O arquivo está localizado em *\<drive>:* \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer.  
  
2.  Localize \<**Authentication**>.  
  
3.  Copie uma das estruturas XML a seguir que seja mais adequada para as suas necessidades. A primeira estrutura XML oferece espaços reservados para especificar todos os elementos, que estão descritos na próxima seção:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsBasic>  
                       <LogonMethod>3</LogonMethod>  
                       <Realm></Realm>  
                       <DefaultDomain></DefaultDomain>  
                 </RSWindowsBasic>  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     Se você estiver usando valores padrão, poderá copiar a estrutura de elementos mínima:  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsBasic/>  
          </AuthenticationTypes>  
    ```  
  
4.  Cole-a nas entradas existentes de \<**Authentication**>.  
  
     Se você estiver usando vários tipos de autenticação, adicione apenas o elemento **RSWindowsBasic** , mas não exclua as entradas para **RSWindowsNegotiate**, **RSWindowsNTLM**ou **RSWindowsKerberos**.  
  
     Observe que não é possível usar **Personalizada** com outros tipos de autenticação.  
  
5.  Substitua os valores vazios de \<**Realm**> ou \<**DefaultDomain**> por valores válidos para seu ambiente.  
  
6.  Salve o arquivo.  
  
7.  Se você configurou uma implantação em expansão, repita essas etapas para outros servidores de relatório na implantação.  
  
8.  Reinicie o servidor de relatório para terminar as sessões que estão atualmente abertas.  
  
## <a name="rswindowsbasic-reference"></a>Referência de RSWindowsBasic  
 Os elementos a seguir podem ser especificados na configuração da autenticação Básica.  
  
|Elemento|Obrigatório|Valores válidos|  
|-------------|--------------|------------------|  
|LogonMethod|Sim<br /><br /> Se você não especificar um valor, será usado 3.|**2** = Logon de rede, indicado para servidores de alto desempenho na autenticação de senhas em texto sem formatação.<br /><br /> **3** = Logon de texto não criptografado, que preserva as credenciais de logon no pacote de autenticação enviado com cada solicitação HTTP, permitindo que o servidor represente o usuário durante a conexão com outros servidores da rede. (Padrão)<br /><br /> Observação: Valores 0 (para logon interativo) e 1 (para logon em lotes) **NÃO** têm suporte no [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|  
|Realm|Opcional|Especifica uma partição de recursos que inclui recursos de autorização e autenticação usados para controlar o acesso a recursos protegidos da organização.|  
|DefaultDomain|Opcional|Especifica o domínio usado pelo servidor para autenticar o usuário. Este valor é opcional, mas, caso seja omitido, o servidor de relatório usará o nome do computador como domínio. Se o computador for um membro de domínio, esse domínio será o padrão. Se você instalou o servidor de relatório em um controlador de domínio, o domínio usado será o que é controlado pelo computador.|  
  
## <a name="see-also"></a>Consulte Também  
 [Domínios do aplicativo para aplicativos do Servidor de Relatório](../../reporting-services/report-server/application-domains-for-report-server-applications.md)   
 [Segurança e proteção do Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md)  
  
  
