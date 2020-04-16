---
title: sys.bandwidth_usage (Banco de Dados Azure SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ea963c07a15cd5c2db3cca113680026d3100936b
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "67942572"
---
# <a name="sysbandwidth_usage-azure-sql-database"></a>sys.bandwidth_usage (Banco de Dados SQL do Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

> [!NOTE]
> Isso se aplica [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]apenas a V11.**  
  
 Retorna informações sobre a largura de banda de rede usada por cada banco de dados em um ** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] servidor de banco de dados V11**, . Cada linha retornada para um banco de dados determinado resume uma única direção e a classe de uso durante um período de uma hora.  
  
 **Isso foi preterido [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]em um .**  
  
 A exibição **sys.bandwidth_usage** contém as seguintes colunas.  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**time**|A hora em que a largura de banda foi consumida. As linhas nessa exibição são por hora. Por exemplo, 2009-09-19 02:00:00.000 significa que a largura de banda foi consumida em 19 de setembro de 2009 entre 2h e 3h.|  
|**database_name**|O nome do banco de dados que usou largura de banda.|  
|**Direção**|O tipo de largura de banda que foi usado, um de:<br /><br /> Ingress: Dados que estão [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]se movendo para o .<br /><br /> Egress: Dados que estão [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]saindo do .|  
|**classe**|A classe da largura de banda que foi usada, um de:<br />Interno: Dados que estão se movendo dentro da plataforma Azure.<br />Externo: Dados que estão saindo da plataforma Azure.<br /><br /> Esta classe será retornada somente se o banco de dados estiver envolvido em uma relação de cópia contínua entre regiões ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]). Se um determinado banco de dados não participar de qualquer relação de cópia contínua, as linhas "Interlink" não serão devolvidas. Para obter mais informações, consulte "Comentários", posteriormente neste tópico.|  
|**time_period**|O período de tempo em que o uso ocorreu é Pico ou Fora do Horário de Pico. The Peak time is based on the region in which the server was created. Por exemplo, se um servidor tiver sido criado na região "US_Northwest", o horário de pico será definido como estando entre 10h e 18h. PST.|  
|**quantity**|A quantidade de largura de banda, em quilobytes (KBs), que foi usada.|  
  
## <a name="permissions"></a>Permissões

 Essa exibição só está disponível no banco de dados **principal** para o login principal em nível de servidor.  
  
## <a name="remarks"></a>Comentários  
  
### <a name="external-and-internal-classes"></a>Classes External e Internal

 Para cada banco de dados usado em um determinado momento, a exibição **sys.bandwidth_usage** retorna linhas que mostram a classe e a direção do uso da largura de banda. O exemplo a seguir ilustra os dados que podem ser expostos para um banco de dados específico. Neste exemplo, a hora é 2012-04-21 17:00:00, que ocorre durante o horário de pico. O nome do banco de dados é Db1. Neste exemplo, **sys.bandwidth_usage** retornou uma linha para todas as quatro combinações das direções de Ingress e Egress e classes Externas e Internas, da seguinte forma:  
  
|time|database_name|direction|classe|time_period|quantidade|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|Entrada|Externo|Peak|66|  
|2012-04-21 17:00:00|Db1|Saída|Externo|Peak|741|  
|2012-04-21 17:00:00|Db1|Entrada|Interna|Peak|1052|  
|2012-04-21 17:00:00|Db1|Saída|Interna|Peak|3525|  
  
### <a name="interpreting-data-direction-for-ssgeodr"></a>Interpretando a direção de dados do [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]

 Para [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)], os dados de uso de largura de banda são visíveis no banco de dados mestre lógico nos dois lados de uma relação de cópia contínua. Portanto, você deve interpretar os indicadores de direção de ingestão e saída da perspectiva das bases de dados que você está consultando. Por exemplo, considere um fluxo de replicação que transfere 1 MB de dados do servidor de origem para o servidor de destino. Nesse caso, no servidor de origem, 1 MB é contado como total de dados enviados, e no servidor de destino, 1 MB é registrado como dados recebidos.  
  
> [!NOTE]  
> O volume de dados transferido vai do servidor de origem para o servidor de destino, na direção do fluxo de dados do usuário. No entanto, é necessário fazer alguma transferência de dados na outra direção.  
