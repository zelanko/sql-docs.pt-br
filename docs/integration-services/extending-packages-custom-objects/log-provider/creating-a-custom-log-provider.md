---
description: Criando um provedor de log personalizado
title: Criar um provedor de logs personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom log providers [Integration Services], creating
ms.assetid: fc20af96-9eb8-4195-8d3f-8a4d7c753f24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d12ea8d1c1289ef917c5781980af4f09eacfdf18
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123102"
---
# <a name="creating-a-custom-log-provider"></a>Criando um provedor de log personalizado

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  O ambiente de tempo de execução do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tem extensas capacidades de log. Um log permite capturar eventos que ocorrem durante a execução de pacotes. O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui vários provedores de log que permitem a criação e o armazenamento de logs em vários formatos, como XML, texto, banco de dados ou no log de eventos do Windows. Se um desses provedores ou formatos de saída não forem adequados às suas necessidades, você pode criar um provedor de log personalizado.  
  
 As etapas envolvidas na criação de um provedor de log personalizado são semelhantes às etapas de criação de qualquer outro objeto personalizado para o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Crie uma classe nova herdada da classe base. Para um provedor de log, a classe base é <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>.  
  
-   Aplique o atributo que identifica o tipo de objeto para a classe. Para um provedor de log, o atributo é <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>.  
  
-   Substitua a implementação dos métodos e propriedades da classe base. Para um provedor de log, eles incluem a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> e os métodos <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>.  
  
-   As interfaces do usuário personalizadas para provedores de log personalizados não são implementadas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
## <a name="getting-started-with-a-custom-log-provider"></a>Guia de Introdução com um provedor de log personalizado  
  
### <a name="creating-projects-and-classes"></a>Criando projetos e classes  
 Como todos os provedores de log gerenciados derivam da classe base <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>, o primeiro passo para criar um provedor de log personalizado é criar um projeto de biblioteca de classes na linguagem de programação gerenciada de sua preferência e criar uma classe herdada da classe base. Nessa classe derivada, você substituirá os métodos e propriedades da classe base para implementar sua funcionalidade personalizada.  
  
 Configure o projeto para assinar o assembly que será gerado com um arquivo de chave de nome forte.  
  
> [!NOTE]  
>  Muitos provedores de log do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] têm uma interface do usuário personalizada que implementa o <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> e substitui a caixa de texto **Configuração** na caixa de diálogo **Configurar Logs de SSIS** por uma lista suspensa filtrada com gerenciadores de conexões disponíveis. Porém, interfaces do usuário personalizadas para provedores de log personalizados não são implementadas no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
### <a name="applying-the-dtslogprovider-attribute"></a>Aplicando o atributo DtsLogProvider  
 Aplique o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> à classe que você criou para identificá-lo como um provedor de log. Esse atributo fornece informações de tempo de design, como o nome e a descrição do provedor de log. As propriedades **DisplayName** e **Description** do atributo correspondem às colunas **Nome** e **Descrição** exibidas no editor **Configurar Logs do SSIS**, exibidas durante a configuração de registro em log para um pacote no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
> [!IMPORTANT]  
>  A propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.LogProviderType%2A> do atributo não é usada. Porém, você deve digitar um valor para ela ou o provedor de log personalizado não aparecerá na lista de provedores de log disponíveis.  
  
> [!NOTE]  
>  Como as interfaces do usuário personalizadas para provedores de log personalizados não são implementadas no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], especificar um valor para a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> não tem nenhum efeito.  
  
```vb  
<DtsLogProvider(DisplayName:="MyLogProvider", Description:="A simple log provider.", LogProviderType:="Custom")> _  
Public Class MyLogProvider  
     Inherits LogProviderBase  
    ' TODO: Override the base class methods.  
End Class  
```  
  
```csharp  
[DtsLogProvider(DisplayName="MyLogProvider", Description="A simple log provider.", LogProviderType="Custom")]  
public class MyLogProvider : LogProviderBase  
{  
    // TODO: Override the base class methods.  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-log-provider"></a>Compilando, implantando e depurando um provedor de log personalizado  
 As etapas para compilar, implantar e depurar um provedor de log personalizado no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] são muito semelhantes às etapas necessárias para outros tipos de objetos personalizados. Para obter mais informações, consulte [Compilar, implantar e depurar objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Codificar um provedor de logs personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)   
 [Desenvolver uma interface do usuário para um provedor de logs personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-user-interface-for-a-custom-log-provider.md)  
  
  
