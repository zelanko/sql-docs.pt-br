---
title: Palavras reservadas (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5435c2a48417156abd6d4f831bf61c9ba6440fab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482571"
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
  
##  <a name="models"></a>Modelos  
 Se você criar um modelo com o nome definido como **nome**, não selecione **criar entidade com o mesmo nome que o modelo** porque o **nome** não pode ser usado para o nome de uma entidade.  
  
##  <a name="entities"></a>Contabilidade  
 Para nomes de entidade, você não pode usar **Name** nem **Code**.  
  
##  <a name="exhierarchies"></a>Hierarquias explícitas  
 Para nomes de hierarquia explícita, você não pode usar **Name** nem **Code**.  
  
##  <a name="attributes"></a>Atributos  
  
-   **SESSÃO**  
  
-   **Código**  
  
-   **Nome**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a>Os  
 Para membros, você não pode usar **MDMMemberStatus** ou **root** para o valor do atributo **Code** .  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Master Data Services](master-data-services-overview-mds.md)  
  
  
