---
title: Bibliotecas de .NET Framework com suporte | Microsoft Docs
description: Com o CLR hospedado no SQL Server, você pode criar usando bibliotecas de classe de .NET Framework com suporte e bibliotecas sem suporte que você registra com um banco de dados.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
author: rothja
ms.author: jroth
ms.openlocfilehash: 610dcca5103e4a819b0e6c59629ddd4d510f5469
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756352"
---
# <a name="supported-net-framework-libraries"></a>Bibliotecas do .NET Framework compatíveis
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Com o CLR (common language runtime) hospedado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você pode criar procedimentos armazenados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidas pelo usuário em código gerenciado. Com a funcionalidade contida nas bibliotecas de classe do .NET Framework, você tem acesso a classes pré-criadas que fornecem recursos de manipulação de cadeia de caracteres, operações matemáticas avançadas, acesso a arquivos, criptografia, e mais. Essas classes podem ser acessadas de qualquer procedimento armazenado gerenciado, tipo definido pelo usuário, gatilho, função definida pelo usuário ou agregação definida pelo usuário.  
  
> [!NOTE]  
>  Se você reparar ou atualizar assemblies sem suporte no GAC (cache de assembly global), seu aplicativo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possivelmente deixará de funcionar. Isso ocorre porque o reparo ou a atualização de bibliotecas no GAC não atualiza esses assemblies dentro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se um assembly existir tanto em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como no GAC, as duas cópias do assembly deverão ser exatamente iguais. Caso isso não aconteça, ocorrerá um erro quando o assembly for usado pela integração CLR do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se você atender ou atualizar qualquer assembly no GAC que também esteja registrado no banco de dados, incluindo assemblies de .NET Framework sem suporte, certifique-se de também atender ou atualizar a cópia do assembly dentro de seus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bancos de dados com a instrução **ALTER assembly** . Para obter mais informações, consulte o [artigo 949080 da base de dados de conhecimento](https://support.microsoft.com/kb/949080).  
  
## <a name="supported-libraries"></a>Bibliotecas com suporte  
 A partir do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem uma lista de bibliotecas suportadas do .NET Framework, que foram testadas para garantir o atendimento aos padrões de confiabilidade e segurança para interação com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. As bibliotecas suportadas não precisam ser explicitamente registradas no servidor para que possam ser usadas no seu código; [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] as carrega diretamente do GAC (Cache de Assembly Global).  
  
 As bibliotecas/namespaces suportados pela integração CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são:  
  
-   CustomMarshalers  
-   Microsoft.VisualBasic  
-   Microsoft.VisualC  
-   mscorlib  
-   Sistema  
-   System.Configuration  
-   System.Core  
-   System.Data  
-   System.Data.OracleClient  
-   System.Data.SqlXml  
-   System.Deployment  
-   System.Security  
-   System.Transactions  
-   System.Web.Services  
-   System.Xml  
-   System.Xml.Linq  

<!--
Any modifications to the list above should be duplicated on the following page:
https://docs.microsoft.com/sql/relational-databases/clr-integration/assemblies-designing#supported-net-framework-assemblies
-->

## <a name="unsupported-libraries"></a>Bibliotecas sem-suporte  
 As bibliotecas sem-suporte ainda podem ser chamadas de seus procedimentos armazenados gerenciados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidos pelo usuário. A biblioteca sem suporte deve primeiro ser registrada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados, usando a instrução **Create assembly** , antes que possa ser usada em seu código. Qualquer biblioteca sem-suporte que é registrada e executada no servidor deveria ser examinada e testada para fins de segurança e confiabilidade.  
  
 Por exemplo, não há suporte para o namespace **System. DirectoryServices** . Você deve registrar o assembly System.DirectoryServices.dll com permissões **não seguras** antes de poder chamá-lo do seu código. A permissão **não segura** é necessária porque as classes no namespace **System. DirectoryServices** não atendem aos requisitos de **segurança** ou **EXTERNAL_ACCESS**. Para obter mais informações, consulte [restrições de modelo de programação de integração CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) e segurança de acesso a código de [integração CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Segurança de acesso ao código de integração CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restrições do modelo de programação da Integração CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
