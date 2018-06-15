---
title: Mapas personalizados em relatórios móveis do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea22c2ea60a681accc747e9426fbecb4aad7b515
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33018513"
---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Mapas personalizados nos relatórios móveis do Reporting Services
Os mapas geográficos no Editor de Relatórios Móveis do SQL Server são definidos em um formato conhecido como *ESRI shapefiles*.  
  
Criado inicialmente por uma empresa privada, esse é agora um formato semiaberto amplamente usado em grande parte dos aplicativos GIS. De acordo com esse formato, o Editor de Relatórios Móveis exige que dois arquivos sejam fornecidos ao definir um mapa:  
  
- Um arquivo .SHP para geometrias de forma  
- Um arquivo .DBF para metadados  
  
Os nomes dos arquivos de base devem corresponder (por exemplo, *canada.shp* e *canada.dbf*). Os metadados devem incluir o campo *NAME* com o valor do nome da forma correspondente (chave) a ser usado ao preencher o mapa com os dados.  
  
> **Observação**: os dois arquivos de mapa juntos, o SHP e DBF, não podem ser maiores do que 512 KB. Se os arquivos de mapa forem muito grandes, use uma ferramenta como [http://mapshaper.org/](http://mapshaper.org/) para reduzir seu tamanho.  
  
Consulte como [Adicionar mapas personalizados a relatórios móveis](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md).  
  
## <a name="technical-information"></a>Informações técnicas  
  
- A especificação oficial: [http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- O arquivo shapefile da Wikipedia: [http://en.wikipedia.org/wiki/Shapefile](http://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>Criando e editando geometria de mapa  
  
Criar e editar shapefiles é um processo complexo que está além do escopo deste documento. Aqui estão alguns recursos e aplicativos para ajudá-lo a começar:  
  
- ArcGIS: [http://www.arcgis.com/](http://www.arcgis.com/)  
- Plug-in MAPublisher para Adobe Illustrator: [http://www.avenza.com/mapublisher](http://www.avenza.com/mapublisher)  
- QuantumGIS (gratuito): [http://www.qgis.org/](http://www.qgis.org/)  
- Manco ShapeFile Editor: [http://www.mancosoftware.com/ShapeFileEditor](http://www.mancosoftware.com/ShapeFileEditor)  
  
## <a name="existing-shapefiles"></a>Shapefiles existentes  
  
Muitos shapefiles existentes podem ser baixados da Web, de sites como estes:  
  
- Diva-GIS: [http://www.diva-gis.org/Data](http://www.diva-gis.org/Data)  
- OpenStreetMap: [http://openstreetmapdata.com/data](http://openstreetmapdata.com/data)  
  
### <a name="see-also"></a>Confira também  
- [Mapas nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Criar e publicar relatórios móveis com o Editor de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
