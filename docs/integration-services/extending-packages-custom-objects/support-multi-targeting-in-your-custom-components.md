---
title: Suporte multiplataforma seus componentes personalizados | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016)
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bf7649b06354bfa621624ddfcf22bdea90bf0467
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="support-multi-targeting-in-your-custom-components"></a>Suporte a vários destinos em seus componentes personalizados
 Agora você pode usar o Designer de SSIS no SQL Server Data Tools (SSDT) para criar, manter e executar pacotes que o destino do SQL Server 2016, SQL Server 2014 ou SQL Server 2012. Para obter o SSDT para Visual Studio 2015, consulte [baixar SQL Server Data Tools mais recente](https://msdn.microsoft.com/library/mt204009.aspx). 

 No Gerenciador de Soluções, clique com o botão direito do mouse em um projeto do Integration Services e selecione **Propriedades** para abrir as páginas de propriedades do projeto. Na guia **Geral** de **Propriedades de Configuração**, selecione a propriedade **TargetServerVersion** e, em seguida, escolha o SQL Server 2012, SQL Server 2014 ou SQL Server 2016.  
   
 ![A propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto](../../integration-services/media/targetserverversion2.png "propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>Suporte à versão vários e multiplataforma para componentes personalizados
 
Todos os cinco tipos de extensões personalizadas SSIS oferece suporte multiplataforma.
-   Gerenciadores de conexões
-   Tarefas
-   Enumeradores
-   Provedores de logs
-   Componentes de fluxo de dados

Para extensões gerenciadas, o Designer SSIS carrega a versão da extensão para a versão de destino especificado. Por exemplo:
-   Quando a versão de destino for SQL Server 2012, o designer carrega a versão 2012 da extensão.
-   Quando a versão de destino for SQL Server 2016, o designer carrega a versão de 2016 da extensão.

Extensões COM não dão suporte a vários destinos. Designer SSIS sempre carrega a extensão COM a versão atual do SQL Server, independentemente da versão de destino especificado.

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>Adicionar suporte básico para várias versões e vários destinos

Para obter orientações básicas, consulte [obtendo suas extensões personalizadas do SSIS com suporte pelo suporte a várias versões de 2015 SSDT para SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/). Esta postagem de blog descreve as seguintes etapas ou requisitos.

-   Implante assemblies para as pastas apropriadas.

-   Crie um arquivo de mapa de extensão para o SQL Server 2014 e versões alta.

## <a name="add-code-to-switch-versions"></a>Adicione código para alternar versões

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>Versões de comutador em um Gerenciador de conexão personalizada, a tarefa, o enumerador ou o provedor de log

Para um Gerenciador de conexão personalizada, tarefas, enumerador ou provedor de log, adicionar lógica de downgrade no **SaveToXML** método.

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

### <a name="switch-versions-in-a-custom-data-flow-component"></a>Versões de comutador em um componente de fluxo de dados personalizados

Para um Gerenciador de conexão personalizada, tarefas, enumerador ou provedor de log, adicionar lógica de downgrade no novo **PerformDowngrade** método.

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

**Mensagem de erro.** Não é possível converter o objeto COM do tipo 'REC0 ComObject' interface tipo 'Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100'. Esta operação falhou porque a chamada de QueryInterface no componente COM para a interface com IID '{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}' falhou devido ao seguinte erro: há suporte para essa interface (exceção de HRESULT: 0x80004002 (E_NOINTERFACE)). (Dtspipelinewrap).

**Solução.** Se sua extensão personalizado faz referência a assemblies de interoperabilidade do SSIS como dtspipelinewrap ou dtsruntimewrap, defina o valor da **Embed Interop Types** propriedade para * * False ".

![Inserir tipos de interoperabilidade](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>Não é possível carregar alguns tipos, quando a versão de destino é o SQL Server 2012

Esse problema afeta determinados tipos como IErrorReportingService ou IUserPromptService.

**Mensagem de erro (exemplo).** Não foi possível carregar o tipo 'Microsoft.DataWarehouse.Design.IErrorReportingService' do assembly ' Microsoft.DataWarehouse, Version = 13.0.0.0, Culture = neutral, PublicKeyToken = 89845dcd8080cc91'.

**Solução alternativa.** Use uma MessageBox em vez dessas interfaces, quando a versão de destino é o SQL Server 2012.


