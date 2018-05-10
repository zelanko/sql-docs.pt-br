---
title: CREATE CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CERTIFICATE
- CREATE_CERTIFICATE_TSQL
- sql13.swb.createcertificate.f1
- CERTIFICATE_TSQL
- CREATE CERTIFICATE
- sql13.swb.certificateproperties.f1
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- certificates [SQL Server], adding
- certificates [SQL Server]
- adding certificates
- cryptography [SQL Server], certificates
- CREATE CERTIFICATE statement
ms.assetid: a4274b2b-4cb0-446a-a956-1c8e6587515d
caps.latest.revision: 74
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: abd46332127b1b15280df0ec5bab5655da5a148a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-certificate-transact-sql"></a>CREATE CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Adiciona um certificado a um banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 Este recurso é incompatível com a exportação de banco de dados usando a DACFx (estrutura de aplicativo da camada de dados). Você deve remover todos os certificados antes de exportar.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE CERTIFICATE certificate_name [ AUTHORIZATION user_name ]   
    { FROM <existing_keys> | <generate_new_keys> }  
    [ ACTIVE FOR BEGIN_DIALOG =  { ON | OFF } ]  
  
<existing_keys> ::=   
    ASSEMBLY assembly_name  
    | {   
        [ EXECUTABLE ] FILE = 'path_to_file'  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]   
      }  
    | {   
        BINARY = asn_encoded_certificate  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]  
      }  
