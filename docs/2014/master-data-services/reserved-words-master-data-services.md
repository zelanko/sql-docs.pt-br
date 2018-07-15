---
title: Palavras reservadas (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2aaee670cd89e957a6ad4700963606ffe0d4ef4f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221658"
---
# <a name="reserved-words-master-data-services"></a>Palavras reservadas (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], quando você cria objetos ou membros de modelo, algumas palavras não podem ser usadas. Usar essas palavras pode causar erros.  
  
> [!NOTE]  
>  Você também deve limitar o uso de caracteres especiais (símbolos, hifenização, etc.)  
  
-   [Modelos](#models)  
  
-   [Entidades](#entities)  
  
-   [Hierarquias explícitas](#exhierarchies)  
  
-   [Atributos](#attributes)  
  
-   [Membros](#members)  
  
##  <a name="models"></a> Modelos  
 Se você cria um modelo com o nome definido como **nome**, não selecione **criar entidade com o mesmo nome do modelo** porque **nome** não pode ser usado para o nome de uma entidade.  
  
##  <a name="entities"></a> Entidades  
 Para nomes de entidade, você não pode usar **Name** nem **Code**.  
  
##  <a name="exhierarchies"></a> Hierarquias explícitas  
 Para nomes de hierarquia explícita, você não pode usar **Name** nem **Code**.  
  
##  <a name="attributes"></a> Atributos  
  
-   **ID**  
  
-   **Code**  
  
-   **Nome**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> Membros  
 Para membros, você não pode usar **MDMMemberStatus** ou **raiz** para o **código** valor do atributo.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do Master Data Services](master-data-services-overview-mds.md)  
  
  
