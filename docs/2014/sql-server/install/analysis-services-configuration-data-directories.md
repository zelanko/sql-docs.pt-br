---
title: Configuração de Analysis Services-diretórios de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ef732855-b7af-4f40-a619-5573c1c354bb
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 47d4299cde4575f7443faa1546aeffdb41fe12d5
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83859168"
---
# <a name="analysis-services-configuration---data-directories"></a>Configuração do Analysis Services - diretórios de dados
  Os diretórios padrão na tabela a seguir podem ser configurados pelo usuário durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A permissão para acessar esses arquivos é concedida a administradores locais e a membros do grupo de segurança SQLServerMSASUser$\<instância> que é criado e provisionado durante a instalação.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
  
|Description|Diretório padrão|Recomendações|  
|-----------------|-----------------------|---------------------|  
|Diretório raiz de dados|C:\Arquivos de Programas\microsoft SQL Server\MSAS12. \< InstanceID> \OLAP\Data \| Verifique se a pasta \Program files\Microsoft SQL Server \ está protegida com permissões limitadas. O desempenho do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] depende, em muitas configurações, do desempenho do armazenamento no qual o diretório de dados está localizado. Coloque esse diretório no armazenamento de melhor desempenho conectado ao sistema. Para instalações de cluster de failover, verifique se os diretórios de dados estão colocados no disco compartilhado.|  
|Diretório do arquivo de log|C:\Arquivos de Programas\microsoft SQL Server\MSAS12. \< InstanceID> \OLAP\Log \| esse é o diretório para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] arquivos de log e inclui o log FlightRecorder. Se você aumentar a duração do registrador de voo, atente para que o diretório de logs tenha espaço suficiente.|  
|Diretório temporário|C:\Arquivos de Programas\microsoft SQL Server\MSAS12. \< InstanceID> \OLAP\Temp \| Coloque o diretório temp no subsistema de armazenamento de alto desempenho.|  
|Diretório de backup|C:\Arquivos de Programas\microsoft SQL Server\MSAS12. \< InstanceID> \OLAP\Backup \| este é o diretório para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] arquivos de backup padrão. Em instalações do PowerPivot para SharePoint, também é onde os Serviços de Sistema PowerPivot armazenam em cache arquivos de dados PowerPivot.<br /><br /> Verifique se as permissões apropriadas estão definidas para impedir perda de dados e se o grupo de usuários do serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tem permissões suficientes para gravar no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
## <a name="notes"></a>Observações  
  
-   As instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que são implantadas em um farm do SharePoint armazenam arquivos de aplicativos, arquivos de dados e propriedades em bancos de dados de conteúdo e bancos de dados de aplicativo de serviços.  
  
-   Ao adicionar recursos a uma instalação existente, não é possível alterar o local de um recurso instalado anteriormente, nem especificar o local para o novo recurso.  
  
-   Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também devem ser instalados em diretórios separados.  
  
-   Os arquivos de programas e os arquivos de dados não podem ser instalados nas seguintes situações:  
  
    -   Em uma unidade de disco removível  
  
    -   Em um sistema de arquivos que usa compactação  
  
    -   Em um diretório onde os arquivos do sistema estão localizados  
  
## <a name="see-also"></a>Consulte Também  
 [Locais de arquivos para instâncias padrão e nomeadas do SQL Server](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
  
