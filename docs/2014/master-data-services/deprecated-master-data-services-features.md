---
title: Recursos de Master Data Services preteridos no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 89d2d5d8cee989d6541cdb256b0a7aaf48d00162
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48142206"
---
# <a name="deprecated-master-data-services-features-in-sql-server-2014"></a>Recursos do Master Data Services substituídos no SQL Server 2014
  Este tópico descreve os recursos substituídos do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que ainda estão disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Esses recursos estão programados para serem removidos em uma versão futura do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Recursos preteridos não devem ser usados em aplicativos novos.  
  
## <a name="staging-process"></a>Processo de preparo  
 O processo de preparo que era usado no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] não está mais disponível no aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . No entanto, ele ainda está disponível no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Erros de preparo do processo de preparo do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] não são mais exibidos na interface do usuário. Códigos de erro que eram populados durante o processo de preparo ainda estão disponíveis nas tabelas de preparo e podem ser encontrados aqui: [ http://msdn.microsoft.com/library/ff487022.aspx ](http://msdn.microsoft.com/library/ff487022.aspx).  
  
 As tabelas de preparo (tblStgMember, tblStgMemberAttribute e tblStgRelationship) ainda estão disponíveis no banco de dados. O procedimento armazenado usado para iniciar o processo de preparo (mdm.udpStagingSweep) ainda está disponível no banco de dados.  
  
 Os métodos de serviço Web que chamam o processo de preparo ainda estão disponíveis.  
  
 O intervalo de preparo definido no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] aplica-se ao processo de preparo no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] e no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 Um novo processo de preparação de maior desempenho foi implementado no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Importação de dados &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
## <a name="metadata"></a>Metadados  
 Embora o modelo de metadados ainda seja exibido no aplicativo Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , ele não deve ser usado. Ela será removida em uma versão futura. Os usuários também não podem mais exibir metadados na área funcional do **Gerenciador** e você não pode mais criar versões do modelo de Metadados.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do Master Data Services descontinuados no SQL Server 2014](discontinued-master-data-services-features.md)  
  
  
