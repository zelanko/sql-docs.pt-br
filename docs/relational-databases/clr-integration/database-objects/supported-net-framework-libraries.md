---
title: Suporte para bibliotecas do .NET Framework | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9b970822a872a03fa3f2ba3044d2e8432ac595e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="supported-net-framework-libraries"></a>Bibliotecas do .NET Framework compatíveis
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Com o CLR (common language runtime) hospedado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você pode criar procedimentos armazenados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidas pelo usuário em código gerenciado. Com a funcionalidade contida nas bibliotecas de classe do .NET Framework, você tem acesso a classes pré-criadas que fornecem recursos de manipulação de cadeia de caracteres, operações matemáticas avançadas, acesso a arquivos, criptografia, e mais. Essas classes podem ser acessadas de qualquer procedimento armazenado gerenciado, tipo definido pelo usuário, gatilho, função definida pelo usuário ou agregação definida pelo usuário.  
  
> [!NOTE]  
>  Se você reparar ou atualizar assemblies sem suporte no GAC (cache de assembly global), seu aplicativo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possivelmente deixará de funcionar. Isso ocorre porque o reparo ou a atualização de bibliotecas no GAC não atualiza esses assemblies dentro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se um assembly existir tanto em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como no GAC, as duas cópias do assembly deverão ser exatamente iguais. Caso isso não aconteça, ocorrerá um erro quando o assembly for usado pela integração CLR do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se você reparar ou atualizar todos os assemblies no GAC que também são registrados no banco de dados, incluindo os assemblies do .NET Framework não suportados, certifique-se também reparou ou atualizou a cópia do assembly dentro de sua [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bancos de dados com o  **ALTER ASSEMBLY** instrução. Para obter mais informações, consulte [artigo 949080 da Base de dados de Conhecimento](http://support.microsoft.com/kb/949080).  
  
## <a name="supported-libraries"></a>Bibliotecas com suporte  
 A partir do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem uma lista de bibliotecas suportadas do .NET Framework, que foram testadas para garantir o atendimento aos padrões de confiabilidade e segurança para interação com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. As bibliotecas suportadas não precisam ser explicitamente registradas no servidor para que possam ser usadas no seu código; [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] as carrega diretamente do GAC (Cache de Assembly Global).  
  
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
 As bibliotecas sem-suporte ainda podem ser chamadas de seus procedimentos armazenados gerenciados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidos pelo usuário. A biblioteca de suporte deve ser registrada primeiro no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados usando o **CREATE ASSEMBLY** instrução, antes de ser usada em seu código. Qualquer biblioteca sem-suporte que é registrada e executada no servidor deveria ser examinada e testada para fins de segurança e confiabilidade.  
  
 Por exemplo, o **System. DirectoryServices** não há suporte para o namespace. Você deve registrar o assembly System.DirectoryServices.dll com **UNSAFE** permissões antes de chamar do seu código. O **UNSAFE** permissão é necessária porque classes de **System. DirectoryServices** namespace não atende aos requisitos para **seguro** ou  **EXTERNAL_ACCESS**. Para obter mais informações, consulte [restrições do modelo de programação de integração de CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) e [segurança de acesso do código de integração de CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criando um Assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Segurança de acesso do código de integração de CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restrições do modelo de programação da integração CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
