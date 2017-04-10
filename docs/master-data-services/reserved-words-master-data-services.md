---
title: "Palavras reservadas (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "palavras reservadas [Master Data Services]"
  - "Master Data Services, palavras reservadas"
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
caps.latest.revision: 11
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 11
---
# Palavras reservadas (Master Data Services)
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
  
-   **Código**  
  
-   **EnterUserName**  
  
-   **LastChgUserName**  
  
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
 Para membros, você não pode usar **MDMMemberStatus**, **MDMUnused**ou **ROOT** como valor do atributo **Código** .  
  
## Consulte também  
 [Visão geral do Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
  