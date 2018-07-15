---
title: Representação e credenciais para conexões | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- authentication [CLR integration]
- user impersonation [CLR integration]
- credentials [CLR integration]
- database objects [CLR integration], security
ms.assetid: 293dce7d-1db2-4657-992f-8c583d6e9ebb
caps.latest.revision: 31
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9af64be53b702dfded163a06562e4f6bdf7e5a61
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350868"
---
# <a name="impersonation-and-credentials-for-connections"></a>Representação e credenciais para conexões
  Na integração CLR (Common Language Runtime) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o uso da Autenticação do Windows é complexo, porém é mais seguro do que o uso da Autenticação do SQL Server. Quando usar a Autenticação do Windows, lembre-se das considerações a seguir.  
  
 Por padrão, um processo do SQL Server que se conecta ao Windows adquire o contexto de segurança da conta de serviço do Windows para SQL Server. Todavia, é possível mapear uma função CLR para uma identidade proxy, de modo que suas conexões de saída tenham um contexto de segurança diferente daquele da conta de serviço do Windows.  
  
 Em alguns casos, talvez você queira representar o chamador usando a propriedade `SqlContext.WindowsIdentity` em vez de executar como a conta de serviço. A instância de `WindowsIdentity` representa a identidade do cliente que invocou o código de chamada e só estará disponível se o cliente usou a Autenticação do Windows. Depois de obter a instância de `WindowsIdentity`, você poderá chamar `Impersonate` para alterar o token de segurança do thread e, em seguida, abrir as conexões ADO.NET em nome do cliente.  
  
 Depois de chamar SQLContext.WindowsIdentity.Impersonate, você não pode acessar dados locais e você não pode acessar dados do sistema. Para acessar os dados novamente, você precisa chamar WindowsImpersonationContext.Undo.  
  
 O exemplo a seguir mostra como representar o chamador por meio da propriedade `SqlContext.WindowsIdentity`.  
  
 Visual C#  
  
```  
WindowsIdentity clientId = null;  
WindowsImpersonationContext impersonatedUser = null;  
  
clientId = SqlContext.WindowsIdentity;  
  
// This outer try block is used to protect from   
// exception filter attacks which would prevent  
// the inner finally block from executing and   
// resetting the impersonation.  
try  
{  
   try  
   {  
      impersonatedUser = clientId.Impersonate();  
      if (impersonatedUser != null)  
         return GetFileDetails(directoryPath);  
         else return null;  
   }  
   finally  
   {  
      if (impersonatedUser != null)  
         impersonatedUser.Undo();  
   }  
}  
catch  
{  
   throw;  
}  
```  
  
> [!NOTE]  
>  Para obter informações sobre alterações de comportamento na representação, consulte [alterações recentes em recursos do mecanismo de banco de dados no SQL Server 2014](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
 Além disso, se você obteve a instância de identidade do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows, por padrão não poderá propagar essa instância para outro computador; a infraestrutura de segurança do Windows impõe essa restrição por padrão. Porém, há um mecanismo chamado "delegação" que permite a propagação de identidades do Windows por vários computadores. Você pode aprender mais sobre delegação no artigo da TechNet, "[transição do protocolo Kerberos e delegação restrita](http://go.microsoft.com/fwlink/?LinkId=50419)".  
  
## <a name="see-also"></a>Consulte também  
 [Objeto SqlContext](../../clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
