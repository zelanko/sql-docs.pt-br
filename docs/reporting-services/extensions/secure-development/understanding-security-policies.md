---
title: Noções básicas sobre políticas de segurança | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
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
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6649017002fb3dd5df2dc3ee68a0d759ded24887
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "63193393"
---
# <a name="understanding-security-policies"></a>Compreendendo políticas de segurança
  Qualquer código executado por um servidor de relatório deve fazer parte de uma política de segurança de acesso a códigos específica. Essas políticas de segurança consistem em grupos de códigos que mapeiam evidência para um conjunto de conjuntos de permissões nomeados. Frequentemente, os grupos de códigos estão associados a um conjunto de permissões nomeado que especifica permissões permitidas para código nesse grupo. O runtime usa a evidência fornecida por um host confiável ou pelo carregador para determinar a quais grupos de códigos o código pertence e, portanto, quais permissões conceder ao código. O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] segue esta arquitetura de política de segurança, conforme definido pelo CLR (Common Language Runtime) do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. As seções a seguir descrevem os vários tipos de código em [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e a as regras de política associadas a eles.  
  
## <a name="report-server-assemblies"></a>Assemblies do Servidor de Relatório  
 Os assemblies do servidor de relatório são os que contêm código que faz parte do produto [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] é escrito com o uso de assemblies de código gerenciado. Todos esses assemblies têm nome forte (isto é, são assinados digitalmente). Os grupos de códigos desses assemblies são definidos com a **StrongNameMembershipCondition**, que fornece evidência com base nas informações de chave pública do nome forte do assembly. O grupo de códigos recebe o conjunto de permissões **FullTrust**.  
  
## <a name="report-server-extensions-rendering-data-delivery-and-security"></a>Extensões do servidor de relatório (renderização, dados, entrega e segurança)  
 As extensões do servidor de relatório são extensões de dados personalizados, entrega, renderização e segurança, criadas por você ou terceiros para ampliar a funcionalidade do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Você deve conceder **FullTrust** a essas extensões ou ao código de assembly nos arquivos de configuração de política associados ao componente do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] estendido. As extensões fornecidas como parte do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] são assinadas com a chave pública do servidor de relatório e recebem o conjunto de permissões **FullTrust**.  
  
> [!IMPORTANT]  
>  Você deve modificar os arquivos de configuração de política do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para permitir **FullTrust** a qualquer extensão de terceiros. Se você não adicionar um grupo de códigos com **FullTrust** às extensões personalizadas, elas não poderão ser usadas pelo servidor de relatório.  
  
 Para obter mais informações sobre os arquivos de configuração de política no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], consulte [Usando os arquivos de política de segurança do Reporting Services](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).  
  
## <a name="expressions-used-in-reports"></a>Expressões usadas em relatórios  
 As expressões de relatório são expressões de código embutidas ou métodos definidos pelo usuário dentro do elemento **Code** de um arquivo de linguagem de definição de relatório. Há um grupo de códigos já configurado nos arquivos de política que concede a essas expressões a permissão **Execução** definida por padrão. O grupo de códigos se parece com o seguinte:  
  
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
  
 A permissão **Execução** permite que o código seja executado, mas não use recursos protegidos. Todas as expressões localizadas em um relatório são compiladas em um assembly (chamado de assembly de “hosts de expressão”) armazenado como parte de um relatório compilado. Quando o relatório é executado, o servidor de relatório carrega o assembly de hosts de expressão e faz chamadas nesse assembly para executar expressões. Os assemblies de hosts de expressão são assinados com uma chave específica usada para definir o grupo de códigos para todos os hosts de expressão.  
  
 As expressões de relatório fazem referência a coleções de modelo de objeto de relatório (campos, parâmetros etc.) e executam tarefas simples como operações aritméticas e de cadeia de caracteres. O código que executa essas operações simples só exige a permissão **Execução**. Por padrão, os métodos definidos pelo usuário no elemento **Code** e qualquer assembly personalizado recebem a permissão **Execução** no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Assim, para a maioria das expressões, a configuração atual não requer a modificação de nenhum arquivo de política de segurança. Para conceder permissões adicionais a assemblies de hosts de expressão, um administrador precisa modificar os arquivos de configuração de política do servidor de relatório e Designer de Relatórios, além de alterar o grupo de códigos de expressões do relatório. Como essa é uma configuração global, alterar permissões padrão para os hosts de expressão afeta todos os relatórios. Por esse motivo, é altamente recomendado que você coloque todo código que solicite segurança adicional em um assembly personalizado. Apenas a esse assembly serão concedidas as permissões necessárias.  
  
> [!IMPORTANT]  
>  O código que chama os assemblies externos ou recursos protegidos deve ser incorporado a um assembly personalizado para uso em relatórios. Ao fazer isso, você ganhará mais controle sobre as permissões solicitadas e declaradas por seu código. Você não deve fazer chamadas a métodos seguros no elemento **Code**. Fazer isso exige a concessão de **FullTrust** aos hosts de expressão de relatório e a concessão do acesso completo a todo o código personalizado ao CLR.  
  
> [!CAUTION]  
>  Não conceda **FullTrust** ao grupo de códigos para um host de expressão de relatório. Se fizer isso, você permitirá que todas as expressões de relatório façam chamadas do sistema protegidas.  
  
## <a name="custom-assemblies-referenced-in-reports"></a>Assemblies personalizados referenciados em relatórios  
 Algumas expressões de relatório podem chamar assemblies de código de terceiros, também conhecidos no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] como assemblies personalizados. O servidor de relatório espera que esses assemblies tenham, pelo menos, a permissão **Execução** nos arquivos de configuração de política. Por padrão, os arquivos de política fornecidos com o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] concedem a permissão **Execução** a todos os assemblies iniciados na zona “Meu Computador”. Você pode conceder permissões adicionais a assemblies personalizados conforme necessário.  
  
 Em alguns casos, pode ser necessário executar uma operação que exija permissões de código específicas em uma expressão de relatório. Geralmente isso significa que uma expressão de relatório precisa fazer uma chamada a um método de biblioteca CLR protegido (como um que acessa arquivos ou o Registro do sistema). A documentação do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] descreve as permissões de código necessárias para tornar essa chamada segura; para executar a chamada, o código de chamada deve receber essas permissões seguras específicas. Se você fizer a chamada em uma expressão de relatório ou no elemento **Code**, o assembly de host de expressão deverá receber as permissões apropriadas. Entretanto, após conceder as permissões aos hosts de expressão, todos os códigos executados em qualquer expressão em qualquer relatório receberão essa permissão específica. É muito mais seguro fazer a chamada de um assembly personalizado e conceder a ele as permissões específicas.  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de acesso do código no Reporting Services](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)   
 [Desenvolvimento seguro &#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