<generate_new_keys> ::=   
    [ ENCRYPTION BY PASSWORD = 'password' ]   
    WITH SUBJECT = 'certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<private_key_options> ::=  
      {   
        FILE = 'path_to_private_key'  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
    |  
      {   
        BINARY = private_key_bits  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
  
<date_options> ::=  
    START_DATE = 'datetime' | EXPIRY_DATE = 'datetime'  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CERTIFICATE certificate_name   
    { <generate_new_keys> | FROM <existing_keys> }  
    [ ; ]  
  
<generate_new_keys> ::=   
    WITH SUBJECT ='certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<existing_keys> ::=   
    {   
      FILE ='path_to_file'  
      WITH PRIVATE KEY   
         (   
           FILE ='path_to_private_key'  
           , DECRYPTION BY PASSWORD ='password'   
         )  
    }  
  
<date_options> ::=  
    START_DATE ='datetime' | EXPIRY_DATE ='datetime'  
```  
  
## <a name="arguments"></a>Argumentos  
 *certificate_name*  
 É o nome do certificado no banco de dados.  
  
 AUTHORIZATION *user_name*  
 É o nome do usuário que é o proprietário desse certificado.  
  
 ASSEMBLY *assembly_name*  
 Especifica um assembly assinado que já foi carregado no banco de dados.  
  
 [ EXECUTABLE ] FILE ='*path_to_file*'  
 Especifica o caminho completo, incluindo nome de arquivo, para um arquivo codificado por DER que contém o certificado. Se a opção EXECUTABLE for usada, o arquivo será um DLL que assinado pelo certificado. *path_to_file* pode ser um caminho local ou um caminho UNC para um local de rede. O arquivo é acessado no contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa conta deve ter as permissões de sistema de arquivos necessárias.  
  
 WITH PRIVATE KEY  
 Especifica que a chave privada do certificado foi carregada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa cláusula é válida apenas quando o certificado é criado a partir de um arquivo. Para carregar a chave privada de um assembly, use [ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md).  
  
 FILE ='*path_to_private_key*'  
 Especifica o caminho completo, incluindo o nome de arquivo, até a chave privada. *path_to_private_key* pode ser um caminho local ou um caminho UNC para um local de rede. O arquivo é acessado no contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa conta deve ter as permissões de sistema de arquivos necessárias.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 asn_encoded_certificate  
 Bits de certificado codificado ASN especificados como uma constante binária.  
  
 BINARY =*private_key_bits*  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Bits de chave privada especificados como constante binária. Estes bits podem estar no formato criptografado. Se criptografado, o usuário deve fornecer uma senha de descriptografia. Verificações de diretiva de senha não são executadas nesta senha. Os bits de chave privada devem estar em um formato de arquivo PVK.  
  
 DECRYPTION BY PASSWORD ='*key_password*'  
 Especifica a senha necessária para descriptografar uma chave privada recuperada de um arquivo. Essa cláusula será opcional se a chave privada for protegida por uma senha nula. Não é recomendável salvar uma chave privada em um arquivo sem proteção de senha. Se uma senha for necessária, mas nenhuma senha for especificada, a instrução falhará.  
  
 ENCRYPTION BY PASSWORD ='*password*'  
 Especifica a senha usada para criptografar a chave privada. Use esta opção somente se quiser criptografar o certificado com uma senha. Se essa cláusula for omitida, a chave privada será criptografada usando a chave mestra do banco de dados. A *password* deve atender aos requisitos da política de senha do Windows do computador que executa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Password Policy](../../relational-databases/security/password-policy.md).  
  
 SUBJECT ='*certificate_subject_name*'  
 O termo *subject* refere-se a um campo nos metadados do certificado conforme definido pelo padrão X.509. O assunto não deve ter mais do que 64 caracteres, e esse limite é aplicado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Linux. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Windows, a entidade pode ter até 128 caracteres. Os assuntos que excederem 128 caracteres serão truncados quando forem armazenados no catálogo, mas o BLOB (objeto binário grande) que contém o certificado manterá o nome completo do assunto.  
  
 START_DATE ='*datetime*'  
 É a data na qual o certificado se torna válido. Se não especificada, START_DATE será definida com a data atual. START_DATE está na hora UTC e pode ser especificado em qualquer formato que possa ser convertido em uma data e hora.  
  
 EXPIRY_DATE ='*datetime*'  
 É a data na qual o certificado expira. Se não for especificada, EXPIRY_DATE será definida com uma data um ano após START_DATE. EXPIRY_DATE está na hora UTC e pode ser especificado em qualquer formato que possa ser convertido em uma data e hora. O Service Broker [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica a data de expiração. No entanto, a expiração não é imposta quando o certificado é usado para criptografia.  
  
 ACTIVE FOR BEGIN_DIALOG = { **ON** | OFF }  
 Disponibiliza o certificado para o iniciador de uma conversa de caixa de diálogo do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. O valor padrão é ON.  
  
## <a name="remarks"></a>Remarks  
 Um certificado é um protegível em nível de banco de dados que segue o padrão X.509 e oferece suporte aos campos X.509 V1. CREATE CERTIFICATE pode carregar um certificado de um arquivo ou assembly. Essa instrução também pode gerar um par de chaves e criar um certificado autoassinado.  
  
 A Chave Privada deve ser \<= 2.500 bytes em formato criptografado. Chaves privadas geradas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm 1.024 bits de extensão até [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e 2.048 bits de extensão começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. As chaves particulares importadas de uma origem externa têm um comprimento mínimo de 384 bits e máximo de 4.096 bits. O comprimento de uma chave privada importada deve ser um número inteiro múltiplo de 64 bits. Certificados usados para TDE são limitados a um tamanho de chave privado de 3456 bits.  
  
 Todo o Número de Série do certificado é armazenado, mas somente os primeiros 16 bytes aparecem na exibição do catálogo sys.certificates.  
  
 Todo o campo do Emissor do certificado é armazenado, mas somente os primeiros bytes 884 na exibição de catálogo sys.certificates.  
  
 A chave privada deve corresponder à chave pública especificada por *certificate_name*.  
  
 Ao criar um certificado de um contêiner, o carregamento da chave privada é opcional. Mas quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um certificado autoassinado, a chave privada sempre é criada. Por padrão, a chave privada é criptografada usando a chave mestra do banco de dados. Se a chave mestra do banco de dados não existir e nenhuma senha for especificada, a instrução falhará.  
  
 A opção ENCRYPTION BY PASSWORD não será necessária quando a chave privada for criptografada com a chave mestra do banco de dados. Use essa opção somente quando a chave privada for criptografada com uma senha. Se nenhuma senha for especificada, a chave privada do certificado será criptografada com a chave mestra do banco de dados. Omitir essa cláusula causará um erro se a chave mestra do banco de dados não puder ser aberta.  
  
 Não é necessário especificar uma senha de descriptografia quando a chave privada for criptografada com a chave mestra do banco de dados.  
  
> [!NOTE]  
>  As funções internas para criptografia e assinatura não verificam as datas de expiração de certificados. Os usuários dessas funções devem decidir quando verificar expiração de certificado.  
  
 Uma descrição binária de um certificado pode ser criada usando as funções [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md) e [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md). Para obter um exemplo que use **CERTPRIVATEKEY** e **CERTENCODED** para copiar um certificado para outro banco de dados, veja o exemplo B no tópico [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE CERTIFICATE no banco de dados. Somente logons do Windows, logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e funções de aplicativo podem ter certificados. Grupos e funções não podem possuir certificados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-self-signed-certificate"></a>A. Criando um certificado autoassinado  
 O exemplo a seguir cria um certificado denominado `Shipping04`. A chave privada desse certificado é protegida usando uma senha.  
  
```  
CREATE CERTIFICATE Shipping04   
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
   WITH SUBJECT = 'Sammamish Shipping Records',   
   EXPIRY_DATE = '20201031';  
GO  
```  
  
### <a name="b-creating-a-certificate-from-a-file"></a>B. Criando um certificado de um arquivo  
 O exemplo a seguir cria um certificado no banco de dados, carregando o par de chaves a partir de arquivos.  
  
```  
CREATE CERTIFICATE Shipping11   
    FROM FILE = 'c:\Shipping\Certs\Shipping11.cer'   
    WITH PRIVATE KEY (FILE = 'c:\Shipping\Certs\Shipping11.pvk',   
    DECRYPTION BY PASSWORD = 'sldkflk34et6gs%53#v00');  
GO   
```  
  
### <a name="c-creating-a-certificate-from-a-signed-executable-file"></a>C. Criando um certificado a partir de um arquivo executável assinado  
  
```  
CREATE CERTIFICATE Shipping19   
    FROM EXECUTABLE FILE = 'c:\Shipping\Certs\Shipping19.dll';  
GO  
```  
  
 Como alternativa, é possível criar um assembly a partir do arquivo `dll` e, em seguida, um certificado a partir do assembly.  
  
```  
CREATE ASSEMBLY Shipping19   
    FROM ' c:\Shipping\Certs\Shipping19.dll'   
    WITH PERMISSION_SET = SAFE;  
GO  
CREATE CERTIFICATE Shipping19 FROM ASSEMBLY Shipping19;  
GO  
```  
  
### <a name="d-creating-a-self-signed-certificate"></a>D. Criando um certificado autoassinado  
 O exemplo a seguir cria um certificado chamado `Shipping04` sem especificar uma senha de criptografia. Este exemplo pode ser usado com [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
```  
CREATE CERTIFICATE Shipping04   
   WITH SUBJECT = 'Sammamish Shipping Records';  
GO  
```  
  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)   
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
  
  


