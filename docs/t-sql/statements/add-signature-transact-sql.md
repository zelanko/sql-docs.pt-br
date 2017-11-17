---
title: Adicionar assinatura (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ADD SIGNATURE
- ADD_SIGNATURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ADD SIGNATURE statement
- adding digital signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 64d8b682-6ec1-4e5b-8aee-3ba11e72d21f
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d171b17749cbe5333a11405eb48ac4b9293151d6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="add-signature-transact-sql"></a>ADD SIGNATURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Adiciona uma assinatura digital a um procedimento armazenado, função, assembly ou gatilho. Além disso, adiciona uma referenda a um procedimento armazenado, uma função, um assembly ou um gatilho.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ADD [ COUNTER ] SIGNATURE TO module_class::module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | CERTIFICATE cert_name [ WITH PASSWORD = 'password' ]  
    | CERTIFICATE cert_name WITH SIGNATURE = signed_blob   
    | ASYMMETRIC KEY Asym_Key_Name  
    | ASYMMETRIC KEY Asym_Key_Name [ WITH PASSWORD = 'password'.]  
    | ASYMMETRIC KEY Asym_Key_Name WITH SIGNATURE = signed_blob  
```  
  
## <a name="arguments"></a>Argumentos  
 *module_class*  
 É a classe do módulo ao qual a assinatura é adicionada. O padrão para módulos de escopo de esquema é OBJECT.  
  
 *nome_de_módulo*  
 É o nome de um procedimento armazenado, função, assembly ou gatilho a serem assinados ou referendados.  
  
 CERTIFICADO *cert_name*  
 É o nome de um certificado com o qual assinar ou referendar o procedimento armazenado, função, assembly ou gatilho.  
  
 COM a senha ='*senha*'  
 É a senha necessária para descriptografar a chave privada do certificado ou chave assimétrica. Esta cláusula só será necessária se a chave privada não for protegida pela chave mestra de banco de dados.  
  
 ASSINATURA =*signed_blob*  
 Especifica o BLOB (objeto binário grande) assinado do módulo. Esta cláusula será útil se você quiser enviar um módulo sem enviar a chave privada. Ao usar esta cláusula, somente o módulo, a assinatura e a chave pública são necessários para adicionar o objeto binário grande a um banco de dados. *signed_blob* é o próprio blob em formato hexadecimal.  
  
 CHAVE ASSIMÉTRICA *Asym_Key_Name*  
 É o nome de uma chave assimétrica com a qual assinar ou referendar o procedimento armazenado, função, assembly ou gatilho.  
  
## <a name="remarks"></a>Comentários  
 O módulo que é assinado ou referendado e o certificado ou chave assimétrica usados para assiná-lo já devem existir. Todo caractere no módulo é incluído no cálculo de assinatura. Isso inclui retornos de carro à esquerda e alimentação de linha.  
  
 Um módulo pode ser assinado e referendado por qualquer número de certificados e chaves assimétricas.  
  
 A assinatura de um módulo é descartada quando o módulo é alterado.  
  
 Se um módulo tiver uma cláusula EXECUTE AS, a SID (ID de segurança) do principal também será incluída como parte do processo de assinatura.  
  
> [!CAUTION]  
>  A assinatura de módulo só deve ser usada para conceder permissões, e nunca para negar ou revogar permissões.  
  
 Funções embutidas com valor de tabela não podem ser assinadas.  
  
 As informações sobre assinaturas são visíveis na exibição do catálogo sys.crypt_properties.  
  
> [!WARNING]  
>  Ao recriar um procedimento para a assinatura, todas as instruções no lote original devem corresponder ao lote de recriação. Se qualquer parte do lote for diferente, mesmo em espaços ou comentários, a assinatura resultante será diferente.  
  
## <a name="countersignatures"></a>Referendas  
 Ao executar um módulo assinado, as assinaturas serão acrescentadas temporariamente ao token do SQL, mas as assinaturas serão perdidas se o módulo executar outro módulo ou se o módulo finalizar a execução. Uma referenda é uma forma especial de assinatura. Por si só, uma referenda não concede permissões, porém, permite que as assinaturas feitas pelo mesmo certificado ou chave assimétrica sejam mantidas enquanto durar a chamada feita ao objeto referendado.  
  
 Por exemplo, presuma que a usuária Alice chame o procedimento ProcSelectT1ForAlice, que chama o procedimento procSelectT1, que seleciona da tabela T1. Alice tem permissão de EXECUTE em ProcSelectT1ForAlice e procSelectT1, mas ela não tem permissão de SELECT em T1 e nenhum encadeamento de propriedade é envolvido nesta cadeia inteira. Alice não pode acessar a tabela T1 diretamente ou pelo uso de ProcSelectT1ForAlice e procSelectT1. Como desejamos que Alice use sempre ProcSelectT1ForAlice para acesso, nós não desejamos conceder permissão para ela executar procSelectT1. Como podemos fazer isso?  
  
-   Se nós assinarmos procSelectT1, de modo que procSelectT1 acesse T1, Alice poderá invocar procSelectT1 diretamente e não terá que chamar ProcSelectT1ForAlice.  
  
-   Poderíamos negar permissão de EXECUTE em procSelectT1 para Alice, porém Alice também não poderia chamar procSelectT1 através de ProcSelectT1ForAlice.  
  
-   Assinar ProcSelectT1ForAlice não funcionaria por si só, porque a assinatura seria perdida na chamada para procSelectT1.  
  
No entanto, ao assinar procSelectT1 com o mesmo certificado usado para assinar ProcSelectT1ForAlice, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manterá a assinatura na cadeia de chamada e permitirá acesso a T1. Se Alice tentar chamar procSelectT1 diretamente, ela não poderá acessar T1, porque a referenda não concede nenhum direito. O exemplo C abaixo mostra o [!INCLUDE[tsql](../../includes/tsql-md.md)] para este exemplo.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER no objeto e a permissão CONTROL no certificado ou chave assimétrica. Se uma chave privada associada estiver protegida por uma senha, o usuário também precisará ter a senha.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-signing-a-stored-procedure-by-using-a-certificate"></a>A. Assinando um procedimento armazenado com um certificado  
 O exemplo a seguir assina o procedimento armazenado `HumanResources.uspUpdateEmployeeLogin` com o certificado `HumanResourcesDP`.  
  
```  
USE AdventureWorks2012;  
ADD SIGNATURE TO HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
### <a name="b-signing-a-stored-procedure-by-using-a-signed-blob"></a>B. Assinando um procedimento armazenado com um BLOB assinado  
 O exemplo a seguir cria um novo banco de dados e cria um certificado para uso no exemplo. O exemplo cria e assina um procedimento armazenado simples e recupera o BLOB de assinatura de `sys.crypt_properties`. A assinatura é então descartada e adicionada novamente. O exemplo assina o procedimento usando a sintaxe WITH SIGNATURE.  
  
```  
CREATE DATABASE TestSignature ;  
GO  
USE TestSignature ;  
GO  
-- Create a CERTIFICATE to sign the procedure.  
CREATE CERTIFICATE cert_signature_demo   
    ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
    WITH SUBJECT = 'ADD SIGNATURE demo';  
GO  
-- Create a simple procedure.  
CREATE PROC [sp_signature_demo]  
AS  
    PRINT 'This is the content of the procedure.' ;  
GO  
-- Sign the procedure.  
ADD SIGNATURE TO [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo]   
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y' ;  
GO  
-- Get the signature binary BLOB for the sp_signature_demo procedure.  
SELECT cp.crypt_property  
    FROM sys.crypt_properties AS cp  
    JOIN sys.certificates AS cer  
        ON cp.thumbprint = cer.thumbprint  
    WHERE cer.name = 'cert_signature_demo' ;  
GO  
```  
  
 A assinatura `crypt_property` que é retornada por essa instrução será diferente a cada vez que você criar um procedimento. Anote o resultado para uso posteriormente neste exemplo. Neste exemplo, o resultado demonstrado é: `0x831F5530C86CC8ED606E5BC2720DA835351E46219A6D5DE9CE546297B88AEF3B6A7051891AF3EE7A68EAB37CD8380988B4C3F7469C8EABDD9579A2A5C507A4482905C2F24024FFB2F9BD7A953DD5E98470C4AA90CE83237739BB5FAE7BAC796E7710BDE291B03C43582F6F2D3B381F2102EEF8407731E01A51E24D808D54B373`.  
  
```  
-- Drop the signature so that it can be signed again.  
DROP SIGNATURE FROM [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo];  
GO  
-- Add the signature. Use the signature BLOB obtained earlier.  
ADD SIGNATURE TO [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo]  
    WITH SIGNATURE = 0x831F5530C86CC8ED606E5BC2720DA835351E46219A6D5DE9CE546297B88AEF3B6A7051891AF3EE7A68EAB37CD8380988B4C3F7469C8EABDD9579A2A5C507A4482905C2F24024FFB2F9BD7A953DD5E98470C4AA90CE83237739BB5FAE7BAC796E7710BDE291B03C43582F6F2D3B381F2102EEF8407731E01A51E24D808D54B373 ;  
GO  
```  
  
### <a name="c-accessing-a-procedure-using-a-countersignature"></a>C. Acessando um procedimento usando uma referenda  
 O exemplo a seguir mostra como a referenda pode ajudar a controlar o acesso a um objeto.  
  
```  
-- Create tesT1 database  
CREATE DATABASE testDB;  
GO  
USE testDB;  
GO  
-- Create table T1  
CREATE TABLE T1 (c varchar(11));  
INSERT INTO T1 VALUES ('This is T1.');  
  
-- Create a TestUser user to own table T1  
CREATE USER TestUser WITHOUT LOGIN;  
ALTER AUTHORIZATION ON T1 TO TestUser;  
  
-- Create a certificate for signing  
CREATE CERTIFICATE csSelectT  
  ENCRYPTION BY PASSWORD = 'SimplePwd01'  
  WITH SUBJECT = 'Certificate used to grant SELECT on T1';  
CREATE USER ucsSelectT1 FROM CERTIFICATE csSelectT;  
GRANT SELECT ON T1 TO ucsSelectT1;  
  
-- Create a principal with low privileges  
CREATE LOGIN Alice WITH PASSWORD = 'SimplePwd01';  
CREATE USER Alice;  
  
-- Verify Alice cannoT1 access T1;  
EXECUTE AS LOGIN = 'Alice';  
    SELECT * FROM T1;  
REVERT;  
  
-- Create a procedure that directly accesses T1  
CREATE PROCEDURE procSelectT1 AS  
BEGIN  
    PRINT 'Now selecting from T1...';  
    SELECT * FROM T1;  
END;  
GO  
GRANT EXECUTE ON procSelectT1 to public;  
  
-- Create special procedure for accessing T1  
CREATE PROCEDURE  procSelectT1ForAlice AS  
BEGIN  
   IF USER_ID() <> USER_ID('Alice')  
    BEGIN  
        PRINT 'Only Alice can use this.';  
        RETURN  
    END  
   EXEC procSelectT1;  
END;  
GO;  
GRANT EXECUTE ON procSelectT1ForAlice TO PUBLIC;  
  
-- Verify procedure works for a sysadmin user  
EXEC procSelectT1ForAlice;  
  
-- Alice still can't use the procedure yet  
EXECUTE AS LOGIN = 'Alice';  
    EXEC procSelectT1ForAlice;  
REVERT;  
  
-- Sign procedure to grant it SELECT permission  
ADD SIGNATURE TO procSelectT1ForAlice BY CERTIFICATE csSelectT   
WITH PASSWORD = 'SimplePwd01';  
  
-- Counter sign proc_select_t, to make this work  
ADD COUNTER SIGNATURE TO procSelectT1 BY CERTIFICATE csSelectT   
WITH PASSWORD = 'SimplePwd01';  
  
-- Now the proc works.   
-- Note that calling procSelectT1 directly still doesn't work  
EXECUTE AS LOGIN = 'Alice';  
    EXEC procSelectT1ForAlice;  
    EXEC procSelectT1;  
REVERT;  
  
-- Cleanup  
USE master;  
GO  
DROP DATABASE testDB;  
DROP LOGIN Alice;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [crypt_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [Remover assinatura &#40; Transact-SQL &#41;](../../t-sql/statements/drop-signature-transact-sql.md)  
  
  

