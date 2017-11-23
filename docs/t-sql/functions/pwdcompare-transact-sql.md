---
title: PWDCOMPARE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PWDCOMPARE
- PWDCOMPARE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sa account
- passwords [SQL Server], blank
- PWDCOMPARE function [Transact-SQL]
ms.assetid: 5f84ff9e-c1ec-46aa-8501-50f854ebcc3a
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 23b90a0d4a09fc2eb754dc5f298883ef4469ade5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="pwdcompare-transact-sql"></a>PWDCOMPARE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Obtém o valor hash de uma senha e compara-o com o de uma senha existente. PWDCOMPARE pode ser usado para procurar senhas de logon em branco do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou senhas fracas comuns.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PWDCOMPARE ( 'clear_text_password'  
   , password_hash   
   [ , version ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *clear_text_password* **'**  
 É a senha não criptografada. *clear_text_password* é **sysname** (**nvarchar (128)**).  
  
 *password_hash*  
 É o hash de criptografia de uma senha. *password_hash* é **varbinary(128)**.  
  
 *Versão*  
 Parâmetro obsoleto que poderá ser definido como 1 se *password_hash* representa um valor de um logon anterior ao [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] que foi migrado para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior mas nunca convertido a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] sistema. *versão* é **int**.  
  
> [!CAUTION]  
>  Este parâmetro é fornecido para fins de compatibilidade, mas foi ignorado porque há blobs de hash de senha agora contêm suas próprias descrições de versão. [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
 Retornará 1 se o hash do *clear_text_password* corresponde a *password_hash* parâmetro e 0 se não existir.  
  
## <a name="remarks"></a>Comentários  
 A função PWDCOMPARE não é uma ameaça contra a força de hashes de senha porque o mesmo teste pode ser executado por meio de tentativa de logon usando a senha fornecida como o primeiro parâmetro.  
  
 **PWDCOMPARE** não pode ser usado com as senhas de usuários de banco de dados independente. Não há banco de dados independente equivalente.  
  
## <a name="permissions"></a>Permissões  
 PWDENCRYPT está disponível para o público.  
  
 A permissão CONTROL SERVER é necessária para examinar a coluna password_hash de sys.sql_logins.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-identifying-logins-that-have-no-passwords"></a>A. Identificando logons que não têm nenhuma senha  
 O exemplo a seguir identifica logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não têm nenhuma senha.  
  
```  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('', password_hash) = 1 ;  
```  
  
### <a name="b-searching-for-common-passwords"></a>B. Procurando senhas comuns  
 Para procurar senhas comuns que você deseja identificar e alterar, especifique a senha como o primeiro parâmetro. Por exemplo, execute a instrução a seguir para procurar uma senha especificada como `password`.  
  
```  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('password', password_hash) = 1 ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [PWDENCRYPT &#40; Transact-SQL &#41;](../../t-sql/functions/pwdencrypt-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
