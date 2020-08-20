---
description: Formatos de exibição de assinatura (Master Data Services)
title: Formatos de exibição da assinatura
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ff1e2566-ac8f-467d-a6d9-12c3f13879b9
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ac58c9c1edfce6b02f48c31e220d37d842b18527
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456725"
---
# <a name="subscription-view-formats-master-data-services"></a>Formatos de exibição de assinatura (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Com base na entidade ou na hierarquia derivada selecionada, os seguintes formatos estão disponíveis para sua exibição de assinatura.  
  
## <a name="subscription-view-formats"></a>Formatos de exibição da assinatura  
  
|Nome|Descrição|  
|----------|-----------------|  
|**Membros folha**|Contém membros folha e seus valores de atributo associados.|  
|**Histórico de Membros Folha**|Contém dados históricos de membros folha e seus valores de atributo associados. O formato de exibição é Dimensão de Alteração Lenta Tipo 4.|  
|**SCD de Membros Folha Tipo 2**|Contém dados históricos e atuais de membros folha e seus valores de atributo associados. O formato de exibição é Dimensão de Alteração Lenta Tipo 2.|  
|**Membros consolidados**|Contém membros consolidados e seus valores de atributo associados.|  
|**Histórico de Membros Consolidados**|Contém dados históricos de membros consolidados e seus valores de atributo associados. O formato de exibição é Dimensão de Alteração Lenta Tipo 4.|  
|**SCD de Membros Consolidados Tipo 2**|Contém dados históricos e atuais de membros consolidados e seus valores de atributo associados. O formato de exibição é Dimensão de Alteração Lenta Tipo 2.|  
|**Associação da coleção**|Contém uma lista de coleções e seus valores de atributo associados.|  
|**Coleções**|Contém uma lista de coleções e os membros em cada uma, junto com valores de peso e ordem de classificação.|  
|**Histórico de Membros da Coleção**|Contém dados históricos de membros da coleção e seus valores de atributo associados. O formato de exibição é Dimensão de Alteração Lenta Tipo 4.|  
|**SCD de Membros da Coleção Tipo 2**|Contém dados históricos e atuais de membros da coleção e seus valores de atributo associados. O formato de exibição é Dimensão de Alteração Lenta Tipo 2.|  
|**Filho de Pai Explícito**|Contém estruturas de hierarquia explícitas para uma entidade em um formato filho de pai.|  
|**Níveis Explícitos**|Contém estruturas de hierarquia explícitas para uma entidade em formato de nível.|  
|**Filho de Pai Derivado (Exibição de Hierarquia Derivada)**|Contém uma estrutura de hierarquia derivada em formato filho de pai.|  
|**Níveis Derivados (Exibição de Hierarquia Derivada)**|Contém uma estrutura de hierarquia derivada em formato de nível.|  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral: exportando dados &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [Criar uma exibição de assinatura para exportar dados &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)  
  
  
