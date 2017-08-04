---
title: "Conexões (suplemento MDS para Excel) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2f2b2f9d-7744-460e-83cd-56d34ea70ff0
caps.latest.revision: 12
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3223a2a26e9476549afd5bd5dbdef84337414ac8
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="connections-mds-add-in-for-excel"></a>Conexões (suplemento MDS para Excel)
  Para baixar dados no [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], você deve primeiramente criar uma conexão. Uma conexão é como o serviço Web do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] sabe a qual banco de dados do MDS deve se conectar.  
  
 A cadeia de caracteres de conexão geralmente é a URL do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo web, por exemplo `http://contoso/mds`.  
  
 Sempre que você iniciar o Excel, deverá conectar-se a um repositório do MDS. A única exceção é quando a planilha ativa já contêm dados gerenciados no MDS. Nesse caso, uma conexão será estabelecida automaticamente sempre que você atualizar ou publicar dados na planilha.  
  
 Você pode criar várias conexões. A conexão acessada mais recentemente será considerada como padrão.  
  
 Vários usuários podem ser conectados ao mesmo tempo. No entanto, conflitos podem ocorrer quando vários usuários tentarem publicar os mesmos dados. Para obter mais informações, consulte [Visão geral: Importando dados do Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md).  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>Conectar-se automaticamente e carregar dados usados frequentemente  
 Se você desejar conectar-se sempre ao mesmo servidor e carregar o mesmo conjunto de dados, poderá criar arquivos de consulta de atalho que contenham informações de conexão e de filtro. Para obter mais informações sobre arquivos de consulta, consulte [Arquivos de consulta de atalho &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md).  
  
## <a name="data-quality-services"></a>Data Quality Services  
 O [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] possui a funcionalidade Data Quality Services para ajudar a combinar os dados antes de publicá-los no repositório do MDS. Ao fazer uma conexão, se um banco de dados DQS estiver instalado na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que está o banco de dados MDS, você poderá ver os botões do DQS na faixa de opções. Se o banco de dados DQS_Main não existir na instância, esses botões não serão exibidos e a funcionalidade de qualidade de dados não estará disponível.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Crie uma conexão com um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Conectar-se a um repositório do MDS &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Carregue os dados do MDS no Excel.|[Exportar dados para o Excel do Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|Filtre os dados do MDS antes de carregá-los no Excel.|[Filtrar dados antes da exportação &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Visão geral: Exportando dados para o Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [Arquivos de consulta de atalho &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Suplemento do Master Data Services para Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
  
