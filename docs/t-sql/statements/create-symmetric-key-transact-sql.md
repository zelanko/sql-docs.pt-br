---
title: CREATE SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE SYMMETRIC KEY
- SYMMETRIC KEP
- CREATE_SYMMETRIC_KEY_TSQL
- SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SYMMETRIC KEY statement
- temporary symmetric keys [SQL Server]
- symmetric keys [SQL Server], creating
- symmetric keys [SQL Server]
ms.assetid: b5d23572-b79d-4cf1-9eef-d648fa3b1358
caps.latest.revision: 72
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0762a4dfb78edcad361cb8d51dd2c61579ccfef9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33072453"
---
# <a name="create-symmetric-key-transact-sql"></a>CREATE SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gera uma chave simétrica e especifica suas propriedades no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Este recurso é incompatível com a exportação de banco de dados usando a DACFx (estrutura de aplicativo da camada de dados). Você deve remover todas as chaves simétricas antes de exportar.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE SYMMETRIC KEY key_name   
    [ AUTHORIZATION owner_name ]  
    [ FROM PROVIDER provider_name ]  
    WITH 
      [
          <key_options> [ , ... n ]  
        | ENCRYPTION BY <encrypting_mechanism> [ , ... n ] 
      ]
  
<key_options> ::=  
      KEY_SOURCE = 'pass_phrase'  
    | ALGORITHM = <algorithm>  
    | IDENTITY_VALUE = 'identity_phrase'  
    | PROVIDER_KEY_NAME = 'key_name_in_provider'   
    | CREATION_DISPOSITION = {CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
    DES | TRIPLE_DES | TRIPLE_DES_3KEY | RC2 | RC4 | RC4_128  
    | DESX | AES_128 | AES_192 | AES_256   
  
<encrypting_mechanism> ::=  
      CERTIFICATE certificate_name   
    | PASSWORD = 'password'   
    | SYMMETRIC KEY symmetric_key_name   
    | ASYMMETRIC KEY asym_key_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *Key_name*  
 Especifica o nome exclusivo pelo qual a chave simétrica é conhecida no banco de dados. Os nomes de chaves temporárias devem começar com um símbolo de número (#). Por exemplo, **#temporaryKey900007**. Você não pode criar uma chave simétrica que tenha um nome que inicie com mais que um #. Não é possível criar uma chave simétrica temporária usando um provedor EKM.  
  
 AUTHORIZATION *owner_name*  
 Especifica o nome do usuário do banco de dados ou função de aplicativo que possuirá essa chave.  
  
 FROM PROVIDER *provider_name*  
 Especifica um nome e provedor de gerenciamento extensível de chaves (EKM). A chave não é exportada do dispositivo de EKM. O provedor deve ser definido primeiro com o uso da instrução CREATE PROVIDER. Para obter mais informações sobre como criar provedores de chave externa, veja [Gerenciamento extensível de chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 KEY_SOURCE **='***pass_phrase***'**  
 Especifica uma frase secreta da qual a chave deve derivar.  
  
 IDENTITY_VALUE **='***identity_phrase***'**  
 Especifica uma frase de identidade a partir da qual deve ser gerado um GUID para marcar dados criptografados com uma chave temporária.  
  
 PROVIDER_KEY_NAME **='***key_name_in_provider***'**  
 Especifica o nome mencionado no provedor de Gerenciamento Extensível de Chaves.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 CREATION_DISPOSITION **=** CREATE_NEW  
 Cria uma chave nova no dispositivo de Gerenciamento Extensível de Chaves.  Se já existir uma chave no dispositivo, a instrução falhará com erro.  
  
 CREATION_DISPOSITION **=** OPEN_EXISTING  
 Mapeia uma chave simétrica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma chave de gerenciamento extensível de chaves existente. Se CREATION_DISPOSITION = OPEN_EXISTING não for fornecido, isso será padronizado como CREATE_NEW.  
  
 *certificate_name*  
 Especifica o nome do certificado que será usado para criptografar a chave simétrica. O certificado já deve existir no banco de dados.  
  
 **'** *password* **'**  
 Especifica uma senha da qual derivar uma chave TRIPLE_DES para proteger a chave simétrica. A *password* deve atender aos requisitos da política de senha do Windows do computador que executa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sempre use senhas fortes.  
  
 *symmetric_key_name*  
 Especifica uma chave simétrica usada para criptografar a chave que está sendo criada. A chave especificada já deve existir no banco de dados e deve estar aberta.  
  
 *asym_key_name*  
 Especifica uma chave assimétrica usada para criptografar a chave que está sendo criada. Essa chave assimétrica já deve existir no banco de dados.  
  
 \<algorithm>  
Especifique o algoritmo de criptografia.   
> [!WARNING]  
> A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], todos os algoritmos, exceto AES_128, AES_192 e AES_256, foram preteridos. Para usar algoritmos mais antigos (não recomendado), você deve definir o nível de compatibilidade do banco de dados para 120 ou menos.  
  
## <a name="remarks"></a>Remarks  
 Quando uma chave simétrica é criada, a chave simétrica deve ser criptografada usando pelo menos um dos seguintes: senha, certificado, chave simétrica, chave assimétrica ou provedor. A chave pode ter mais de uma criptografia de cada tipo. Em outras palavras, uma única chave simétrica pode ser criptografada com o uso de vários certificados, senhas, chaves simétricas e chaves assimétricas ao mesmo tempo.  
  
> [!CAUTION]  
>  Quando uma chave simétrica é criptografada com uma senha, em vez de um certificado (ou outra chave), o algoritmo de criptografia TRIPLE DES é usado para criptografar a senha. Por esse motivo, as chaves criadas com um algoritmo de criptografia forte, como AES, são protegidas por um algoritmo mais fraco.  
  
 A senha opcional pode ser usada para criptografar a chave simétrica antes de distribuir a chave a vários usuários.  
  
 Chaves temporárias são de propriedade do usuário que as cria. Elas só são válidas para a sessão atual.  
  
 IDENTITY_VALUE gera um GUID com o qual os dados criptografados com a nova chave simétrica devem ser marcados. Essa marcação pode ser usada para corresponder chaves a dados criptografados. O GUID gerado por uma frase específica é sempre o mesmo. Após uma frase ter sido usada para gerar um GUID, ela não poderá ser reutilizada, a menos que haja pelo menos uma sessão usando ativamente a frase. IDENTITY_VALUE é uma cláusula opcional; entretanto, recomendamos usá-la ao armazenar dados criptografados com uma chave temporária.  
  
 Não há nenhum algoritmo de criptografia padrão.  
  
> [!IMPORTANT]  
>  Não recomendamos usar as codificações de fluxo RC4 e RC4_128 para proteger dados confidenciais. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não codifica adicionalmente a criptografia executada com essas chaves.  
  
 As informações sobre chaves simétricas podem ser visualizadas na exibição do catálogo [sys.symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md).  
  
 As chaves simétricas não podem ser criptografadas por chaves simétricas criadas no provedor de criptografia.  
  
 **Esclarecimento em relação aos algoritmos DES:**  
  
-   O DESX foi nomeado incorretamente. As chaves simétricas criadas com ALGORITHM = DESX na verdade usam a cifra TRIPLE DES com uma chave de 192 bits. O algoritmo DESX não é fornecido. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
-   As chaves simétricas criadas com ALGORITHM = TRIPLE_DES_3KEY usam TRIPLE DES com uma chave de 192 bits.  
-   As chaves simétricas criadas com ALGORITHM = TRIPLE_DES usam TRIPLE DES com uma chave de 128 bits.  
  
 **Reprovação do algoritmo RC4:**  
  
 O uso repetido do mesmo RC4 ou RC4_128 KEY_GUID em blocos de dados diferentes resulta na mesma chave RC4 porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não fornece um sal automaticamente. O uso da mesma chave RC4 repetidamente é um erro bem conhecido que resulta em criptografia muito fraca. Portanto preterimos as palavras-chave RC4 e RC4_128. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
> [!WARNING]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER ANY SYMMETRIC KEY no banco de dados. Se AUTHORIZATION for especificada, será necessária a permissão IMPERSONATE no usuário de banco de dados ou a permissão ALTER na função de aplicativo. Se a criptografia for por certificado ou chave assimétrica, exigirá a permissão VIEW DEFINITION no certificado ou na chave assimétrica. Somente logons do Windows, logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e funções de aplicativo podem ter chaves simétricas. Grupos e funções não podem possuir chaves simétricas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-symmetric-key"></a>A. Criando uma chave simétrica  
 O exemplo a seguir cria uma chave simétrica denominada `JanainaKey09` usando o algoritmo `AES 256` e criptografa a nova chave com o certificado `Shipping04`.  
  
```  
CREATE SYMMETRIC KEY JanainaKey09   
WITH ALGORITHM = AES_256  
ENCRYPTION BY CERTIFICATE Shipping04;  
GO  
```  
  
### <a name="b-creating-a-temporary-symmetric-key"></a>B. Criando uma chave simétrica temporária  
 O exemplo seguinte cria uma chave simétrica temporária chamada `#MarketingXXV` na frase secreta: `The square of the hypotenuse is equal to the sum of the squares of the sides`. A chave é fornecida com um GUID gerado na cadeia de caracteres `Pythagoras` e criptografado com o certificado `Marketing25`.  
  
```  
  
CREATE SYMMETRIC KEY #MarketingXXV   
WITH ALGORITHM = AES_128,  
KEY_SOURCE   
     = 'The square of the hypotenuse is equal to the sum of the squares of the sides',  
IDENTITY_VALUE = 'Pythagoras'  
ENCRYPTION BY CERTIFICATE Marketing25;  
GO  
```  
  
### <a name="c-creating-a-symmetric-key-using-an-extensible-key-management-ekm-device"></a>C. Criando uma chave simétrica com um dispositivo EKM (Extensible Key Management, Gerenciamento extensível de chaves)  
 O exemplo seguinte cria uma chave simétrica denominada `MySymKey` usando um provedor chamado `MyEKMProvider` e um nome de chave `KeyForSensitiveData`. Ele atribui a autorização ao `User1` e pressupõe que o administrador de sistema já registrou o provedor denominado `MyEKMProvider` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
CREATE SYMMETRIC KEY MySymKey  
AUTHORIZATION User1  
FROM PROVIDER EKMProvider  
WITH  
PROVIDER_KEY_NAME='KeyForSensitiveData',  
CREATION_DISPOSITION=OPEN_EXISTING;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
