---
title: Personificação e Credenciais para Conexões | Microsoft Docs
description: Na integração SQL Server CLR, você pode querer se passar pelo chamador na Autenticação do Windows usando a propriedade SqlContext.WindowsIdentity.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 382185c036055bb9ea689f551c256a26ee83b0b4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81485124"
---
# <a name="impersonation-and-credentials-for-connections"></a>Representação e credenciais para conexões
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Na integração CLR (Common Language Runtime) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o uso da Autenticação do Windows é complexo, porém é mais seguro do que o uso da Autenticação do SQL Server. Quando usar a Autenticação do Windows, lembre-se das considerações a seguir.  
  
 Por padrão, um processo do SQL Server que se conecta ao Windows adquire o contexto de segurança da conta de serviço do Windows para SQL Server. Todavia, é possível mapear uma função CLR para uma identidade proxy, de modo que suas conexões de saída tenham um contexto de segurança diferente daquele da conta de serviço do Windows.  
  
 Em alguns casos, você pode querer se passar pelo chamador usando a propriedade **SqlContext.WindowsIdentity** em vez de ser executado como conta de serviço. A instância **WindowsIdentity** representa a identidade do cliente que invocou o código de chamada e só está disponível quando o cliente usou a Autenticação do Windows. Depois de obter a instância **Do WindowsIdentity,** você pode chamar **Impersonate** para alterar o token de segurança do segmento e, em seguida, abrir ADO.NET conexões em nome do cliente.  
  
 Depois de chamar SQLContext.WindowsIdentity.Impersonate, você não pode acessar dados locais e não pode acessar dados do sistema. Para acessar os dados novamente, você tem que chamar o WindowsImpersonationContext.Undo.  
  
 O exemplo a seguir mostra como se passar pelo chamador usando a propriedade **SqlContext.WindowsIdentity.**  
  
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
>  Para obter informações sobre mudanças de comportamento na personificação, consulte [Quebrando alterações nos recursos do mecanismo de banco de dados no SQL Server 2016](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
 Além disso, se você obteve a instância de identidade do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows, por padrão não poderá propagar essa instância para outro computador; a infraestrutura de segurança do Windows impõe essa restrição por padrão. Porém, há um mecanismo chamado "delegação" que permite a propagação de identidades do Windows por vários computadores. Você pode aprender mais sobre a delegação no artigo da TechNet, "[Kerberos Protocol Transition and Constrained Delegation](https://go.microsoft.com/fwlink/?LinkId=50419)".  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto SqlContext](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
