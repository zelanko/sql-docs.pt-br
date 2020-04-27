---
title: MSSQLSERVER_3168 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3168 (Database Engine error)
ms.assetid: 991111d9-1eb3-43e9-9333-a75a775c3200
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ea24081f4b3a41211f3bd8d6bba52aaec8b74fc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62868738"
---
# <a name="mssqlserver_3168"></a>MSSQLSERVER_3168
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|3168|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LDDB_SYSTEMWRONGVER|  
|Texto da mensagem|O backup do banco de dados do sistema no dispositivo %ls não pode ser restaurado porque foi criado por uma versão diferente (%ls) da versão deste servidor (%ls).|  
  
## <a name="explanation"></a>Explicação  
 Não é possível restaurar um backup de um banco de dados do sistema (**master**, **model** ou **msdb**) em um build do servidor diferente do build em que o backup foi originalmente executado.  
  
> [!NOTE]  
>  A instalação de uma compilação de service pack ou de hotfix altera o número de compilação do servidor e as compilações do servidor são sempre incrementais.  
  
### <a name="possible-causes"></a>Possíveis causas  
 O esquema de banco de dados para os bancos de dados do sistema pode ter sido alterado nas compilações do servidor. Para certificar-se de que uma alteração de esquema não cause inconsistências, a instrução RESTORE compara o número de compilação do servidor no arquivo de backup com o número de compilação do servidor no qual você está tentando restaurar o backup. Se as compilações forem diferentes, a instrução emitirá uma mensagem de erro 3168 e a operação de restauração será terminada de forma anormal.  
  
 Alguns cenários nos quais esse problema pode acontecer incluem os seguintes:  
  
-   Um usuário tenta restaurar um banco de dados do sistema no servidor A partir de um backup executado no servidor B. Os servidores A e B estão em diferentes compilações do servidor. Por exemplo, o servidor A pode estar em uma compilação da versão original e o servidor B pode estar em uma compilação de service pack 1 (SP1).  
  
-   Um usuário tenta restaurar um banco de dados do sistema a partir de um backup executado no mesmo servidor. Porém, o servidor estava executando uma compilação diferente quando o backup aconteceu. Isto é, o servidor foi atualizado desde a realização do backup.  
  
## <a name="user-action"></a>Ação do usuário  
 O processo de restauração nessa situação está claramente envolvido e só é usado em último caso. Para obter mais informações, consulte “[Não é possível restaurar backups de banco de dados do sistema em um build diferente do SQL Server](https://support.microsoft.com/kb/264474)”.  
  
## <a name="see-also"></a>Consulte Também  
 [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
  
