---
title: ALTER ENDPOINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER ENDPOINT
- ALTER_ENDPOINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER ENDPOINT statement
- modifying endpoints
- endpoints [SQL Server], modifying
ms.assetid: 70f35566-30cf-47c6-8394-dfe5d71629d3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0b07cc17344e27d82155ceaae8e55494deb0bd57
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065675"
---
# <a name="alter-endpoint-transact-sql"></a>ALTER ENDPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Habilita a modificação de um ponto de extremidade existente das seguintes formas:  
  
-   Adicionando um novo método a um ponto de extremidade existente.  
  
-   Modificando ou descartando um método existente do ponto de extremidade.  
  
-   Alterando as propriedades de um ponto de extremidade.  
  
> [!NOTE]  
>  Este tópico descreve a sintaxe e os argumentos que são específicos para ALTER ENDPOINT. Para obter descrições dos argumentos que são comuns a CREATE ENDPOINT e a ALTER ENDPOINT, confira [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
 Serviços Web XML nativos (pontos de extremidade SOAP/HTTP) são removidos a partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER ENDPOINT endPointName [ AUTHORIZATION login ]  
[ STATE = { STARTED | STOPPED | DISABLED } ]  
[ AS { TCP } ( <protocol_specific_items> ) ]  
[ FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING } (  
   <language_specific_items>  
        ) ]  
  
<AS TCP_protocol_specific_arguments> ::=  
AS TCP (  
  LISTENER_PORT = listenerPort  
  [ [ , ] LISTENER_IP = ALL | ( 4-part-ip ) | ( "ip_address_v6" ) ]  
)  
<FOR SERVICE_BROKER_language_specific_arguments> ::=  
FOR SERVICE_BROKER (  
   [ AUTHENTICATION = {   
      WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]  
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ , ENCRYPTION = { DISABLED   
       |   
         {{SUPPORTED | REQUIRED }   
       [ ALGORITHM { RC4 | AES | AES RC4 | RC4 AES } ] }   
   ]  
  
  [ , MESSAGE_FORWARDING = {ENABLED | DISABLED} ]  
  [ , MESSAGE_FORWARD_SIZE = forwardSize  
)  
  
<FOR DATABASE_MIRRORING_language_specific_arguments> ::=  
FOR DATABASE_MIRRORING (  
   [ AUTHENTICATION = {   
      WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]  
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ , ENCRYPTION = { DISABLED   
       |   
         {{SUPPORTED | REQUIRED }   
       [ ALGORITHM { RC4 | AES | AES RC4 | RC4 AES } ] }   
    ]   
   [ , ] ROLE = { WITNESS | PARTNER | ALL }  
)  
  
```  
  
## <a name="arguments"></a>Argumentos  
  
> [!NOTE]  
>  Os argumentos a seguir são específicos para ALTER ENDPOINT. Para obter descrições dos argumentos restantes, confira [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
 **AS** { **TCP** }  
 Não é possível alterar o protocolo de transporte com **ALTER ENDPOINT**.  
  
 **AUTHORIZATION** *login*  
 A opção **AUTHORIZATION** não está disponível em **ALTER ENDPOINT**. A propriedade só pode ser atribuída quando o ponto de extremidade é criado.  
  
 **FOR** { **TSQL** | **SERVICE_BROKER** | **DATABASE_MIRRORING** }  
 Não é possível alterar o tipo de carga com **ALTER ENDPOINT**.  
  
## <a name="remarks"></a>Remarks  
 Quando você usar ALTER ENDPOINT, especifique somente os parâmetros que deseja atualizar. Todas as propriedades de um ponto de extremidade existente permanecem as mesmas, a não ser que você as altere explicitamente.  
  
 Não podem ser executadas instruções ENDPOINT DDL em uma transação de usuário.  
  
 Para obter informações de como escolher um algoritmo de criptografia a ser usado com um ponto de extremidade, confira [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md).  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e em versões posteriores, o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
>   
>  RC4 é um algoritmo relativamente fraco e AES é um algoritmo relativamente forte. Mas AES é consideravelmente mais lento do que RC4. Se segurança for uma prioridade mais alta para você do que a velocidade, recomendamos que use AES.  
  
## <a name="permissions"></a>Permissões  
 O usuário precisa ser membro da função de servidor fixa **sysadmin**, proprietário do ponto de extremidade ou ter recebido a permissão ALTER ANY ENDPOINT.  
  
 Para alterar a propriedade de um ponto de extremidade existente, você deve usar a instrução ALTER AUTHORIZATION. Para obter mais informações, confira [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 Para obter mais informações, consulte [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [DROP ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
