---
title: Suporte multiplataforma em seus componentes personalizados | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016)
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49cdcb7768103ba9cfd62a58bcdcbf5399ae09a1
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="support-multi-targeting-in-your-custom-components"></a>Suporte multiplataforma em seus componentes personalizados
 Agora você pode usar o Designer SSIS no SSDT (SQL Server Data Tools) para criar, manter e executar pacotes destinados ao SQL Server 2016, SQL Server 2014 ou SQL Server 2012. Para obter o SSDT para Visual Studio 2015, consulte [Baixar o SQL Server Data Tools mais recente](../../ssdt/download-sql-server-data-tools-ssdt.md). 

 No Gerenciador de Soluções, clique com o botão direito do mouse em um projeto do Integration Services e selecione **Propriedades** para abrir as páginas de propriedades do projeto. Na guia **Geral** de **Propriedades de Configuração**, selecione a propriedade **TargetServerVersion** e, em seguida, escolha o SQL Server 2012, SQL Server 2014 ou SQL Server 2016.  
   
 ![Propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto](../../integration-services/media/targetserverversion2.png "Propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>Suporte a múltiplas versões e multiplataforma para componentes personalizados
 
Todos os cinco tipos de extensões personalizadas do SSIS dão suporte multiplataforma.
-   Gerenciadores de conexões
-   Tarefas
-   Enumeradores
-   Provedores de logs
-   Componentes de fluxo de dados

Para extensões gerenciadas, o Designer SSIS carrega a versão da extensão para a versão de destino especificada. Por exemplo:
-   Quando a versão de destino for SQL Server 2012, o designer carregará a versão de 2012 da extensão.
-   Quando a versão de destino for SQL Server 2016, o designer carregará a versão de 2016 da extensão.

Extensões COM não dão suporte multiplataforma. O Designer SSIS sempre carrega a extensão COM para versão atual do SQL Server, independentemente da versão de destino especificada.

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>Adicionar suporte básico para várias versões e multiplataforma

Para obter diretrizes básicas, consulte [Obter extensões personalizadas do SSIS a receberem suporte a várias versões do SSDT 2015 para SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/). Esta postagem de blog descreve as etapas ou requisitos a seguir.

-   Implante os assemblies nas pastas apropriadas.

-   Criar um arquivo de mapa de extensão para o SQL Server 2014 e versões superiores.

## <a name="add-code-to-switch-versions"></a>Adicionar código para alternar entre versões

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>Alternar entre versões em uma tarefa, enumerador, provedor de logs ou gerenciador de conexões personalizado

Para uma tarefa, enumerador, provedor de logs ou gerenciador de conexões personalizado, adicione lógica de downgrade no método **SaveToXML**.

```csharp
public void SaveToXML(XmlDocument doc, IDTSInfoEvents events)
{
    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
    }

    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2012)
    {
         // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
    }
}
```

### <a name="switch-versions-in-a-custom-data-flow-component"></a>Alternar entre versões em um componente de fluxo de dados personalizado

Para uma tarefa, enumerador, provedor de logs ou gerenciador de conexões personalizado, adicione lógica de downgrade no novo método **PerformDowngrade**.

```csharp
public override void PerformDowngrade(int pipelineVersion, DTSTargetServerVersion targetServerVersion)
{
    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
        ComponentMetaData.Version = 8;
    }

    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2012)
    {
          // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
        ComponentMetaData.Version = 6;
    }
}
```

## <a name="common-errors"></a>Erros comuns

### <a name="invalidcastexception"></a>InvalidCastException

**Mensagem de erro.** Não é possível converter o objeto COM do tipo 'System.__ComObject para o tipo de interface 'Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100'. Esta operação falhou porque a chamada de QueryInterface no componente COM para a interface com IID '{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}' falhou devido ao seguinte erro: não há suporte para essa interface (exceção de HRESULT: 0x80004002 (E_NOINTERFACE)). (Microsoft.SqlServer.DTSPipelineWrap).

**Solução.** Se sua extensão personalizada faz referência a assemblies de interoperabilidade do SSIS como Microsoft.SqlServer.DTSPipelineWrap ou Microsoft.SqlServer.DTSRuntimeWrap, defina o valor da propriedade **Embed Interop Types** para **False".

![Embed Interop Types](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>Não é possível carregar alguns tipos quando a versão de destino é o SQL Server 2012

Esse problema afeta determinados tipos como IErrorReportingService ou IUserPromptService.

**Mensagem de erro (exemplo).** Não foi possível carregar o tipo 'Microsoft.DataWarehouse.Design.IErrorReportingService' do assembly 'Microsoft.DataWarehouse, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91'.

**Solução alternativa.** Use uma MessageBox em vez dessas interfaces quando a versão de destino é o SQL Server 2012.

