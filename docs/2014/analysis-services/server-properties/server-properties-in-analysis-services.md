---
title: Configurar propriedades de servidor no Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, configuration properties
- Analysis Services, configuration properties
- SQL Server Analysis Services, configuration properties
- configuration options [Analysis Services]
- server properties [Analysis Services]
- properties [Analysis Services], configuration
- properties [Analysis Services]
ms.assetid: 274b89cd-14ed-4666-bc13-eedf1de51e18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 31c05bbc1be8376144eb191ff28a9cdc6eebdd8a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66068897"
---
# <a name="configure-server-properties-in-analysis-services"></a>Configurar propriedades de servidor no Analysis Services
  Um administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode modificar as propriedades padrão de configuração do servidor para uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Cada instância tem suas próprias propriedades de configuração que podem ser definidas independentemente de outras instâncias no mesmo servidor.  
  
 Para definir propriedades de servidor, use o SQL Server Management Studio ou edite o arquivo msmdsrv.ini de uma instância específica.  
  
 Este tópico contém as seguintes seções:  
  
 [Configurar propriedades de servidor (instância)](#bkmk_config)  
  
 [Referência de propriedades de servidor](#bkmk_ref)  
  
##  <a name="bkmk_config"></a> Configurar propriedades de servidor (instância)  
 As páginas de propriedades no SQL Server Management Studio contêm um subconjunto das propriedades disponíveis, enquanto mostrando só essas propriedades que são ser modificadas mais provável. O conjunto cheio de propriedades pode ser localizado no arquivo msmdsrv.ini.  
  
> [!NOTE]  
>  Este tópico não documenta as propriedades de configuração de implantação no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações sobre a configuração de implantação, consulte [especificando as definições de configuração para implantação de solução](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md).  
  
#### <a name="view-or-set-configuration-properties-in-management-studio"></a>Exibir ou definir as propriedades de configuração no Management Studio  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
     No Pesquisador de Objetos, clique com o botão direito do mouse na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e clique em **Propriedades**. A página Geral aparece, exibindo as propriedades usadas mais comumente.  
  
2.  Para exibir propriedades adicionais, clique na caixa de seleção **Mostrar (Todas) as Propriedades Avançadas** na parte inferior da página.  
  
     Modificar as propriedades de servidor tem suporte somente para servidores de modos de tabela e modos multidimensionais. Se você instalou o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], sempre use os valores padrão a menos que você seja direcionado de outra forma por um engenheiro de suporte de produto da Microsoft.  
  
     Para obter orientação sobre como resolver problemas operacionais ou de desempenho por meio de propriedades de servidor, consulte [Guia de operações do SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
     Você também pode ler sobre as propriedades de servidor (basicamente, muitas delas permanecem inalteradas nas últimas versões) neste white paper da Microsoft, [SQL Server 2005 Analysis Services (SSAS) Server Properties](https://go.microsoft.com/fwlink/?LinkID=199102)(Propriedades de servidor do SSAS [SQL Server 2005 Analysis Services]).  
  
    > [!NOTE]  
    >  Algumas propriedades só podem ser definidas no msmdrsrv.ini arquivo. Se a propriedade que você deseja definir não for nem sequer visível que depois que você mostrar propriedades avançadas, precisará editar o msmdsrv.ini arquivo diretamente.  
  
#### <a name="view-or-edit-configuration-properties-in-the-msmdsrvini-file"></a>Exibir ou editar manualmente propriedades de configuração no arquivo msmdsrv.ini  
  
1.  Antes de você começar, verifique a **DataDir** propriedade na página de propriedades Geral em Management Studio verificar o local dos arquivos de programa de Analysis Services, incluindo o arquivo msmdsrv.ini. Verificando o local dos arquivos de programa assegurará que você está modificando o arquivo correto.  
  
    > [!NOTE]  
    >  Em uma instalação padrão, o arquivo pode ser localizado na pasta \Arquivos de Programas\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP\Config  
  
2.  Criar um backup do arquivo no caso de você precisa reverter ao arquivo original.  
  
3.  Usar um editor de texto para exibir ou editar o arquivo msmdsrv.ini.  
  
4.  Após salvar o arquivo, reinicie o serviço.  
  
##  <a name="bkmk_ref"></a> Referência à propriedade de servidor  
 As propriedades de configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são importantes para o ajuste refinado do sistema. Por exemplo, para tornar o comportamento das consultas consistente com seus requisitos, você pode definir as propriedades pertinentes.  
  
 Os tópicos seguintes explicam as várias propriedades de configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] :  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Propriedades gerais](general-properties.md)|As propriedades gerais são básicas e avançadas e, incluem propriedades que definem o diretório de dados, diretório de backup e outros comportamentos do servidor.|  
|[Propriedades de mineração de dados](data-mining-properties.md)|As propriedades de mineração de dados que controlam quais algoritmos são habilitados e quais são desabilitados. Por padrão, todos os algoritmos são habilitados.|  
|DSO|DSO não tem mais suporte. Propriedades DSO são ignoradas.|  
|[Propriedades de recurso](feature-properties.md)|As propriedades do recurso pertencem aos recursos de produtos, a maioria delas avançadas, inclusive propriedades que controlam vínculos entre instâncias do servidor.|  
|[Propriedades de armazenamento de arquivos](filestore-properties.md)|As propriedades de repositório de arquivos são apenas para uso avançado. Elas incluem configurações de gerenciamento de memória avançadas.|  
|[Propriedades do gerenciador de bloqueio](lock-manager-properties.md)|As propriedades do gerenciador de bloqueio definem os comportamentos do servidor em relação aos bloqueios e aos tempos limite. A maioria dessas propriedades é apenas para uso avançado.|  
|[Propriedades do log](log-properties.md)|As propriedades de log controlam onde e como os eventos são registrados no servidor. Isso inclui log de erros, log de exceções, flight recorder, log de consultas e rastreamentos.|  
|[Propriedades de memória](memory-properties.md)|As propriedades de memória controlam como o servidor usa a memória. Eles são principalmente para uso avançado.|  
|[Propriedades de rede](network-properties.md)|As propriedades de rede controlam o comportamento do servidor referente ao sistema de rede, inclusive propriedades que controlam a compressão e XML binário. A maioria dessas propriedades é apenas para uso avançado.|  
|[Propriedades OLAP](olap-properties.md)|As propriedades OLAP controlam o processamento de dimensões e cubo, processamento lento, cache de dados e comportamento das consultas. Isso inclui propriedades básicas e avançadas.|  
|[Propriedades de segurança](security-properties.md)|A seção de segurança contém propriedades básicas e avançadas que definem as permissões de acesso. Isso inclui configurações que pertencem a administradores e usuários.|  
|[Propriedades de pool de threads](thread-pool-properties.md)|As propriedades de pool de threads controlam quantos threads o servidor cria. Essas são principalmente propriedades avançadas.|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de instância do Analysis Services](../instances/analysis-services-instance-management.md)   
 [Especificando definições de configuração para implantação de solução](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
