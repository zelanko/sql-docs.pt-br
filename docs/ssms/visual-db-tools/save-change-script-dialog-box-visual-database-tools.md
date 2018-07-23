---
title: Caixa de diálogo Salvar Script de Alteração (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.generatechangescript
- vdtsql.chm:65544
ms.assetid: fc9d1639-5efa-44fe-a04f-4d4d0def2833
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 16c01e5b60cc893d653a2cfdcff846ee9e6bcb27
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38030824"
---
# <a name="save-change-script-dialog-box-visual-database-tools"></a>Caixa de diálogo Salvar Script de Alteração (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Essa caixa de diálogo mostra o script do [!INCLUDE[tsql](../../includes/tsql_md.md)] para as alterações que você fez desde a última vez em que você salvou a tabela. Isso também lhe permite salvar o script para um arquivo de texto em um local de sua escolha.  
  
Você pode acessar essa caixa de diálogo depois de ter feito alterações não salvas em uma tabela no Designer de tabela. No menu **Designer de Tabela** , clique em **Gerar Script de Alteração**.  
  
> [!NOTE]  
> Scripts de alteração fornecidos pelo Visual Database Tools não contêm nenhum tratamento de erros. Eles assumem que os objetos de banco de dados não foram alterados desde que a ferramenta foi aberta e que, portanto, não ocorrerão problemas relacionados a alterações. Antes de executar um script de alteração, deve-se incluir as instruções adequadas de tratamento de erros.  
  
## <a name="options"></a>Opções  
**Gerar script de alteração automaticamente em todos os salvamentos**  
Se a caixa de diálogo **Salvar Script de Alteração** estiver marcada, ela aparecerá sempre que você salvar alterações em uma tabela.  
  
**Sim**  
Ative a caixa de diálogo **Salvar** , em que você poderá escolher o local para o arquivo de texto.  
  
**Não**  
Cancele a criação do script de alteração.  
  
