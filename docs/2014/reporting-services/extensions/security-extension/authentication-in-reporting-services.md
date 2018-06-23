---
title: Autenticação no Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], authentication
- forms-based authentication [Reporting Services]
- authentication [Reporting Services]
- custom authentication [Reporting Services]
ms.assetid: 103ce1f9-31d8-44bb-b540-2752e4dcf60b
caps.latest.revision: 23
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: df847dc70d13d61a43b6ba3554280cece774b49a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019530"
---
# <a name="authentication-in-reporting-services"></a>Autenticação no Reporting Services
  A autenticação é o processo de estabelecimento do direito de um usuário a uma identidade. Existem muitas técnicas que você pode usar para autenticar um usuário. O modo mais comum é usar senhas. Quando você implementa a Autenticação de Formulários, por exemplo, deseja uma implementação que solicite credenciais dos usuários (normalmente por meio de alguma interface que solicita um nome de login e uma senha) e depois valide os usuários em um repositório de dados, como uma tabela de banco de dados ou um arquivo de configuração. Se as credenciais não puderem ser validadas, o processo de autenticação falhará e o usuário assumirá uma identidade anônima.  
  
## <a name="custom-authentication-in-reporting-services"></a>Autenticação personalizada no Reporting Services  
 No [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], o sistema operacional Windows lida com a autenticação de usuários por meio da segurança integrada ou da recepção explícita e da validação de credenciais de usuário. A autenticação personalizada pode ser desenvolvida no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para dar suporte a esquemas de autenticação adicionais. Isso é possível por meio da interface de extensão de segurança <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension>. Todas as extensões herdam da interface base <xref:Microsoft.ReportingServices.Interfaces.IExtension> para qualquer extensão implantada e usada pelo servidor de relatório. <xref:Microsoft.ReportingServices.Interfaces.IExtension>, além de <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension>, são membros do namespace <xref:Microsoft.ReportingServices.Interfaces>.  
  
 A principal forma de autenticar em um servidor de relatório no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] é o método <xref:ReportService2010.ReportingService2010.LogonUser%2A>. Esse membro do serviço Web Reporting Services pode ser usado para passar credenciais de usuário a um servidor de relatório para validação. Seu subjacente implementa de extensão de segurança **Iauthenticationextension** que contém o código de autenticação personalizado. Na amostra da Autenticação de Formulários, **LogonUser**, que executa uma verificação de autenticação nas credenciais fornecidas e em um repositório de usuários personalizado de um banco de dados. Um exemplo de implementação de **LogonUser** é semelhante a esta:  
  
```  
public bool LogonUser(string userName, string password, string authority)  
{  
   return AuthenticationUtilities.VerifyPassword(userName, password);  
}  
  
```  
  
 A função de exemplo a seguir é usada para verificar as credenciais fornecidas:  
  
```  
  
internal static bool VerifyPassword(string suppliedUserName,  
   string suppliedPassword)  
{   
   bool passwordMatch = false;  
   // Get the salt and pwd from the database based on the user name.  
   // See "How To: Use DPAPI (Machine Store) from ASP.NET," "How To:  
   // Use DPAPI (User Store) from Enterprise Services," and "How To:  
   // Create a DPAPI Library" for more information about how to use  
   // DPAPI to securely store connection strings.  
   SqlConnection conn = new SqlConnection(  
      "Server=localhost;" +   
      "Integrated Security=SSPI;" +  
      "database=UserAccounts");  
   SqlCommand cmd = new SqlCommand("LookupUser", conn);  
   cmd.CommandType = CommandType.StoredProcedure;  
  
   SqlParameter sqlParam = cmd.Parameters.Add("@userName",  
       SqlDbType.VarChar,  
       255);  
   sqlParam.Value = suppliedUserName;  
   try  
   {  
      conn.Open();  
      SqlDataReader reader = cmd.ExecuteReader();  
      reader.Read(); // Advance to the one and only row  
      // Return output parameters from returned data stream  
      string dbPasswordHash = reader.GetString(0);  
      string salt = reader.GetString(1);  
      reader.Close();  
      // Now take the salt and the password entered by the user  
      // and concatenate them together.  
      string passwordAndSalt = String.Concat(suppliedPassword, salt);  
      // Now hash them  
      string hashedPasswordAndSalt =  
         FormsAuthentication.HashPasswordForStoringInConfigFile(  
         passwordAndSalt,  
         "SHA1");  
      // Now verify them. Returns true if they are equal.  
      passwordMatch = hashedPasswordAndSalt.Equals(dbPasswordHash);  
   }  
   catch (Exception ex)  
   {  
       throw new Exception("Exception verifying password. " +  
          ex.Message);  
   }  
   finally  
   {  
       conn.Close();  
   }  
   return passwordMatch;  
}  
```  
  
## <a name="authentication-flow"></a>Fluxo de autenticação  
 O serviço Web Reporting Services oferece extensões de autenticação personalizadas para habilitar a Autenticação de Formulários feita pelo Gerenciador de Relatórios e pelo servidor de relatório.  
  
 O método <xref:ReportService2010.ReportingService2010.LogonUser%2A> do serviço Web Reporting Services é usado para enviar credenciais ao servidor de relatório para autenticação. O serviço Web usa cabeçalhos HTTP para passar um tíquete de autenticação (conhecido como "cookie") do servidor para o cliente para solicitações de logon validadas.  
  
 A ilustração a seguir mostra o método de autenticação de usuários no serviço Web quando o seu aplicativo é implantado com um servidor de relatório configurado para usar uma extensão de autenticação personalizada.  
  
 ![Fluxo de autenticação de segurança do Reporting Services](../../media/rosettasecurityextensionauthenticationflow.gif "Fluxo de autenticação de segurança do Reporting Services")  
  
 Como mostrado na Figura 2, o processo de autenticação é assim:  
  
