---
title: "Noções básicas sobre as políticas de segurança | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- code groups [Reporting Services]
- code access security [Reporting Services], security policies
- Execution permission set
- custom assemblies [Reporting Services], security
- permission sets [Reporting Services]
- expressions [Reporting Services], security
- evidence [Reporting Services]
- FullTrust permission set
- security policies [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: a9bf043a-139a-4929-9a58-244815323df0
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 4c8fa977e2b9cdd596e3029be4954daea7fe239d
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="understanding-security-policies"></a>Compreendendo políticas de segurança 
  Qualquer código executado por um servidor de relatório deve fazer parte de uma política de segurança de acesso a códigos específica. Essas políticas de segurança consistem em grupos de códigos que mapeiam evidência para um conjunto de conjuntos de permissões nomeados. Frequentemente, os grupos de códigos estão associados a um conjunto de permissões nomeado que especifica permissões permitidas para código nesse grupo. O tempo de execução usa a evidência fornecida por um host confiável ou pelo carregador para determinar a quais grupos de códigos o código pertence e, portanto, quais permissões conceder ao código. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]segue esta arquitetura de política de segurança conforme definido pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] common language runtime (CLR). As seções a seguir descrevem os vários tipos de código em [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e a as regras de política associadas a eles.  
  
## <a name="report-server-assemblies"></a>Assemblies do Servidor de Relatório  
 Os assemblies do servidor de relatório são os que contêm código que faz parte do produto [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] é escrito com o uso de assemblies de código gerenciado. Todos esses assemblies têm nome forte (isto é, são assinados digitalmente). Os grupos de códigos para esses assemblies são definidos usando o **StrongNameMembershipCondition**, que fornece evidência com base nas informações de chave pública de nome forte do assembly. O grupo de códigos é concedido a **FullTrust** conjunto de permissões.  
  
## <a name="report-server-extensions-rendering-data-delivery-and-security"></a>Extensões do servidor de relatório (renderização, dados, entrega e segurança)  
 As extensões do servidor de relatório são extensões de dados personalizados, entrega, renderização e segurança, criadas por você ou terceiros para ampliar a funcionalidade do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Você deve conceder **FullTrust** para essas extensões ou código de assembly nos arquivos de configuração de política associado a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] componente que você estiver estendendo. As extensões enviadas como parte do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] são assinados com a chave pública do servidor de relatório e receber o **FullTrust** conjunto de permissões.  
  
> [!IMPORTANT]  
>  Você deve modificar o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] arquivos de configuração de política para permitir **FullTrust** para qualquer extensão de terceiros. Se você não adicionar um grupo de códigos com **FullTrust** para suas extensões personalizadas, eles não podem ser usados pelo servidor de relatório.  
  
 Para obter mais informações sobre os arquivos de configuração de política no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], consulte [usando o Reporting Services Security Policy Files](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).  
  
## <a name="expressions-used-in-reports"></a>Expressões usadas em relatórios  
 Expressões de relatório são expressões de código embutido ou métodos definidos pelo usuário contidos o **código** elemento de um arquivo de linguagem de definição de relatório. Há um grupo de códigos já configurado nos arquivos de política que concede a essas expressões a **execução** permissão definida por padrão. O grupo de códigos se parece com o seguinte:  
  
```  
<CodeGroup  
   class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="Execution"  
   Name="Report_Expressions_Default_Permissions"  
   Description="This code group grants default permissions for code in report expressions and Code element. ">  
    <IMembershipCondition  
       class="StrongNameMembershipCondition"  
       version="1"  
       PublicKeyBlob="002400..."  
    />  
</CodeGroup>  
```  
  
 **Execução** permissão permite que o código execute (Executar), mas não para usar recursos protegidos. Todas as expressões localizadas em um relatório são compiladas em um assembly (chamado de assembly de “hosts de expressão”) armazenado como parte de um relatório compilado. Quando o relatório é executado, o servidor de relatório carrega o assembly de hosts de expressão e faz chamadas nesse assembly para executar expressões. Os assemblies de hosts de expressão são assinados com uma chave específica usada para definir o grupo de códigos para todos os hosts de expressão.  
  
 As expressões de relatório fazem referência a coleções de modelo de objeto de relatório (campos, parâmetros etc.) e executam tarefas simples como operações aritméticas e de cadeia de caracteres. Código que executa essas operações simples só requer **execução** permissão. Por padrão, os métodos definidos pelo usuário a **código** elemento e todos os assemblies personalizados recebem **execução** permissão no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Assim, para a maioria das expressões, a configuração atual não requer a modificação de nenhum arquivo de política de segurança. Para conceder permissões adicionais a assemblies de hosts de expressão, um administrador precisa modificar os arquivos de configuração de política do servidor de relatório e Designer de Relatórios, além de alterar o grupo de códigos de expressões do relatório. Como essa é uma configuração global, alterar permissões padrão para os hosts de expressão afeta todos os relatórios. Por esse motivo, é altamente recomendado que você coloque todo código que solicite segurança adicional em um assembly personalizado. Apenas a esse assembly serão concedidas as permissões necessárias.  
  
> [!IMPORTANT]  
>  O código que chama os assemblies externos ou recursos protegidos deve ser incorporado a um assembly personalizado para uso em relatórios. Ao fazer isso, você ganhará mais controle sobre as permissões solicitadas e declaradas por seu código. Você não deve fazer chamadas a métodos seguros no **código** elemento. Isso requer que você conceda **FullTrust** para o host de expressão de relatório e concede todas as personalizado acesso completo ao código do CLR.  
  
> [!CAUTION]  
>  Não conceda **FullTrust** ao grupo de códigos para um host de expressão do relatório. Se fizer isso, você permitirá que todas as expressões de relatório façam chamadas do sistema protegidas.  
  
## <a name="custom-assemblies-referenced-in-reports"></a>Assemblies personalizados referenciados em relatórios  
 Algumas expressões de relatório podem chamar assemblies de código de terceiros, também conhecidos no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] como assemblies personalizados. O servidor de relatório espera esses assemblies para ter pelo menos **execução** permissão nos arquivos de configuração de política. Por padrão, arquivos de política enviados com [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] conceder **execução** permissão para todos os assemblies começando da zona 'Meu computador'. Você pode conceder permissões adicionais a assemblies personalizados conforme necessário.  
  
 Em alguns casos, pode ser necessário executar uma operação que exija permissões de código específicas em uma expressão de relatório. Geralmente isso significa que uma expressão de relatório precisa fazer uma chamada a um método de biblioteca CLR protegido (como um que acessa arquivos ou o Registro do sistema). A documentação do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] descreve as permissões de código necessárias para tornar essa chamada segura; para executar a chamada, o código de chamada deve receber essas permissões seguras específicas. Se você fizer a chamada de uma expressão de relatório ou o **código** elemento, o assembly de host de expressão deve ter as permissões apropriadas. Entretanto, após conceder as permissões aos hosts de expressão, todos os códigos executados em qualquer expressão em qualquer relatório receberão essa permissão específica. É muito mais seguro fazer a chamada de um assembly personalizado e conceder a ele as permissões específicas.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança de acesso do código no Reporting Services](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)   
 [Proteger o desenvolvimento de &#40; Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
