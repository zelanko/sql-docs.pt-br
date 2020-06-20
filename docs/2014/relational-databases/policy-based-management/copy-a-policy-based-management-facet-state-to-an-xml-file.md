---
title: Copiar um estado de faceta do gerenciamento baseado em políticas para um arquivo XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, copy facet state to XML file
ms.assetid: 7d604ab1-6dd6-4f8e-a79c-eba99ab106fd
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1daea321a8d81b3476b6abb7eb328f5d59c9df41
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068960"
---
# <a name="copy-a-policy-based-management-facet-state-to-an-xml-file"></a>Copiar um estado de faceta do Gerenciamento Baseado em Políticas para um arquivo XML
  Este tópico descreve como copiar o estado de uma faceta de Gerenciamento Baseado em Política para um arquivo XML no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para copiar um estado de faceta para um arquivo XML, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Os procedimentos deste tópico exigem a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-copy-a-facet-state-to-an-xml-file"></a>Para copiar um estado de faceta para um arquivo XML  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um objeto de instância, banco de dados ou objeto de banco de dados e clique em **Facetas**.  
  
2.  Na caixa de diálogo **Exibir Facetas -**_nome_do_objeto_, clique em **Exportar Estado Atual como Política**.  
  
3.  Na caixa de diálogo **Exportar como Política** , digite o caminho e o nome do arquivo ou use o botão Procurar (**...**) para localizar o arquivo e digite o nome do arquivo XML. Para obter mais informações sobre as opções disponíveis nesta caixa de diálogo, consulte [Export As Policy Dialog Box](export-as-policy-dialog-box.md).  
  
4.  Ao concluir, clique em **OK**.  
  
  
