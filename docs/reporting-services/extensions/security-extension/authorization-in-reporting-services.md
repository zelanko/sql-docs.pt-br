---
title: Autorização no Reporting Services | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- authorization [Reporting Services]
ms.assetid: 15fc1c7b-560c-4737-b126-e0d428a1b530
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2210d5eb5997ec66e707a90cdc52dc24328e6f6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193341"
---
# <a name="authorization-in-reporting-services"></a>Autorização no Reporting Services
  Autorização é o processo de determinar se uma identidade deve receber o tipo de acesso solicitado a um determinado recurso no banco de dados de servidor de relatório. O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa uma arquitetura de autorização baseada em função que concede um acesso de usuário a um determinado recurso com base na atribuição de função do usuário para o aplicativo. As extensões de segurança para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] contêm uma implementação de um componente de autorização usado para conceder acesso a usuários assim que eles se autenticam no servidor de relatório. A autorização é invocada quando um usuário tenta executar uma operação no sistema ou um item de servidor de relatório por meio da API SOAP e via acesso à URL. Isso é possível por meio da interface de extensão de segurança **IAuthorizationExtension2**. Como foi dito anteriormente, todas as extensões herdam de **IExtension** , a interface base para qualquer extensão que você implanta. **IExtension** e **IAuthorizationExtension2** são membros do namespace **Microsoft.ReportingServices.Interfaces**.  
  
## <a name="checking-access"></a>Verificando o acesso  
 Em autorização, a chave para qualquer implementação de segurança personalizada é a verificação de acesso, que é implementada no método <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>. <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> é chamado a cada vez que um usuário tenta uma operação no servidor de relatório. O método <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> é sobrecarregado para cada tipo de operação. Para operações de pasta, um exemplo de uma verificação de acesso poderia ficar assim:  
  
```  
// Overload for Folder operations  
public bool CheckAccess(  
   string userName,   
   IntPtr userToken,   
   byte[] secDesc,   
   FolderOperation requiredOperation)  
{  
   // If the user is the administrator, allow unrestricted access.  
   if (userName == m_adminUserName)   
      return true;  
  
   AceCollection acl = DeserializeAcl(secDesc);  
   foreach(AceStruct ace in acl)  
   {  
         if (userName == ace.PrincipalName)  
         {  
            foreach(FolderOperation aclOperation in   
               ace.FolderOperations)  
            {  
               if (aclOperation == requiredOperation)  
                     return true;  
            }  
         }  
   }  
   return false;  
}  
```  
  
 O servidor de relatório chama o método <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> passando o nome do usuário conectado, um token de usuário, o descritor de segurança para o item e a operação solicitada. Aqui você poderia verificar o descritor de segurança para o nome de usuário e a permissão apropriada para concluir a solicitação, retornar **true** para mostrar que o acesso foi concedido ou **false** para mostrar que o acesso foi negado.  
  
## <a name="security-descriptors"></a>Descritores de segurança  
 Ao definir políticas de autorização em itens do banco de dados do servidor de relatório, um aplicativo cliente (como o Gerenciador de Relatórios) envia as informações do usuário na extensão de segurança junto com a política de segurança do item. Essa política de segurança e as informações do usuário são conhecidas coletivamente como um descritor de segurança. Um descritor de segurança contém as seguintes informações para um item no banco de dados do servidor de relatório:  
  
-   O grupo ou o usuário com algum tipo de permissão para executar operações no item.  
  
-   O tipo do item.  
  
-   Uma lista de controle de acesso discricionário que controla acesso ao item.  
  
 Os descritores de segurança são criados por meio do serviço Web <xref:ReportService2010.ReportingService2010.SetPolicies%2A> e dos métodos <xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A>.  
  
### <a name="authorization-flow"></a>Fluxo de autorização  
 A autorização do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] é controlada pela extensão de segurança configurada para ser executada atualmente no servidor. A autorização é baseada em função e está limitada às permissões e operações fornecidas pela arquitetura de segurança do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . O diagrama a seguir descreve o processo de autorização de usuários a operar em itens no banco de dados do servidor de relatório:  
  
 ![Fluxo de autorização de segurança do Reporting Services](../../../reporting-services/extensions/security-extension/media/rosettasecurityextensionauthorizationflow.gif "Fluxo de autorização de segurança do Reporting Services")  
  
 Como mostrado neste diagrama, a autorização segue esta sequência:  
  
1.  Uma vez autenticados, os aplicativos cliente fazem solicitações ao servidor de relatório por meio dos métodos do serviço Web Servidor de Relatório. Um tíquete de autenticação é passado ao servidor de relatório na forma de um cookie no cabeçalho HTTP de cada solicitação Web.  
  
2.  O cookie é validado antes de qualquer verificação de acesso.  
  
3.  Após a validação do cookie, o servidor de relatório chama <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> e o usuário recebe uma identidade.  
  
4.  O usuário tenta executar uma operação por meio do serviço Web Reporting Services.  
  
5.  O servidor de relatório chama o método <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>.  
  
6.  O descritor de segurança é recuperado e passado a uma implementação de extensão de segurança personalizada de <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>. Neste ponto, o usuário, grupo ou computador é comparado ao descritor de segurança do item acessado e é autorizado a executar a operação solicitada.  
  
7.  Se o usuário for autorizado, o serviço Web executará a operação e devolverá uma resposta ao aplicativo de chamada.  
  
  
