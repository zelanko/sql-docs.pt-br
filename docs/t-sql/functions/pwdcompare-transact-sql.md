---
title: PWDCOMPARE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PWDCOMPARE
- PWDCOMPARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sa account
- passwords [SQL Server], blank
- PWDCOMPARE function [Transact-SQL]
ms.assetid: 5f84ff9e-c1ec-46aa-8501-50f854ebcc3a
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 65d4e1418dcf8f74cd994034097bc3ae0495e910
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65943278"
---
# <a name="pwdcompare-transact-sql"></a>PWDCOMPARE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Obtém o valor hash de uma senha e compara-o com o de uma senha existente. PWDCOMPARE pode ser usado para procurar senhas de logon em branco do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou senhas fracas comuns.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PWDCOMPARE ( 'clear_text_password'  
   , password_hash   
   [ , version ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *clear_text_password* **'**  
 É a senha não criptografada. *clear_text_password* é **sysname** (**nvarchar(128)**).  
  
 *password_hash*  
 É o hash de criptografia de uma senha. *password_hash* é **varbinary(128)**.  
  
 *version*  
 Parâmetro obsoleto que poderá ser definido como 1 se *password_hash* representar um valor de um logon anterior a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] que foi migrado para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior, mas nunca convertido no sistema [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. *version* é **int**.  
  
> [!CAUTION]  
>  Esse parâmetro é fornecido para fins de compatibilidade com versões anteriores, mas é ignorado, pois os blobs de hash de senha agora contêm suas próprias descrições de versão. [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
 Retorna 1 se o hash da *clear_text_password* corresponde ao parâmetro *password_hash*, e 0 se ele não existe.  
  
## <a name="remarks"></a>Remarks  
 A função PWDCOMPARE não é uma ameaça contra a força de hashes de senha porque o mesmo teste pode ser executado por meio de tentativa de logon usando a senha fornecida como o primeiro parâmetro.  
  
 Não é possível usar **PWDCOMPARE** com as senhas de usuários de bancos de dados independentes. Não há banco de dados independente equivalente.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [PWDENCRYPT &#40;Transact-SQL&#41;](../../t-sql/functions/pwdencrypt-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
