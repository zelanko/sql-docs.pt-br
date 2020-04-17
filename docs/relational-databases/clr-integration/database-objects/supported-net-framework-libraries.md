---
title: Bibliotecas-quadro .NET suportadas | Microsoft Docs
description: Com o CLR hospedado no SQL Server, você pode criar o autor usando bibliotecas de classe .NET Framework suportadas e bibliotecas não suportadas que você registra em um banco de dados.
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
ms.openlocfilehash: 459cd091043d567b4c93555c271213d066f3989e
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487095"
---
# <a name="supported-net-framework-libraries"></a>Bibliotecas do .NET Framework compatíveis
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Com o CLR (common language runtime) hospedado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você pode criar procedimentos armazenados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidas pelo usuário em código gerenciado. Com a funcionalidade contida nas bibliotecas de classe do .NET Framework, você tem acesso a classes pré-criadas que fornecem recursos de manipulação de cadeia de caracteres, operações matemáticas avançadas, acesso a arquivos, criptografia, e mais. Essas classes podem ser acessadas de qualquer procedimento armazenado gerenciado, tipo definido pelo usuário, gatilho, função definida pelo usuário ou agregação definida pelo usuário.  
  
> [!NOTE]  
>  Se você reparar ou atualizar assemblies sem suporte no GAC (cache de assembly global), seu aplicativo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possivelmente deixará de funcionar. Isso ocorre porque o reparo ou a atualização de bibliotecas no GAC não atualiza esses assemblies dentro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se um assembly existir tanto em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como no GAC, as duas cópias do assembly deverão ser exatamente iguais. Caso isso não aconteça, ocorrerá um erro quando o assembly for usado pela integração CLR do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se você atender ou atualizar quaisquer conjuntos no GAC que também estejam registrados no banco de dados, incluindo conjuntos .NET [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Framework não suportados, certifique-se de também fazer o serviço ou atualizar a cópia do conjunto dentro de seus bancos de dados com a declaração **ALTER ASSEMBLY.** Para obter mais informações, consulte [o artigo 949080](https://support.microsoft.com/kb/949080)da Base de Conhecimento .  
  
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
 As bibliotecas sem-suporte ainda podem ser chamadas de seus procedimentos armazenados gerenciados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidos pelo usuário. A biblioteca sem suporte deve primeiro [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ser registrada no banco de dados, usando a declaração **CREATE ASSEMBLY,** antes de poder ser usada em seu código. Qualquer biblioteca sem-suporte que é registrada e executada no servidor deveria ser examinada e testada para fins de segurança e confiabilidade.  
  
 Por exemplo, o **namespace System.DirectoryServices** não é suportado. Você deve registrar o conjunto System.DirectoryServices.dll com permissões **INSEGURAS** antes de poder chamá-lo do seu código. A permissão **INSEGURA** é necessária porque as classes no **namespace System.DirectoryServices** não atendem aos requisitos **de SAFE** ou **EXTERNAL_ACCESS**. Para obter mais informações, consulte [as restrições do modelo de programação de integração da CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) e a [segurança de acesso ao código de integração da CLR.](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Criando uma Assembléia](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Segurança de acesso ao código de integração clr](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restrições do modelo de programação da Integração CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
