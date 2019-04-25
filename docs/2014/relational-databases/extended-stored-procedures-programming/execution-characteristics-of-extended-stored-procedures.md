---
title: Características de execução de procedimentos armazenados estendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], executing
- executing extended stored procedures [SQL Server]
ms.assetid: 6fe1f7e8-cc02-49df-8a2a-d47a96ec3567
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d21f002ca6b7ea185df2e01f66abf0e1ef5cfd1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62512208"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>Características de execução de procedimentos armazenados estendidos
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 A execução de um procedimento armazenado estendido tem as seguintes características:  
  
-   A função de procedimento armazenado estendido é executada no contexto de segurança de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   A função de procedimento armazenado estendido é executada no espaço de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O thread associado com a execução do procedimento armazenado estendido é igual ao usado na conexão do cliente.  
  
    > [!IMPORTANT]  
    >  Antes de adicionar procedimentos armazenados estendidos ao servidor e conceder permissões de execução a outros usuários, o administrador do sistema deve examinar detalhadamente cada procedimento armazenado estendido para certificar-se de que ele não contém código nocivo ou mal-intencionado.  
  
-  
  
 Depois que o procedimento armazenado estendido DLL é carregada, a DLL permanece carregada no espaço de endereço do servidor de até [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for interrompido ou o administrador a Descarregue explicitamente o DLL usando DBCC *DLL_name* (gratuito).  
  
 O procedimento armazenado estendido pode ser executado a partir do [!INCLUDE[tsql](../../includes/tsql-md.md)] como um procedimento armazenado usando a instrução EXECUTE:  
  
```  
EXECUTE @retval = xp_extendedProcName @param1, @param2 OUTPUT  
```  
  
## <a name="parameters"></a>Parâmetros  
 \@ *retval*  
 É um valor de retorno.  
  
 \@ *param1*  
 É um parâmetro de entrada.  
  
 \@ *param2*  
 É um parâmetro de entrada/saída.  
  
> [!CAUTION]  
>  Os procedimentos armazenados estendidos oferecem aprimoramentos de desempenho e estendem a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, como a DLL do procedimento armazenado estendido e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compartilham o mesmo espaço de endereço, um procedimento problemático pode afetar adversamente o funcionamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Embora as exceções lançadas pela DLL do procedimento armazenado estendido sejam tratadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível danificar áreas de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como precaução de segurança, apenas os administradores do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem adicionar procedimentos armazenados estendidos ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses procedimentos devem ser extensivamente testados antes ser instalados.  
  
## <a name="see-also"></a>Consulte também  
 [Programando procedimentos armazenados estendidos](database-engine-extended-stored-procedures-programming.md)   
 [Consulta de procedimentos armazenados estendidos no SQL Server](querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
