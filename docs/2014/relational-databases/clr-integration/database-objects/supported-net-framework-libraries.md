---
title: Suporte para bibliotecas do .NET Framework | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8c50e18862d2c3ca5b5e900c6eccebe6e921ea94
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37351028"
---
# <a name="supported-net-framework-libraries"></a>Bibliotecas do .NET Framework compatíveis
  Com o CLR (common language runtime) hospedado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você pode criar procedimentos armazenados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidas pelo usuário em código gerenciado. Com a funcionalidade contida nas bibliotecas de classe do .NET Framework, você tem acesso a classes pré-criadas que fornecem recursos de manipulação de cadeia de caracteres, operações matemáticas avançadas, acesso a arquivos, criptografia, e mais. Essas classes podem ser acessadas de qualquer procedimento armazenado gerenciado, tipo definido pelo usuário, gatilho, função definida pelo usuário ou agregação definida pelo usuário.  
  
> [!NOTE]  
>  Se você reparar ou atualizar assemblies sem suporte no cache de assembly global (GAC), seu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se um assembly existir tanto em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] integração CLR. Se você reparar ou atualizar qualquer assembly no GAC que também está registrado no banco de dados, incluindo os assemblies do .NET Framework sem suporte, verifique se também reparou ou atualizou a cópia do assembly nos bancos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com a instrução `ALTER ASSEMBLY`. Para obter mais informações, consulte [artigo 949080 da Base de dados de Conhecimento](http://support.microsoft.com/kb/949080).  
  
## <a name="supported-libraries"></a>Bibliotecas com suporte  
 Começando com [!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)] tem uma lista de bibliotecas do .NET Framework com suporte, que foram testados para garantir que eles atendam aos padrões de confiabilidade e segurança para interação com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] carrega-os diretamente do Global Assembly Cache (GAC).  
  
 As bibliotecas/namespaces suportados pela integração CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são:  
  
-   CustomMarshalers  
  
-   Microsoft.VisualBasic  
  
-   Microsoft.VisualC  
  
-   mscorlib  
  
-   Sistema  
  
-   System.Configuration  
  
-   System.Data  
  
-   System.Data.OracleClient  
  
-   System.Data.SqlXml  
  
-   System.Deployment  
  
-   System.Security  
  
-   System.Transactions  
  
-   System.Web.Services  
  
-   System.Xml  
  
-   System.Core.dll  
  
-   System.Xml.Linq.dll  
  
## <a name="unsupported-libraries"></a>Bibliotecas sem-suporte  
 As bibliotecas sem-suporte ainda podem ser chamadas de seus procedimentos armazenados gerenciados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidos pelo usuário. A biblioteca sem-suporte deve ser registrada primeiro no banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], usando a instrução `CREATE ASSEMBLY`, antes de poder ser usada no seu código. Qualquer biblioteca sem-suporte que é registrada e executada no servidor deveria ser examinada e testada para fins de segurança e confiabilidade.  
  
 Por exemplo, o namespace `System.DirectoryServices` não é suportado. Você deve registrar o assembly System.DirectoryServices.dll com permissões `UNSAFE` antes de poder chamá-lo do seu código. A permissão `UNSAFE` é necessária porque classes no namespace `System.DirectoryServices` não satisfazem aos requisitos para `SAFE` ou `EXTERNAL_ACCESS`. Para obter mais informações, consulte [restrições do modelo de programação de integração de CLR](clr-integration-programming-model-restrictions.md) e [segurança de acesso do código de integração de CLR](../security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criando um Assembly](../assemblies/creating-an-assembly.md)   
 [Segurança de acesso do código de integração de CLR](../security/clr-integration-code-access-security.md)   
 [Restrições do modelo de programação da integração CLR](clr-integration-programming-model-restrictions.md)  
  
  
