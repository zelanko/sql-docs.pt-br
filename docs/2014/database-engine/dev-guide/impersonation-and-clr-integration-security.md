---
title: Representação e segurança da integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- execution context [CLR integration]
- user impersonation [CLR integration]
- context [CLR integration]
ms.assetid: 1495a7af-2248-4cee-afdb-9269fb3a7774
caps.latest.revision: 17
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 05b117f27d0c27ca9288f94aade079df876fafad
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243196"
---
# <a name="impersonation-and-clr-integration-security"></a>Representação e segurança de integração CLR
  Quando código gerenciado acessa recursos externos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não representa automaticamente o contexto de execução atual no qual a rotina está em execução. O código nos assemblies `EXTERNAL_ACCESS` e `UNSAFE` pode representar explicitamente o contexto de execução atual.  
  
> [!NOTE]  
>  Para obter informações sobre alterações de comportamento na representação, consulte [alterações recentes em recursos do mecanismo de banco de dados no SQL Server 2014](../breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
 O provedor de acesso a dados em processo oferece uma interface de programação de aplicativo, `SqlContext.WindowsIdentity`, que pode ser usada para recuperar o token associado ao contexto de segurança atual. O código gerenciado nos assemblies `EXTERNAL_ACCESS` e `UNSAFE` pode usar esse método para recuperar o contexto e usar o método `WindowsIdentity.Impersonate` do .NET Framework para representar esse contexto. As restrições seguintes se aplicam quando o código do usuário é representado explicitamente:  
  
-   O acesso a dados em processo não é permitido quando o código gerenciado está em um estado representado. O código pode desfazer a representação e chamar o acesso a dados em processo. Observe que isso exige o armazenamento do valor de retorno (um objeto`WindowsImpersonationContext`) do método original `Impersonate` e chamada do método `Undo` em `WindowsImpersonationContext`.  
  
     Essa restrição significa que, quando ocorre o acesso a dados em processo, ele é sempre no contexto do contexto de segurança atual em vigor da sessão. Ele não pode ser modificado por meio da representação explícita no código gerenciado.  
  
-   No código gerenciado em execução assíncrona (por exemplo, por meio de assemblies `UNSAFE` que criam threads e que executam códigos de maneira assíncrona), o acesso a dados em processo jamais é permitido. Isso é verdadeiro, independentemente de haver ou não representação.  
  
 Quando o código está em execução em um contexto sem representação diferente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele não pode realizar chamadas de acesso a dados em processo; ele deve desfazer o contexto de representação antes de fazer as chamadas. Quando o acesso a dados em processo é feito no código gerenciado, o contexto de execução original do ponto de entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] no código gerenciado é sempre usado na autorização.  
  
 Os assemblies `EXTERNAL_ACCESS` e `UNSAFE` acessam recursos do sistema operacional usando a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a menos que representem de maneira voluntária o contexto de segurança atual conforme a descrição. Por conta disso, os autores dos assemblies `EXTERNAL_ACCESS` exigem um nível de confiança mais elevado do que os de assemblies `SAFE`, especificado pela permissão em nível de logon `EXTERNAL ACCESS`. Apenas logons confiáveis para a execução de códigos na conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem receber a permissão `EXTERNAL ACCESS`.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança da integração CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Representação e credenciais para conexões](../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
  
  
