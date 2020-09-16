---
description: Caixa de diálogo Salvar Script de Alteração (Visual Database Tools)
title: Caixa de diálogo Salvar Script de Alteração
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.generatechangescript
- vdtsql.chm:65544
ms.assetid: fc9d1639-5efa-44fe-a04f-4d4d0def2833
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 7388283d4605547a400c284c2499e4f0d9c4db46
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468323"
---
# <a name="save-change-script-dialog-box-visual-database-tools"></a>Caixa de diálogo Salvar Script de Alteração (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Essa caixa de diálogo mostra o script do [!INCLUDE[tsql](../../includes/tsql-md.md)] para as alterações que você fez desde a última vez em que você salvou a tabela. Isso também lhe permite salvar o script para um arquivo de texto em um local de sua escolha.  
  
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
  
