---
title: Validar Assinaturas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.subscriptions.f1
helpviewer_keywords:
- Validate Subscriptions dialog box
ms.assetid: 0ca39a35-f22c-46c5-82a4-342e34bf5d1b
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fba42b0cd532f61dc71c89ba67c09798f69891fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836674"
---
# <a name="validate-subscriptions"></a>Validar Assinaturas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Use a caixa de diálogo **Validar Assinaturas** para especificar que as assinaturas em uma publicação transacional devem ser validadas na próxima execução, para cada assinatura, do Distribution Agent. Os resultados de validação são exibidos no Replication Monitor. Para obter mais informações, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
## <a name="options"></a>Opções  
 **Validar todas as assinaturas SQL Server**  
 Selecione para validar dados para todas as assinaturas SQL Server nesta publicação.  
  
 **Validar estas assinaturas**  
 Selecione se você não quiser validar todas as assinaturas. Selecione na lista as assinaturas que você quer validar.  
  
 **Opções de Validação**  
 Clique para acessar a caixa de diálogo **Opções de Validação de Assinatura** , que permite especificar se deve ser usada a validação de contagem de linhas ou validação de soma de verificação binária.  
  
## <a name="see-also"></a>Consulte Também  
 [Validar os dados replicados](../../relational-databases/replication/validate-replicated-data.md)  
  
  
