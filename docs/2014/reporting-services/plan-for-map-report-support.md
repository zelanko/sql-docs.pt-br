---
title: Planejar o suporte a relatórios de mapa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ddc97a7-7ee5-475d-bc49-3b814dce7e19
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df796e2dd4e132164f00716a9cb12f7b498d8984
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108077"
---
# <a name="plan-for-map-report-support"></a>Planejar para suporte ao relatório de mapa
  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]dá suporte a relatórios de mapa que usam fontes de dados espaciais. Os dados espaciais podem vir de bancos de dados do SQL Server, de arquivos de formas ESRI ou da Galeria de Mapas instalada com o Reporting Services ou o Construtor de Relatórios. Um mapa também pode exibir um plano de fundo de peças de mapas do Bing. Um autor de relatório pode criar um relatório que especifica dados espaciais ou peças de mapa do Bing como dinâmicos e recuperados em tempo de execução ou como estáticos e inseridos na definição de relatório.  
  
## <a name="support-for-bing-maps"></a>Suporte para Bing Maps  
 Os mapas podem incluir uma camada em segundo plano que exibe peças de mapa do Bing. Para exibir um relatório publicado que tem uma camada de peça de mapa, o servidor de relatório deve ser configurado para recuperar peças de mapa dos Serviços Web do Bing Maps. Para obter mais informações, consulte [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md).  
  
 Em cada relatório, os autores de relatório podem especificar se usar uma conexão de Protocolo SSL para recuperar peças do servidor de peças de mapa. Para fazer isso, no painel Propriedades da camada do bloco, é necessário definir a propriedade booliana UseSecureConnection como `true`.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso de peças de mapa do Bing no seu relatório, consulte [termos de uso adicionais](https://go.microsoft.com/fwlink/?LinkId=151371) e a [Política de Privacidade](https://go.microsoft.com/fwlink/?LinkId=151372).  
  
## <a name="report-design-recommendations"></a>Recomendações de design de relatórios  
 O bom design para relatórios de mapa requer que o autor do relatório avalie as desvantagens entre dados espaciais estáticos e dinâmicos e encontre o equilíbrio ideal para os usuários do relatório. Elementos de mapa inseridos podem aumentar significativamente o tamanho da definição do relatório, mas reduzem o tempo necessário para exibir o mapa no relatório. Elementos de mapa dinâmico reduzem o tamanho da definição do relatório, mas aumentam o tempo necessário para processar e exibir o mapa. O autor do relatório deve localizar o equilíbrio certo entre estes problemas.  
  
 Quando o tamanho da definição de relatório é um problema, como administrador de servidor de relatório, você pode encorajar os designers de relatório a reduzirem a quantidade de dados espaciais em uma definição de relatório.  
  
 Sob as condições a seguir, elementos de mapa são inseridos na definição de relatório:  
  
-   Quando o relatório é criado, a fonte de dados espaciais está no sistema de arquivos local. Isso inclui dados espaciais da Galeria de Mapas ou arquivos de formas ESRI que foram instalados localmente. Por padrão, o assistente de mapa e o assistente de camada do mapa inserem dados espaciais de fontes de dados no sistema de arquivos local.  
  
-   O autor do relatório escolhe a opção para inserir dados espaciais manualmente no relatório.  
  
 Para ajudar a reduzir o tamanho de definições de relatório que têm mapas, os autores de relatório podem usar um ou mais das opções seguintes:  
  
-   No Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], adicione fontes de dados espaciais que são arquivos de formas ESRI para o projeto do servidor de relatório. Quando você implanta o projeto, os arquivos de formas ESRI são publicados no servidor de relatório além do relatório. Quando o autor de relatório executa o assistente de Mapa, ele pode especificar uma fonte de dados espacial do projeto de Servidor de Relatório e os elementos de mapas não são incorporados por padrão nas definições de relatório.  
  
-   No Construtor de Relatórios, adicione fontes de dados espaciais que são arquivos de formas ESRI selecionando Arquivos de formas no servidor de relatório. Quando o autor do relatório executa o assistente de Mapa, ele pode navegar e selecionar uma fonte de dados espaciais no servidor de relatório e, por padrão, os elementos de mapa não são inseridos nas definições de relatório.  
  
-   Quando os dados de mapa devem ser inseridos, ajuste o centro do visor e o nível de zoom para incluir apenas os dados de mapa necessários para o relatório.  
  
 Para obter mais informações, [mapas &#40;Construtor de relatórios e SSRS&#41;](report-design/maps-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Solucionar problemas de relatórios: mapear relatórios &#40;Construtor de Relatórios e SSRS&#41;](report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