1.  Um aplicativo cliente chama o método do serviço Web <xref:ReportService2010.ReportingService2010.LogonUser%2A> para autenticar um usuário.  
  
2.  O serviço Web faz uma chamada para o <xref:ReportService2010.ReportingService2010.LogonUser%2A> método de sua extensão de segurança, especificamente, a classe que implementa **IAuthenticationExtension**.  
  
3.  A sua implementação de <xref:ReportService2010.ReportingService2010.LogonUser%2A> valida o nome de usuário e a senha no repositório de usuários ou na autoridade de segurança.  
  
4.  Após a autenticação bem-sucedida, o serviço Web criará um cookie e o gerenciará para a sessão.  
  
5.  O serviço Web devolve o tíquete de autenticação ao aplicativo de chamada no cabeçalho HTTP.  
  
 Quando o serviço Web autenticar um usuário com êxito por meio da extensão de segurança, vai gerar um cookie que será usado para as solicitações subsequentes. O cookie pode não persistir dentro da autoridade de segurança personalizada porque o servidor de relatório não possui a autoridade de segurança. O cookie é retornado a partir do método <xref:ReportService2010.ReportingService2010.LogonUser%2A> do serviço Web e é usado em chamadas subsequentes do método do serviço Web e no acesso à URL.  
  
> [!NOTE]  
>  Para impedir o comprometimento do cookie durante a transmissão, os cookies de autenticação retornados de <xref:ReportService2010.ReportingService2010.LogonUser%2A> devem ser transmitidos de forma segura usando criptografia SSL.  
  
 Se você acessar o servidor de relatório por meio do acesso à URL quando uma extensão de segurança personalizada for instalada, o IIS (Serviços de Informações da Internet) e o [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] gerenciarão automaticamente a transmissão do tíquete de autenticação. Se você estiver acessando o servidor de relatório por meio da API SOAP, a sua implementação da classe proxy deverá incluir suporte adicional para o gerenciamento do tíquete de autenticação. Para obter mais informações sobre como usar a API SOAP e gerenciar o tíquete de autenticação, consulte "Usando o serviço Web com segurança personalizada".  
  
## <a name="forms-authentication"></a>Autenticação de Formulários  
 A Autenticação de Formulários é um tipo de autenticação do [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] na qual um usuário não autenticado é direcionado a um formulário HTML. Quando o usuário fornece credenciais, o sistema emite um cookie com um tíquete de autenticação. Em solicitações posteriores, o sistema verifica o cookie primeiro para ver se o usuário já foi autenticado pelo servidor de relatório.  
  
 O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] pode ser estendido para dar suporte à Autenticação de Formulários que usa as interfaces de extensibilidade de segurança disponíveis por meio da API do Reporting Services. Se você estender o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para usar a Autenticação de Formulários, use o protocolo SSL (Secure Sockets Layer) para todas as comunicações feitas com o servidor de relatório para impedir que usuários maliciosos obtenham acesso ao cookie de outro usuário. O SSL permite que clientes e que um servidor de relatório autentiquem uns aos outros e garantam que nenhum outro computador poderá ler o conteúdo das comunicações entre os dois computadores. Todos os dados enviados de um cliente por meio de uma conexão SSL são criptografados para que os usuários maliciosos não possam interceptar senhas ou dados enviados para um servidor de relatório.  
  
 A Autenticação de Formulário é geralmente implementada para dar suporte a contas e à autenticação para plataformas diferentes do Windows. Uma interface gráfica é apresentada a um usuário que solicite acesso a um servidor de relatório e as credenciais fornecidas serão enviadas a uma autoridade de segurança para autenticação.  
  
 A Autenticação de Formulários exige que uma pessoa esteja presente para inserir as credenciais. Para aplicativos autônomos que se comunicam diretamente com o serviço Web Reporting Services, a Autenticação de Formulários deve ser combinada a um esquema de autenticação personalizado.  
  
 A Autenticação de Formulários é apropriada para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] quando:  
  
-   Você precisa armazenar e autenticar usuários que não têm contas do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] o Windows e  
  
-   Você precisa fornecer o seu próprio formulário de interface do usuário como página de logon entre páginas diferentes de um site.  
  
 Considere o seguinte ao escrever uma extensão de segurança personalizada que dê suporte à Autenticação de Formulários:  
  
-   Se você usar a Autenticação de Formulários, o acesso anônimo deverá ser habilitado no diretório virtual de servidor de relatório no IIS (Serviços de Informações da Internet).  
  
-   A autenticação do [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] deve ser definida como Formulários. Você configura autenticação do [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] no arquivo Web.config para o servidor de relatório.  
  
-   O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] pode autenticar e autorizar usuários com a Autenticação do Windows ou a autenticação personalizada, mas não com ambas. O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] não dá suporte ao uso simultâneo de várias extensões de segurança.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de segurança](../security-extension/implementing-a-security-extension.md)  
  
  