---
title: Palavras reservadas (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
caps.latest.revision: 11
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: af5326c054f80b376e43db0d18dfeb2b9ef85997
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="reserved-words-master-data-services"></a>Palavras reservadas (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], quando você cria objetos ou membros de modelo, algumas palavras não podem ser usadas. Usar essas palavras pode causar erros.  
  
> [!NOTE]  
>  Você também deve limitar o uso de caracteres especiais (símbolos, hifenização, etc.)  
  
-   [Modelos](../master-data-services/reserved-words-master-data-services.md#models)  
  
-   [Entidades](../master-data-services/reserved-words-master-data-services.md#entities)  
  
-   [Hierarquias explícitas](../master-data-services/reserved-words-master-data-services.md#exhierarchies)  
  
-   [Atributos](../master-data-services/reserved-words-master-data-services.md#attributes)  
  
-   [Membros](../master-data-services/reserved-words-master-data-services.md#members)  
  
##  <a name="models"></a> Modelos  
 Se você criar um modelo com o nome definido como **Name** ou **Code**, não selecione **Criar entidade com o mesmo nome como modelo** porque **Name** ou **Code** não podem ser usados para o nome de uma entidade.  
  
##  <a name="entities"></a> Entidades  
 Para nomes de entidade, você não pode usar **Name** nem **Code**.  
  
##  <a name="exhierarchies"></a> Hierarquias explícitas  
 Para nomes de hierarquia explícita, você não pode usar **Name** nem **Code**.  
  
##  <a name="attributes"></a> Atributos  
  
-   **ID**  
  
-   **Code**  
  
-   **EnterUserName**  
  
-   **LastChgUserName**  
  
-   **Name**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> Membros  
 Para membros, você não pode usar **MDMMemberStatus**, **MDMUnused**ou **ROOT** como valor do atributo **Código** .  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
  

