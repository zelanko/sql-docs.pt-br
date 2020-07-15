---
title: Opção de configuração de servidor default trace enabled | Microsoft Docs
description: Saiba mais sobre a opção "default trace enabled". Descubra como o rastreamento padrão pode ajudar na solução de problemas.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], traces
- traces [SQL Server], logs
- default trace enabled option
ms.assetid: 1322d668-44f4-469e-8fd6-e0d02a81c8f2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bfeec7df441b841cbbaa5da7c0b693f37749e861
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772559"
---
# <a name="default-trace-enabled-server-configuration-option"></a>Opção de configuração de servidor default trace enabled
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Use a opção **default trace enabled** para habilitar ou desabilitar os arquivos de log de rastreamento padrão. A funcionalidade de rastreamento padrão proporciona um log detalhado e persistente de atividades e alterações relacionadas principalmente às opções de configuração.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.  
  
## <a name="purpose"></a>Finalidade  
 O rastreamento padrão proporciona assistência à solução de problemas para administradores de banco de dados, garantindo que eles disponham do log dos dados necessários para diagnosticar problemas na primeira vez em que ocorrem.  
  
## <a name="viewing"></a>Exibindo  
 Os logs de rastreamento padrão podem ser abertos e examinados através do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ou consultados com [!INCLUDE[tsql](../../includes/tsql-md.md)] por meio da função do sistema `fn_trace_gettable` . [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] abre os arquivos de log de rastreamento padrão da mesma forma que os arquivos de saída de rastreamento normais. O log de rastreamento padrão é armazenado, por padrão, no diretório `\MSSQL\LOG` usando um arquivo de rastreamento de substituição. O nome de arquivo de base para o arquivo de log de rastreamento padrão é `log.trc`. Em uma instalação típica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o rastreamento padrão encontra-se habilitado e, desse modo, torna-se TraceID 1. Se habilitado após a instalação e a criação de outros rastreamentos, TraceID pode se tornar um número maior.  
  
 Para obter mais informações sobre como usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler para exibir esse arquivo de rastreamento, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
### <a name="example"></a>Exemplo:  
 A instrução a seguir abre o log de rastreamento padrão no local padrão:  
  
```  
SELECT *   
FROM fn_trace_gettable  
('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\LOG\log.trc', default);  
GO  
  
```  
  
## <a name="configuring"></a>Configurando  
 Quando definida como 1, a opção **default trace enabled** habilita o **Rastreamento Padrão**. A configuração padrão desta opção é 1 (ON). Um valor 0 desativa o rastreamento.  
  
 A opção **default trace enabled** é uma opção avançada. Se estiver usando o procedimento armazenado do sistema **sp_configure** para alterar a configuração, você só poderá alterar a opção **default trace enabled** quando **show advanced options** estiver definida como 1. A configuração entra em vigor imediatamente sem a reinicialização do servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
