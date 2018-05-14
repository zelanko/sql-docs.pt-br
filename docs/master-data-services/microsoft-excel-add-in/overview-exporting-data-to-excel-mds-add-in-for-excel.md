---
title: 'Visão geral: Exportando dados para o Excel (Suplemento MDS para Excel) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: microsoft-excel-add-in
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b628548b-982b-4e45-abf4-c8e83e3ab1c2
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 54d22cd0f649c8a30a4d0eb5c69240ac2da9d4d1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="overview-exporting-data-to-excel-mds-add-in-for-excel"></a>Visão geral: Exportando dados para o Excel (Suplemento MDS para Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], é necessário carregar os dados do repositório do MDS em uma planilha ativa do Excel antes que você possa trabalhar com eles. Quando você terminar o trabalho com os dados, importe-os para o repositório do MDS para que outros usuários possam compartilhá-los.  
  
 Os dados exportados são limitados àqueles que você tem permissão para acessar. A permissão para acessar os dados é definida no aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ou programaticamente.  
  
 Ao exportar grandes quantidades de dados, você pode definir os avisos que são exibidos quando os dados levam muito tempo para serem carregados. Para fazer isso, no grupo **Opções** , clique em **Configurações**. Na guia **Dados** , selecione **Exibir aviso de filtro para grandes conjuntos de dados**.  
  
> [!WARNING]  
>  Uma pasta de trabalho habilitada para MDS deve ser aberta e atualizada somente no Excel com o Suplemento de MDS para Excel. Abrir uma pasta de trabalho habilitada para MDS no Excel em um computador no qual o Suplemento do Excel do MDS não está instalado não tem suporte e pode causar corrupção do arquivo da pasta de trabalho. Se você quiser compartilhar dados com outra pessoa, envie por email um arquivo de consulta de atalho, em vez de salvar a planilha e enviá-la por email. Para obter mais informações sobre a consulta, consulte [Enviar um arquivo de consulta de atalho por email &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md).  
  
## <a name="filtering-data"></a>Filtrando dados  
 Você pode filtrar os dados antes de importá-los para limitar a quantidade de dados baixada. Isso inclui a seleção dos atributos (colunas) que você deseja carregar, a ordem em que deseja exibir os atributos e os membros (linhas de dados) com os quais deseja trabalhar. Para obter mais informações, consulte [Filtrar dados antes da exportação &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md).  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>Conectar-se automaticamente e carregar dados usados frequentemente  
 Se você desejar se conectar sempre ao mesmo servidor e exportar o mesmo conjunto de dados, poderá criar arquivos de consulta de atalho que contêm informações de conexão e de filtro. Para obter mais informações sobre arquivos de consulta, consulte [Shortcut Query Files &#40;MDS Add-in for Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md).  
  
## <a name="refreshing-data"></a>Atualizando dados  
 Os dados do repositório do MDS poderão ser atualizados por outros usuários após a exportação. Você pode recuperar esses dados sem perder as alterações feitas nos dados não MDS. Para obter mais informações, consulte [Atualizando dados &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Filtre os dados do MDS antes de carregá-los no Excel.|[Filtrar dados antes da exportação &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)|  
|Carregue os dados do MDS no Excel.|[Exportar dados para o Excel do Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|Altere a ordem das colunas antes de baixar os dados.|[Reordenar colunas &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Conexões &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [Arquivos de consulta de atalho &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Suplemento do Master Data Services para Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
-   [Segurança &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
  
