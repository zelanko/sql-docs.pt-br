---
description: organizar trabalhos
title: organizar trabalhos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job category
- organize jobs
ms.assetid: 629c3e06-f933-483b-8621-280dbb7a7bd1
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 4e89519a5524126808a52ea663800de8b9b9b323
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440411"
---
# <a name="organize-jobs"></a>organizar trabalhos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

As categorias de trabalho ajudam a organizar os trabalhos de modo a facilitar sua filtragem e agrupamento. Por exemplo, você pode organizar todos os seus trabalhos de backup de banco de dados na categoria Manutenção de Banco de Dados. Você também pode criar suas próprias categorias de trabalho.  
  
> [!WARNING]  
> As categorias multisservidor só existem em um servidor mestre. Há apenas uma categoria de trabalho padrão disponível em um servidor mestre: [**Não Categorizado (Multisservidor)**]. Quando um trabalho multisservidor é baixado, sua categoria é alterada para **Trabalhos do MSX** no servidor de destino.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição|Tópico|  
|-|-|  
|Descreve como criar uma categoria de trabalho.|[Criar uma categoria de trabalho](../../ssms/agent/create-a-job-category.md)|  
|Descreve como excluir uma categoria de trabalho.|[Excluir uma categoria de trabalho](../../ssms/agent/delete-a-job-category.md)|  
|Descreve como atribuir um trabalho a uma categoria de trabalho.|[Atribuir um trabalho a uma categoria de trabalho](../../ssms/agent/assign-a-job-to-a-job-category.md)|  
|Descreve como alterar a associação de uma categoria de trabalho.|[Change the Membership of a Job Category](../../ssms/agent/change-the-membership-of-a-job-category.md)|  
|Descreve como listar as informações de categoria.|[Listar informações de categoria de trabalho](../../ssms/agent/list-job-category-information.md)|  
