---
title: MSSQLSERVER_1203 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1203 (Database Engine error)
ms.assetid: 33a35f00-98c8-46c6-b432-544b326b6117
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bed60fc9fd7ceddbebff276ddecbf2c5bf9c7c12
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968046"
---
# <a name="mssqlserver_1203"></a>MSSQLSERVER_1203
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|1203|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LK_NOT|  
|Texto da mensagem|A ID de processo %d tentou desbloquear um recurso que não tem: %.*ls. Tente a transação novamente, porque esse erro pode ter sido causado por uma condição de tempo. Se o problema persistir, contate o administrador de banco de dados.|  
  
## <a name="explanation"></a>Explicação  
 Esse erro acontece quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está envolvido em alguma atividade diferente da limpeza usual de pós-processamento e acha que uma determinada página que está tentando desbloquear já está desbloqueada.  
  
### <a name="possible-causes"></a>Possíveis causas  
 A causa subjacente deste erro pode estar relacionada a problemas estruturais dentro do banco de dados afetado. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerencia a aquisição e a liberação de páginas para manter o controle de simultaneidade no ambiente multiusuário. Esse mecanismo é mantido pelo uso de várias estruturas de bloqueio interno que identificam a página e o tipo de bloqueio presente. Os bloqueios são adquiridos para processar páginas afetadas e são liberados quando o processamento é finalizado.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute o DBCC CHECKDB no banco de dados em que o objeto se encontra. Se o DBCC CHECKDB não informar nenhum erro, você deverá tentar restabelecer a conexão e executar o comando.  
  
> [!IMPORTANT]  
>  Se você estiver executando o DBCC CHECKDB com uma das cláusulas REPAIR e isso não corrigir o problema de índice, ou se você não estiver seguro de qual efeito o DBCC CHECKDB com uma cláusula de REPAIR terá sobre seus dados, entre em contato com seu provedor de suporte.  
  
  
