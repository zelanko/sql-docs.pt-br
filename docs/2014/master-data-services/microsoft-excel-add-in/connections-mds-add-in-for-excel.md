---
title: Conexões (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 2f2b2f9d-7744-460e-83cd-56d34ea70ff0
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c5593e7dd54ebdfcc2eb67dd94f6f9f9dd02cbcb
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360058"
---
# <a name="connections-mds-add-in-for-excel"></a>Conexões (suplemento MDS para Excel)
  Para baixar dados no [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], você deve primeiramente criar uma conexão. Uma conexão é como o serviço Web do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] sabe a qual banco de dados do MDS deve se conectar.  
  
 Normalmente, a cadeia de conexão é a URL do aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], por exemplo, http://contoso/mds.  
  
 Sempre que você iniciar o Excel, deverá conectar-se a um repositório do MDS. A única exceção é quando a planilha ativa já contêm dados gerenciados no MDS. Nesse caso, uma conexão será estabelecida automaticamente sempre que você atualizar ou publicar dados na planilha.  
  
 Você pode criar várias conexões. A conexão acessada mais recentemente será considerada como padrão.  
  
 Vários usuários podem ser conectados ao mesmo tempo. No entanto, conflitos podem ocorrer quando vários usuários tentarem publicar os mesmos dados. Para obter mais informações, consulte [dados de publicação &#40;suplemento MDS para Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md).  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>Conectar-se automaticamente e carregar dados usados frequentemente  
 Se você desejar conectar-se sempre ao mesmo servidor e carregar o mesmo conjunto de dados, poderá criar arquivos de consulta de atalho que contenham informações de conexão e de filtro. Para obter mais informações sobre arquivos de consulta, consulte [Arquivos de consulta de atalho &#40;Suplemento MDS para Excel&#41;](shortcut-query-files-mds-add-in-for-excel.md).  
  
## <a name="data-quality-services"></a>Data Quality Services  
 O [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] possui a funcionalidade Data Quality Services para ajudar a combinar os dados antes de publicá-los no repositório do MDS. Ao fazer uma conexão, se um banco de dados DQS estiver instalado na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que está o banco de dados MDS, você poderá ver os botões do DQS na faixa de opções. Se o banco de dados DQS_Main não existir na instância, esses botões não serão exibidos e a funcionalidade de qualidade de dados não estará disponível.  
  
## <a name="troubleshooting-connections"></a>Solucionando problemas de conexões  
 Quando você se conectar ao MDS, se você encontrar qualquer consulte problemas [ https://social.technet.microsoft.com/wiki/contents/articles/4520.aspx ](https://social.technet.microsoft.com/wiki/contents/articles/4520.aspx) para dicas de solução de problemas.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Crie uma conexão com um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Conectar-se a um repositório do MDS &#40;Suplemento MDS para Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Carregue os dados do MDS no Excel.|[Carregar dados do MDS no Excel](export-data-to-excel-from-master-data-services.md)|  
|Filtre os dados do MDS antes de carregá-los no Excel.|[Filtrar dados antes de carregar &#40;suplemento do MDS para Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Carregamento de dados &#40;suplemento do MDS para Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [Arquivos de consulta de atalho &#40;Suplemento MDS para Excel&#41;](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Suplemento do Master Data Services para Microsoft Excel](master-data-services-add-in-for-microsoft-excel.md)  
  
  
