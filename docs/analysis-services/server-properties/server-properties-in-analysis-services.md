---
title: Propriedades do servidor do Analysis Services | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ce74bb210e3d5d3cd01120b0bd406672db6dd5ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207961"
---
# <a name="server-properties-in-analysis-services"></a>Propriedades do servidor do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Um administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode modificar as propriedades padrão de configuração do servidor de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Cada instância tem suas próprias propriedades de configuração, que são definidas de forma independente de outras instâncias no mesmo servidor.  
  
 Para configurar o servidor, use o SQL Server Management Studio ou edite o arquivo msmdsrv. ini de uma instância específica do SQL Server Analysis Services.  
 
As páginas de propriedades do SQL Server Management Studio mostram um subconjunto das propriedades mais prováveis de serem modificadas. A lista completa de propriedades pode ser encontrada no arquivo msmdsrv.ini.   
  
> [!NOTE]  
>  Em uma instalação do SQL Server Analysis Services padrão, msmdsrv. ini pode ser encontrado em \Program Files\Microsoft Server\MSAS13 SQL. Pasta MSSQLSERVER\OLAP\Config.
> 
> Outras propriedades que afetam a configuração do servidor incluem as propriedades de configuração de implantação no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações sobre essas propriedades, consulte [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md).
 
## <a name="configure-properties-in-management-studio"></a>Configurar as propriedades no Management Studio 
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2. No Pesquisador de Objetos, clique com o botão direito do mouse na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e clique em **Propriedades**. A página Geral aparece, exibindo as propriedades usadas mais comumente.  

3.  Para exibir propriedades adicionais, clique na caixa de seleção **Mostrar (Todas) as Propriedades Avançadas** na parte inferior da página.  
  
     Modificar as propriedades de servidor tem suporte somente para servidores de modos de tabela e modos multidimensionais. Se você instalou o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], sempre use os valores padrão, a menos que seja de outra forma direcionado pelo Suporte da Microsoft.  
  
  
## <a name="configure-properties-in-msmdsrvini"></a>Configurar as propriedades no msmdsrv.ini
  
Algumas propriedades só podem ser definidas no msmdrsrv.ini arquivo. Essas propriedades não se aplicam ao Azure Analysis Services.
Se a propriedade que você deseja definir não for nem sequer visível que depois que você mostrar propriedades avançadas, precisará editar o msmdsrv.ini arquivo diretamente. 
  
1.  Verifique a propriedade **DataDir** na página de propriedades Geral em Management Studio para verificar o local dos arquivos de programa de Analysis Services, incluindo o arquivo msmdsrv.ini.

     Em um servidor que tem várias instâncias, a verificação do local do arquivo de programa garante que você está modificando o arquivo correto.  
  
2.  Navegue até a pasta **config** do local da pasta dos arquivos de programa.

3. Criar um backup do arquivo no caso de você precisa reverter ao arquivo original.  
  
4.  Usar um editor de texto para exibir ou editar o arquivo msmdsrv.ini.  
  
5.  Salve o arquivo e reinicie o serviço.  
  
##  <a name="server-property-reference"></a>Referência à propriedade de servidor  
  
 Os seguintes tópicos descrevem as várias propriedades de configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] :  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Propriedades gerais](../../analysis-services/server-properties/general-properties.md)|As propriedades gerais são básicas e avançadas e, incluem propriedades que definem o diretório de dados, diretório de backup e outros comportamentos do servidor.|  
|[Propriedades de mineração de dados](../../analysis-services/server-properties/data-mining-properties.md)|As propriedades de mineração de dados que controlam quais algoritmos são habilitados e quais são desabilitados. Por padrão, todos os algoritmos são habilitados.| 
|[Propriedades do DAX](../../analysis-services/server-properties/dax-properties.md)|Define as propriedades relacionadas a consultas DAX.|
|DSO|DSO não tem mais suporte. Propriedades DSO são ignoradas.|  
|[Propriedades de recurso](../../analysis-services/server-properties/feature-properties.md)|As propriedades do recurso pertencem aos recursos de produtos, a maioria delas avançadas, inclusive propriedades que controlam vínculos entre instâncias do servidor.|  
|[Propriedades de armazenamento de arquivos](../../analysis-services/server-properties/filestore-properties.md)|As propriedades de repositório de arquivos são apenas para uso avançado. Elas incluem configurações de gerenciamento de memória avançadas.|  
|[Propriedades do gerenciador de bloqueio](../../analysis-services/server-properties/lock-manager-properties.md)|As propriedades do gerenciador de bloqueio definem os comportamentos do servidor em relação aos bloqueios e aos tempos limite. A maioria dessas propriedades é apenas para uso avançado.|  
|[Propriedades do log](../../analysis-services/server-properties/log-properties.md)|As propriedades de log controlam onde e como os eventos são registrados no servidor. Isso inclui log de erros, log de exceções, flight recorder, log de consultas e rastreamentos.|  
|[Propriedades de memória](../../analysis-services/server-properties/memory-properties.md)|As propriedades de memória controlam como o servidor usa a memória. Eles são principalmente para uso avançado.|  
|[Propriedades de rede](../../analysis-services/server-properties/network-properties.md)|As propriedades de rede controlam o comportamento do servidor referente ao sistema de rede, inclusive propriedades que controlam a compressão e XML binário. A maioria dessas propriedades é apenas para uso avançado.|  
|[Propriedades OLAP](../../analysis-services/server-properties/olap-properties.md)|As propriedades OLAP controlam o processamento de dimensões e cubo, processamento lento, cache de dados e comportamento das consultas. Isso inclui propriedades básicas e avançadas.|  
|[Propriedades de segurança](../../analysis-services/server-properties/security-properties.md)|A seção de segurança contém propriedades básicas e avançadas que definem as permissões de acesso. Isso inclui configurações que pertencem a administradores e usuários.|  
|[Propriedades de pool de threads](../../analysis-services/server-properties/thread-pool-properties.md)|As propriedades de pool de threads controlam quantos threads o servidor cria. Essas são principalmente propriedades avançadas.|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de instância do Analysis Services](../../analysis-services/instances/analysis-services-instance-management.md)   
 [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
