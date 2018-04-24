---
title: Categorias de trabalho – Gerenciar categorias de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.job.categories.f1
helpviewer_keywords:
- Job Categories dialog box
ms.assetid: 38276438-40b1-43ce-9aae-6805be6d9332
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e1a24047bc2d1bc79bcb5a054607df822d5b24b7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="job-categories---manage-job-categories"></a>Categorias de trabalho – Gerenciar categorias de trabalho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use a caixa de diálogo **Categorias de Trabalho** para adicionar ou excluir categorias de trabalho. Categorias de trabalho internas não podem ser excluídas.  
  
## <a name="options"></a>Opções  
**Nome**  
O nome da categoria de trabalho.  
  
**Número de trabalhos na categoria**  
O número de trabalhos definido para essa categoria.  
  
**Exibir Trabalhos**  
Abre a caixa de diálogo **Propriedades** para a categoria selecionada, para listar todos os trabalhos atualmente definidos para aquela categoria.  
  
**Adicionar**  
Abre a caixa de diálogo **Nova Categoria de Trabalho** , para adicionar uma nova categoria de trabalho  
  
**Delete (excluir)**  
Remove a categoria de trabalho selecionada. Habilitada somente para categorias de trabalho definidas pelo usuário.  
  
**Atualizar**  
Consulta o servidor para obter as informações atuais.  
  
#### <a name="to-access-the-job-categories-dialog-box"></a>Para acessar a caixa de diálogo Categorias de trabalho  
  
1.  No **Pesquisador de Objetos**, expanda **SQL Server Agent**, clique com o botão direito do mouse em **Trabalhos**e, então, clique em **Gerenciar Categorias de Trabalho**.  
  
