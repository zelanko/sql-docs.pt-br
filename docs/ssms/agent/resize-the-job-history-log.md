---
description: Resize the Job History Log
title: Resize the Job History Log
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 99a06d15025dd4a8ee6970aeb5175bbe58d4cc36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492033"
---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log

[!INCLUDE[applies-to-version/_ssnoversion.md](../../includes/applies-to-version/sqlserver.md)]

> [!IMPORTANT]  
> Atualmente, na [Instância Gerenciada de SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.

Este tópico descreve como definir os limites de tamanho para logs de histórico de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

- **Antes de começar:**  

    [Segurança](#Security)  

- **Para definir limites de tamanho para logs de histórico de trabalho, usando:**  

    [SQL Server Management Studio](#SSMS)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  

### <a name="security"></a><a name="Security"></a>Segurança

Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  

## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Usando o SQL Server Management Studio

*Para redimensionar o log do histórico de trabalhos, com base em um tamanho bruto*

1. No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.

2. Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.

3. Selecione a página **Histórico** e assegure que **Limitar tamanho do log do histórico de trabalho** esteja marcado.

4. Na caixa **Tamanho máximo do log do histórico de trabalho** , insira o número máximo de linhas que o log de histórico do trabalho deve permitir.

5. Na caixa **Máximo de linhas do log do histórico de trabalho por trabalho** , insira o número máximo de linhas que o log de histórico do trabalho deve permitir para um trabalho.

**Para redimensionar o log do histórico de trabalhos com base no tempo:**

1. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e expanda-a.  

2. Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.

3. Selecione a página **Histórico** e selecione **Remover o histórico do agente**.

4. Selecione o número apropriado de **Dias**, **Semanas**ou **Meses**.
