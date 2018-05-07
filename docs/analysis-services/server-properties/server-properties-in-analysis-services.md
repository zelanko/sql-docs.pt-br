---
title: Propriedades do servidor do Analysis Services | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9ac78e321f9e2f760e6d4eb2cb7114e1f2c0fa5b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="server-properties-in-analysis-services"></a>Propriedades do servidor do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode modificar as propriedades padrão de configuração do servidor de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Cada instância tem suas próprias propriedades de configuração, que são definidas de forma independente de outras instâncias no mesmo servidor.  
  
 Para configurar o servidor, use o SQL Server Management Studio ou edite o arquivo msmdsrv.ini de uma instância específica.  
 
As páginas de propriedades do SQL Server Management Studio mostram um subconjunto das propriedades mais prováveis de serem modificadas. A lista completa de propriedades pode ser encontrada no arquivo msmdsrv.ini.   
  
> [!NOTE]  
>  Em uma instalação padrão, msmdsrv.ini pode ser encontrado na pasta \Program Files\Microsoft SQL Server\MSAS13.MSSQLSERVER\OLAP\Config.
> 
> Outras propriedades que afetam a configuração do servidor incluem as propriedades de configuração de implantação no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações sobre essas propriedades, consulte [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md).
 
##  <a name="bkmk_config"></a> Configurar as propriedades no Management Studio 
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2. No Pesquisador de Objetos, clique com o botão direito do mouse na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e clique em **Propriedades**. A página Geral aparece, exibindo as propriedades usadas mais comumente.  

3.  Para exibir propriedades adicionais, clique na caixa de seleção **Mostrar (Todas) as Propriedades Avançadas** na parte inferior da página.  
  
     Modificar as propriedades de servidor tem suporte somente para servidores de modos de tabela e modos multidimensionais. Se você instalou o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], sempre use os valores padrão, a menos que seja de outra forma direcionado pelo Suporte da Microsoft.  
  
     Para obter orientação sobre como resolver problemas operacionais ou de desempenho por meio de propriedades de servidor, consulte [Guia de operações do SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
     Você também pode ler sobre as propriedades de servidor (basicamente, muitas delas permanecem inalteradas nas últimas versões) neste white paper da Microsoft, [SQL Server 2005 Analysis Services (SSAS) Server Properties](http://go.microsoft.com/fwlink/?LinkID=199102)(Propriedades de servidor do SSAS [SQL Server 2005 Analysis Services]).    
  
##  <a name="bkmk_msmdsrvini"></a> Configurar as propriedades no msmdsrv.ini
  Algumas propriedades só podem ser definidas no msmdrsrv.ini arquivo. Se a propriedade que você deseja definir não for nem sequer visível que depois que você mostrar propriedades avançadas, precisará editar o msmdsrv.ini arquivo diretamente.
  
1.  Verifique a propriedade **DataDir** na página de propriedades Geral em Management Studio para verificar o local dos arquivos de programa de Analysis Services, incluindo o arquivo msmdsrv.ini.

     Em um servidor que tem várias instâncias, a verificação do local do arquivo de programa garante que você está modificando o arquivo correto.  
  
2.  Navegue até a pasta **config** do local da pasta dos arquivos de programa.

3. Criar um backup do arquivo no caso de você precisa reverter ao arquivo original.  
  
4.  Usar um editor de texto para exibir ou editar o arquivo msmdsrv.ini.  
  
5.  Salve o arquivo e reinicie o serviço.  
  
##  <a name="bkmk_ref"></a> Referência à propriedade de servidor  
  
 Os seguintes tópicos descrevem as várias propriedades de configuração do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] :  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Propriedades gerais](../../analysis-services/server-properties/general-properties.md)|As propriedades gerais são básicas e avançadas e, incluem propriedades que definem o diretório de dados, diretório de backup e outros comportamentos do servidor.|  
|[Propriedades de mineração de dados](../../analysis-services/server-properties/data-mining-properties.md)|As propriedades de mineração de dados que controlam quais algoritmos são habilitados e quais são desabilitados. Por padrão, todos os algoritmos são habilitados.| 
|[Propriedades do DAX](../../analysis-services/server-properties/dax-properties.md)|Define as propriedades relacionadas a consultas DAX.|
|DSO|DSO não tem mais suporte. Propriedades DSO são ignoradas.|  
|[Propriedades do recurso](../../analysis-services/server-properties/feature-properties.md)|As propriedades do recurso pertencem aos recursos de produtos, a maioria delas avançadas, inclusive propriedades que controlam vínculos entre instâncias do servidor.|  
|[Propriedades Filestore](../../analysis-services/server-properties/filestore-properties.md)|As propriedades de repositório de arquivos são apenas para uso avançado. Elas incluem configurações de gerenciamento de memória avançadas.|  
|[Propriedades do Gerenciador de bloqueio](../../analysis-services/server-properties/lock-manager-properties.md)|As propriedades do gerenciador de bloqueio definem os comportamentos do servidor em relação aos bloqueios e aos tempos limite. A maioria dessas propriedades é apenas para uso avançado.|  
|[Propriedades de log](../../analysis-services/server-properties/log-properties.md)|As propriedades de log controlam onde e como os eventos são registrados no servidor. Isso inclui log de erros, log de exceções, flight recorder, log de consultas e rastreamentos.|  
|[Propriedades de memória](../../analysis-services/server-properties/memory-properties.md)|As propriedades de memória controlam como o servidor usa a memória. Eles são principalmente para uso avançado.|  
|[Propriedades de rede](../../analysis-services/server-properties/network-properties.md)|As propriedades de rede controlam o comportamento do servidor referente ao sistema de rede, inclusive propriedades que controlam a compressão e XML binário. A maioria dessas propriedades é apenas para uso avançado.|  
|[Propriedades OLAP](../../analysis-services/server-properties/olap-properties.md)|As propriedades OLAP controlam o processamento de dimensões e cubo, processamento lento, cache de dados e comportamento das consultas. Isso inclui propriedades básicas e avançadas.|  
|[Propriedades de segurança](../../analysis-services/server-properties/security-properties.md)|A seção de segurança contém propriedades básicas e avançadas que definem as permissões de acesso. Isso inclui configurações que pertencem a administradores e usuários.|  
|[Propriedades do Pool de threads](../../analysis-services/server-properties/thread-pool-properties.md)|As propriedades de pool de threads controlam quantos threads o servidor cria. Essas são principalmente propriedades avançadas.|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de instância do Analysis Services](../../analysis-services/instances/analysis-services-instance-management.md)   
 [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
