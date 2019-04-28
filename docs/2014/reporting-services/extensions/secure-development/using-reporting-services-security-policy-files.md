---
title: Usando arquivos de política de segurança do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- code groups [Reporting Services]
- CodeGroup elements
- configuration files [Reporting Services]
- code access security [Reporting Services], security policies
- security policies [Reporting Services]
- security configuration files [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: 2280fff6-3de7-44b1-87da-5db0ec975928
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ee7ba55e48f4704c912e92a4d8352e7c891c06b6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62989682"
---
# <a name="using-reporting-services-security-policy-files"></a>Usando arquivos de política de segurança do Reporting Services
  O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] armazena informações de política de segurança de componentes em três arquivos de configuração que são copiados no sistema de arquivos durante a instalação. Estes arquivos de configuração podem conter uma combinação de políticas de segurança de uso interno e definidas pelo usuário assemblies de código no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Três arquivos de configuração correspondem aos três componentes de segurança do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]: O servidor de relatório e o serviço Windows, o aplicativo Web do Gerenciador de relatórios e o Designer de relatórios a janela de visualização.  
  
> [!NOTE]  
>  Há dois modos de visualização do Designer de Relatórios: a guia Visualizar e a janela pop-up Visualizar, que é iniciada quando o Projeto de Relatório é inicializado no modo **DebugLocal**. A guia **Visualizar** não é um componente protegível e não aplica as configurações de política de segurança. A janela de exibição foi desenvolvida para simular a funcionalidade do servidor de relatório e, portanto, tem um arquivo de configuração de política que você ou um administrador devem modificar para usar assemblies e extensões personalizadas no Designer de Relatórios.  
  
 Os arquivos de configuração de política de segurança contêm informações sobre a classe de segurança, alguns conjuntos nomeados padrão de permissões e os grupos de código para os assemblies do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Os arquivos de configuração de política do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] são similares ao arquivo Security.config que determina a hierarquia de grupos de código e os conjuntos de permissões associados às políticas do nível corporativo e de máquina do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. O local deste arquivo é C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\CONFIG\security.config.  
  
## <a name="policy-files-in-reporting-services"></a>Arquivos de política do Reporting Services  
 A tabela a seguir lista os arquivos de configuração de política do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], sua localização (supondo uma instalação padrão) e suas respectivas funções.  
  
|Nome do arquivo|Local (instalação padrão)|Descrição|  
|---------------|---------------------------------------|-----------------|  
|rssrvpolicy.config|C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer|O arquivo de configuração de política de servidor de relatório. Estas políticas de segurança afetam principalmente expressões de relatório e assemblies personalizados após um relatório ser implantado em um servidor de relatório. Este arquivo de política também afeta dados personalizados, extensões de entrega, renderização e segurança implantados no servidor de relatório.|  
|rsmgrpolicy.config|C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportManager|Arquivo de configuração de política do Gerenciador de Relatórios. Estas políticas de segurança afetam todos os assemblies que estendem o Gerenciador de Relatórios; por exemplo, extensões de interface de usuário de assinatura para entrega personalizada.|  
|rspreviewpolicy.config|C:\Arquivos de Programas\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies|Arquivo de configuração de política de visualização autônoma do Designer de Relatórios. Estas políticas de segurança afetam assemblies personalizados e expressões de relatório que são usados em relatórios durante a visualização e o desenvolvimento. Estas políticas também afetam extensões personalizadas, como extensões de processamento de dados, que são implantadas no Designer de Relatórios.|  
  
## <a name="modifying-configuration-files"></a>Modificando arquivos de configuração  
 As configurações são especificadas como elementos ou atributos XML. Se você entender de XML e arquivos de configuração, use um editor de texto ou de código para modificar configurações definidas pelo usuário. Os arquivos de configuração de segurança contêm informações sobre a hierarquia de grupos de código e os conjuntos de permissões associados a um nível de política do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. É recomendado usar o utilitário de configuração do .NET Framework (Mscorcfg.msc) ou o utilitário de política de segurança de acesso ao código (Caspol.exe) para modificar políticas de segurança no arquivo Security.config primeiro, de modo que as alterações de política correspondam a elementos válidos de configuração XML para arquivos de política. Feito isso, você pode recortar e colar os novos grupos de código e conjuntos de permissões do Security.config para o arquivo de política do componente ao qual estão sendo adicionadas permissões de código.  
  
> [!IMPORTANT]  
>  Você deve fazer backup dos arquivos de configuração de política antes de fazer alterações.  
  
 O uso desse método tem duas vantagens. Primeiro, permite usar uma ferramenta visual para criar grupos de código e conjuntos de permissões para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Isto é muito mais fácil do que gravar elementos de configuração XML a partir do zero. Em segundo lugar, esse método assegura que os arquivos de configuração de política de segurança não sejam corrompidos com elementos e atributos XML malformados. Para obter mais informações sobre o utilitário de política de Segurança de Acesso do Código, consulte Usando arquivos de política de segurança do Reporting Services no MSDN.  
  
 Antes de modificar arquivos de configuração de política, leia todas as informações disponíveis nesta seção e os tópicos relacionados. A modificação da configuração de política do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] pode afetar significativamente a segurança no que diz respeito a como os componentes do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] executam módulos de código externos.  
  
## <a name="placement-of-codegroup-elements-for-extensions"></a>Colocação de elementos CodeGroup para extensões  
 A colocação de elementos CodeGroup em um arquivo de política de segurança é importante. Para as extensões e os assemblies personalizados que você desenvolver, é recomendado colocar grupos de código personalizados logo abaixo da entrada existente para a associação "$CodeGen$/*" de URL, conforme indicado a seguir:  
  
```  
<CodeGroup  
    class="UnionCodeGroup"  
    version="1"  
    PermissionSetName="FullTrust">  
    <IMembershipCondition   
        class="UrlMembershipCondition"  
        version="1"  
        Url="$CodeGen$/*"  
    />  
</CodeGroup>  
<CodeGroup   
    class="UnionCodeGroup"  
    version="1"  
    PermissionSetName="FullTrust"  
    Name="MyCustomCodeGroup"  
    Description="Code group for my custom extension">  
        <IMembershipCondition class="UrlMembershipCondition"  
        version="1"  
        Url="C:\Program Files\Microsoft SQL Server\MSSQL\Reporting Services\ReportServer\bin\MyAssembly.dll"  
        />  
</CodeGroup>  
```  
  
 Grupos de código adicionais podem ser adicionados um depois do outro.  
  
## <a name="see-also"></a>Consulte também  
 [Compreender as políticas de segurança](understanding-security-policies.md)  
  
  
