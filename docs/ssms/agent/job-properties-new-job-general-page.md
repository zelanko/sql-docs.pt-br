---
description: Propriedades do trabalho – Novo trabalho (página Geral)
title: Propriedades do trabalho – Novo trabalho (página Geral)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.general.f1
ms.assetid: b6832840-1c18-4db8-94fc-080db880ae9f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 992a0ecbc8ec36ce88ca44490d04a6354828a116
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97408852"
---
# <a name="job-properties---new-job-general-page"></a>Propriedades do trabalho – Novo trabalho (página Geral)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> Atualmente, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.

Use esta página para ver e modificar as propriedades gerais de um trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Nome**  
Altera o nome do trabalho.  
  
**Proprietário**  
Seleciona o proprietário para o trabalho.  
  
**Categoria**  
Seleciona a categoria de trabalho para o trabalho.  
  
**...**  
Exibe os trabalhos na categoria selecionada.  
  
**Descrição**  
Altera a descrição do trabalho.  
  
**Enabled**  
Habilita o trabalho. Quando o trabalho não está habilitado, ele não é executado em resposta a uma agenda ou a um alerta, embora você ainda possa iniciar o trabalho usando o procedimento armazenado **sp_start_job** .  
  
**Origem**  
Exibe o servidor mestre para o trabalho. Só disponível na página **Propriedades do Trabalho** – Geral.  
  
**Criado**  
Exibe a data e hora em que o trabalho foi criado. Só disponível na página **Propriedades do Trabalho** – Geral.  
  
**Última modificação**  
Exibe a data e a hora em que o trabalho foi modificado pela última vez. Só disponível na página **Propriedades do Trabalho** – Geral.  
  
**Última execução**  
Exibe a data e hora em que a execução do trabalho foi iniciada pela última vez. Só disponível na página **Propriedades do Trabalho** – Geral.  
  
**Exibir Histórico de Trabalho**  
Exibe o histórico do trabalho para o trabalho Só disponível na página **Propriedades do Trabalho** – Geral.  
  
## <a name="see-also"></a>Consulte Também  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
[Categorias de trabalho – Gerenciar categorias de trabalho](../../ssms/agent/job-categories-manage-job-categories.md)  
