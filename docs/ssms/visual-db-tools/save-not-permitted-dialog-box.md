---
title: "Caixa de diálogo Salvar (Não Permitido) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.table.tablerecreatenosave.f1
ms.assetid: 7efda8e3-739f-4c97-a497-b8808a0acbea
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1224061affb1882d717f184f974a176d30a24a8
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="save-not-permitted-dialog-box"></a>Caixa de diálogo Salvar (Não Permitido)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] A caixa de diálogo **Salvar** (Não Permitido) avisa que não é permitido salvar as alterações que você fez, pois elas requerem que as tabelas listadas sejam descartadas e recriadas.  
  
As ações seguintes poderiam exigir a recriação de uma tabela:  
  
-   Adição de uma nova coluna no meio da tabela  
  
-   Descarte de uma coluna  
  
-   Alteração da nulidade da coluna  
  
-   Alteração da ordem das colunas  
  
-   Alteração do tipo de dados de uma coluna  
  
Para alterar essa opção, no menu **Ferramentas** , clique em **Opções**, expanda **Designers**e clique em **Designers de Tabela e Banco de Dados**. Marque ou desmarque a caixa de seleção **Evitar salvar alterações que exijam recriação de tabela** .  
  
