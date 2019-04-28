---
title: Exibir as propriedades de uma faceta de gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facet properties
ms.assetid: 022a244c-c2e7-4467-b9a2-c7a27859be22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c819fc7fb3b1cc73b67362a0eabd82ad33946fbc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62676861"
---
# <a name="view-the-properties-of-a-policy-based-management-facet"></a>Exibir as propriedades de uma faceta de gerenciamento baseado em políticas
  Este tópico descreve como exibir as propriedades de uma faceta do Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir as propriedades de uma faceta, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-facet"></a>Para visualizar as propriedades de uma faceta  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém a faceta cujas propriedades você deseja exibir.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Facetas** .  
  
5.  Clique com o botão direito do mouse na faceta cujas propriedades você deseja exibir e selecione **Propriedades**. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Propriedades da faceta -**_nome_da_faceta_, confira [Caixa de diálogo Propriedades de Faceta, página Geral](../../integration-services/general-page-of-integration-services-designers-options.md), [Caixa de diálogo Propriedades da Faceta, página Políticas Dependentes](facet-properties-dialog-box-dependent-policies-page.md) e [Caixa de diálogo Propriedades da Faceta, página Condições Dependentes](facet-properties-dialog-box-dependent-conditions-page.md).  
  
6.  Quando terminar, clique em **Fechar**.  
  
  
