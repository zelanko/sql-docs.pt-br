---
title: Habilitar a integração do Data Quality Services com Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ab32938d-a80e-4106-80d4-94b2de3d67dc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5cf9a81134af8d6e90a1b869f8cc011a17a4b93a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482919"
---
# <a name="enable-data-quality-services-integration-with-master-data-services"></a>Habilitar a integração do Data Quality Services com Master Data Services
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], a funcionalidade correspondente é fornecida pelo DQS (Data Quality Services). Essa funcionalidade deve ser habilitada para ser usada.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Um aplicativo Web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e banco de dados devem existir.  
  
-   O recurso Data Quality Services e o Cliente Data Quality devem ser instalados na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados do MDS. Para obter mais informações, consulte [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
### <a name="to-enable-data-quality-services-integration"></a>Para habilitar a integração do Data Quality Services  
  
1.  Abra o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  No painel esquerdo, clique em **Configuração da Web**.  
  
3.  Na página **Configuração da Web** , selecione o site e o aplicativo Web.  
  
4.  Na seção **Habilitar Integração do DQS** , clique em **Habilitar integração com Data Quality Services**.  
  
5.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Correspondência de qualidade de dados no Suplemento MDS para Excel](../microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Suplemento do Master Data Services para Microsoft Excel](../microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)   
 [Instalar o Master Data Services](install-master-data-services.md)  
  
  
