---
title: sys. bandwidth_usage (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- bandwidth_usage
- sys.bandwidth_usage
- bandwidth_usage_TSQL
- sys.bandwidth_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.bandwidth_usage
- bandwidth_usage
ms.assetid: 43ed8435-f059-4907-b5c0-193a258b394a
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1accec58750bfd4a3806308252113a6c2aecc2ac
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031109"
---
# <a name="sysbandwidthusage-azure-sql-database"></a>sys.bandwidth_usage (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Observação: Isso se aplica somente ao [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.**  
  
 Retorna informações sobre a largura de banda usada por cada banco de dados em um  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] servidor lógico do V11**,. Cada linha retornada para um banco de dados determinado resume uma única direção e a classe de uso durante um período de uma hora.  
  
 **Isso foi substituído em uma [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] servidor lógico V12.**  
  
 O **sys. bandwidth_usage** exibição contém as colunas a seguir.  
  
|Column Name|Description|  
|-----------------|-----------------|  
|**time**|A hora em que a largura de banda foi consumida. As linhas nessa exibição são por hora. Por exemplo, 2009-09-19 02:00:00.000 significa que a largura de banda foi consumida em 19 de setembro de 2009 entre 2h e 3h.|  
|**database_name**|O nome do banco de dados que usou largura de banda.|  
|**Direção**|O tipo de largura de banda que foi usado, um de:<br /><br /> Entrada: Dados que são movidos para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Saída: Dados que são movidos para fora do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**class**|A classe da largura de banda que foi usada, um de:<br />Interno: Dados que são movidos dentro da plataforma do Azure.<br />Externas: Dados que são movidos para fora da plataforma do Azure.<br /><br /> Essa classe é retornado somente se o banco de dados está envolvido em uma relação de cópia contínua entre regiões ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]). If a given database does not participate in any continuous copy relationship, then “Interlink” rows are not returned. Para obter mais informações, consulte a seção "Comentários", posteriormente neste tópico.|  
|**time_period**|O período de tempo em que ocorreu o uso é o horário de pico ou OffPeak. The Peak time is based on the region in which the server was created. Por exemplo, se um servidor tiver sido criado na região "US_Northwest", o horário de pico será definido como estando entre 10h e 18h. PST.|  
|**quantity**|A quantidade de largura de banda, em quilobytes (KBs), que foi usada.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição só está disponível na **mestre** banco de dados para o logon principal no nível do servidor.  
  
## <a name="remarks"></a>Remarks  
  
### <a name="external-and-internal-classes"></a>Classes External e Internal  
 Para cada banco de dados usado em um determinado momento, o **sys. bandwidth_usage** exibição retorna linhas que mostram a classe e a direção do uso de largura de banda. O exemplo a seguir ilustra os dados que podem ser expostos para um banco de dados específico. Neste exemplo, a hora é 2012-04-21 17:00:00, que ocorre durante o horário de pico. O nome do banco de dados é Db1. Neste exemplo, **sys. bandwidth_usage** retornou uma linha para todas as quatro combinações Ingress e Egress das direções das classes External e Internal, da seguinte maneira:  
  
|time|database_name|direction|class|time_period|quantity|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|Ingress|External|Peak|66|  
|2012-04-21 17:00:00|Db1|Egress|External|Peak|741|  
|2012-04-21 17:00:00|Db1|Ingress|Internal|Peak|1052|  
|2012-04-21 17:00:00|Db1|Egress|Internal|Peak|3525|  
  
### <a name="interpreting-data-direction-for-includessgeodrincludesssgeodr-mdmd"></a>Interpretando a direção de dados do [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]  
 Para [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)], os dados de uso de largura de banda são visíveis no banco de dados mestre lógico nos dois lados de uma relação de cópia contínua. Portanto, você deve interpretar os indicadores de direção ingress e egress sob a perspectiva do servidor lógico que você está consultando. Por exemplo, considere um fluxo de replicação que transfere 1 MB de dados do servidor de origem para o servidor de destino. Nesse caso, no servidor de origem, 1 MB é contado como total de dados enviados, e no servidor de destino, 1 MB é registrado como dados recebidos.  
  
> [!NOTE]  
>  O volume de dados transferido vai do servidor de origem para o servidor de destino, na direção do fluxo de dados do usuário. No entanto, é necessário fazer alguma transferência de dados na outra direção.  
  
  
