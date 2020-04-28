---
title: Características de execução de procedimentos armazenados estendidos
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], executing
- executing extended stored procedures [SQL Server]
ms.assetid: 6fe1f7e8-cc02-49df-8a2a-d47a96ec3567
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 74ecd20f28e58e133b5710d3cbd9d18b27ca7756
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74095983"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>Características de execução de procedimentos armazenados estendidos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 A execução de um procedimento armazenado estendido tem as seguintes características:  
  
-   A função de procedimento armazenado estendido é executada no contexto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]segurança do.  
  
-   A função de procedimento armazenado estendido é executada no espaço de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O thread associado com a execução do procedimento armazenado estendido é igual ao usado na conexão do cliente.  
  
    > [!IMPORTANT]  
    >  Antes de adicionar procedimentos armazenados estendidos ao servidor e conceder permissões de execução a outros usuários, o administrador do sistema deve examinar detalhadamente cada procedimento armazenado estendido para certificar-se de que ele não contém código nocivo ou mal-intencionado.  
  
-  
  
 Depois que a DLL de procedimento armazenado estendido é carregada, a DLL permanece carregada no espaço de endereço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servidor até que o seja interrompido ou o administrador descarregue explicitamente a DLL usando DBCC *dll_name* (gratuito).  
  
 O procedimento armazenado estendido pode ser executado a partir do [!INCLUDE[tsql](../../includes/tsql-md.md)] como um procedimento armazenado usando a instrução EXECUTE:  
  
```  
EXECUTE @retval = xp_extendedProcName @param1, @param2 OUTPUT  
```  
  
## <a name="parameters"></a>Parâmetros  
 \@ *retval*  
 É um valor de retorno.  
  
 \@*param1*  
 É um parâmetro de entrada.  
  
 \@*param2*  
 É um parâmetro de entrada/saída.  
  
> [!CAUTION]  
>  Os procedimentos armazenados estendidos oferecem aprimoramentos de desempenho e estendem a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, como a DLL do procedimento armazenado estendido e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compartilham o mesmo espaço de endereço, um procedimento problemático pode afetar adversamente o funcionamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Embora as exceções lançadas pela DLL do procedimento armazenado estendido sejam tratadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível danificar áreas de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como precaução de segurança, apenas os administradores do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem adicionar procedimentos armazenados estendidos ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses procedimentos devem ser extensivamente testados antes ser instalados.  
  
## <a name="see-also"></a>Consulte Também  
 [Programando procedimentos armazenados estendidos](../../relational-databases/extended-stored-procedures-programming/database-engine-extended-stored-procedures-programming.md)   
 [Consulta de procedimentos armazenados estendidos no SQL Server](../../relational-databases/extended-stored-procedures-programming/querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
