---
title: Habilitar a integração do Data Quality Services
description: No suplemento Master Data Services para Excel, a funcionalidade correspondente é fornecida pelo DQS (Data Quality Services).
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ab32938d-a80e-4106-80d4-94b2de3d67dc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 27c374ff84a33ed750c9b425dae9a75c6b33f8e0
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "92257839"
---
# <a name="enable-data-quality-services-integration-with-master-data-services"></a>Habilitar a integração do Data Quality Services com Master Data Services

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], a funcionalidade correspondente é fornecida pelo DQS (Data Quality Services). Essa funcionalidade deve ser habilitada para ser usada.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Um aplicativo Web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e banco de dados devem existir.  
  
-   O recurso Data Quality Services e o Cliente Data Quality devem ser instalados na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados do MDS. Para obter mais informações, consulte [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
### <a name="to-enable-data-quality-services-integration"></a>Para habilitar a integração do Data Quality Services  
  
1.  Abra o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  No painel esquerdo, clique em **Configuração da Web**.  
  
3.  Na página **Configuração da Web** , selecione o site e o aplicativo Web.  
  
4.  Na seção **Habilitar Integração do DQS** , clique em **Habilitar integração com Data Quality Services**.  
  
5.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Correspondência de qualidade de dados no Suplemento MDS para Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Suplemento do Master Data Services para Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)   
 [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
