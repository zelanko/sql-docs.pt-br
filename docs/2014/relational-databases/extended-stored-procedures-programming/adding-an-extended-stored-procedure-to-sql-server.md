---
title: Adicionar um procedimento armazenado para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], adding
- adding extended stored procedures
- collations [SQL Server], extended stored procedures
ms.assetid: 10f1bb74-3b43-4efd-b7ab-7a85a8600a50
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b69f6ba2dd0fc6c5b3b2ce4f93e70239d8868007
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020255"
---
# <a name="adding-an-extended-stored-procedure-to-sql-server"></a>Adicionando um procedimento armazenado estendido ao SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 Uma DLL que contém funções de procedimento armazenado estendido funciona como uma extensão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar a DLL, copie o arquivo para um diretório, como aquele que contém o padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivos DLL (C:\Program Files\Microsoft SQL Server\MSSQL12.0. *x*\MSSQL\Binn por padrão).  
  
 Depois que uma DLL de procedimento armazenado estendido for copiada no servidor, um administrador do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve registrar no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todas as funções de procedimento armazenado estendido na DLL. Isso é feito por meio do uso do procedimento armazenado de sistema sp_addextendedproc.  
  
> [!IMPORTANT]  
>  O administrador do sistema deve examinar inteiramente um procedimento armazenado estendido para garantir que ele não contenha código perigoso ou mal-intencionado, antes de adicioná-lo ao servidor e conceder permissões de execução a outros usuários.  Valide todas as entradas de usuário. Não concatene uma entrada de usuário antes de validá-la. Nunca execute um comando construído por uma entrada de usuário inválida.  
  
 O primeiro parâmetro de sp_addextendedproc especifica o nome da função e o segundo, o nome da DLL em que reside essa função. É recomendável especificar o caminho completo da DLL.  
  
> [!IMPORTANT]  
>  As DLLs existentes que não foram registradas com um caminho completo não funcionarão depois da atualização para o SQL Server 2005 ou posterior. Para corrigir o problema, use sp_dropextendedproc para cancelar o registro da DLL e registrá-la novamente com sp_addextendedproc, especificando o caminho completo.  
  
 O nome da função especificada em `sp_addextendedproc` deve ser exatamente igual, inclusive maiúsculas e minúsculas, ao nome da função na DLL. Por exemplo, esse comando registra uma função `xp_hello,`, localizada em uma dll denominada `xp_hello.dll`, como um procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_addextendedproc 'xp_hello', 'c:\Program Files\Microsoft SQL Server\MSSQL12.0.MSSQLSERVER\MSSQL\Binn\xp_hello.dll';  
```  
  
 Se o nome da função especificado em `sp_addextendedproc` não corresponder exatamente ao nome da função na DLL, o novo nome será registrado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas o nome não poderá ser usado. Por exemplo, embora `xp_Hello` é registrado como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimento armazenado localizado em `xp_hello.dll`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não será capaz de encontrar a função na DLL se você usar `xp_Hello` para chamar a função mais tarde.  
  
```  
--Register the function (xp_hello) with an initial upper case  
sp_addextendedproc 'xp_Hello', 'c:\xp_hello.dll';  
  
--Use the newly registered name to call the function  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
--This is the error message  
Server: Msg 17750, Level 16, State 1, Procedure xp_Hello, Line 1  
Could not load the DLL xp_hello.dll, or one of the DLLs it references. Reason: 127(The specified procedure could not be found.).  
```  
  
 Se o nome da função especificado em `sp_addextendedproc` corresponder exatamente ao nome da função na DLL, e o agrupamento da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferenciar maiúsculas e minúsculas, o usuário poderá chamar o procedimento armazenado estendido usando qualquer combinação de letras maiúsculas e minúsculas no nome.  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will succeed in calling xp_hello  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HelLO @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
```  
  
 Quando o agrupamento da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferenciar maiúsculas de minúsculas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá chamar o procedimento armazenado estendido – mesmo que tenha sido registrado exatamente com o mesmo nome e agrupamento da função na DLL –, se o procedimento for chamado com um uso de maiúsculas e minúsculas diferente.  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will result in an error  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
  
--This is the error  
Server: Msg 2812, Level 16, State 62, Line 1  
```  
  
 Não é necessário parar e reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [sp_addextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
