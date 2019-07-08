---
title: Criptografia Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, cryptography system
ms.assetid: ae8226ff-0853-4716-be7b-673ce77dd370
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e0ec7ce1a9c3a171ea44b23c5fa4a5897ad7de8
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388374"
---
# <a name="always-encrypted-cryptography"></a>Criptografia Always Encrypted
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Este documento descreve mecanismos e algoritmos de criptografia para derivar o material criptográfico usado no recurso [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)].  
  
## <a name="keys-key-stores-and-key-encryption-algorithms"></a>Chaves, repositórios de chaves e algoritmos de criptografia de chave
 O Always Encrypted usa dois tipos de chaves: Chaves mestras de coluna e chaves de criptografia de coluna.  
  
 Uma CMK (chave mestra de coluna) é uma chave que criptografa uma chave (por exemplo, uma chave usada para criptografar outras chaves) que está sempre no controle do cliente e é armazenada em um repositório de chaves externas. Um driver de cliente habilitado para Always Encrypted interage com o repositório de chaves por meio de um provedor de repositório CMK, que pode fazer parte da biblioteca de drivers (um provedor do sistema/ [!INCLUDE[msCoName](../../../includes/msconame-md.md)]) ou parte do aplicativo cliente (um provedor personalizado). Atualmente, as bibliotecas de drivers de cliente incluem provedores de repositório de chaves [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para [Repositório de Certificados do Windows](/windows/desktop/SecCrypto/using-certificate-stores) e HSMs (módulos de segurança de hardware).  (Para obter a lista atual de provedores, veja [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md).) Um desenvolvedor de aplicativos pode fornecer um provedor personalizado para um repositório arbitrário.  
  
 Uma CEK (chave de criptografia de coluna) é uma criptografia de conteúdo (por exemplo, uma chave usada para proteger dados) protegida por uma CMK.  
  
 Todos os provedores de repositórios de CMK [!INCLUDE[msCoName](../../../includes/msconame-md.md)] criptografam CEKs usando RSA-OAEP (RSA com Preenchimento de Criptografia Assimétrica Ideal). O provedor de repositório de chaves que dá suporte à API de Criptografia da Microsoft: A próxima geração (CNG) no .NET Framework ([SqlColumnEncryptionCngProvider Class](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncngprovider.aspx)) usa os parâmetros padrão especificados por RFC 8017 na seção A.2.1. Esses parâmetros padrão estão usando uma função de hash de SHA-1 e uma função de geração de máscara de MGF1 com SHA-1. Todos os outros provedores de repositório de chaves usam SHA-256. 
  
## <a name="data-encryption-algorithm"></a>Algoritmo de criptografia de dados  
 O Always Encrypted usa o algoritmo **AEAD_AES_256_CBC_HMAC_SHA_256** para criptografar dados no banco de dados.  
  
 **AEAD_AES_256_CBC_HMAC_SHA_256** é derivado do projeto da especificação em [https://tools.ietf.org/html/draft-mcgrew-aead-aes-cbc-hmac-sha2-05](https://tools.ietf.org/html/draft-mcgrew-aead-aes-cbc-hmac-sha2-05). Ele usa um esquema de Criptografia Autenticada com Dados Associados, seguindo uma abordagem Criptografar depois MAC. Isto é, o texto não criptografado é criptografado primeiro e o MAC é gerado com base no texto cifrado resultante.  
  
 Para ocultar padrões, o **AEAD_AES_256_CBC_HMAC_SHA_256** usa o modo de operação CBC (Encadeamento de Blocos de Criptografia), em que um valor inicial é alimentado no sistema chamado IV (vetor de inicialização). A descrição completa do modo CBC pode ser encontrada em [https://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf](https://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf).  
  
 O**AEAD_AES_256_CBC_HMAC_SHA_256** computa um valor de texto cifrado para determinado valor de texto não criptografado usando as etapas a seguir.  
  
### <a name="step-1-generating-the-initialization-vector-iv"></a>Etapa 1: Gerando o IV (vetor de inicialização)  
 O Always Encrypted dá suporte a duas variações de **AEAD_AES_256_CBC_HMAC_SHA_256**:  
  
-   Aleatória  
  
-   Determinística  
  
 Para criptografia aleatória, o IV é gerado aleatoriamente. Como resultado, toda vez que o mesmo texto não criptografado é criptografado, um texto cifrado diferente é gerado, o que impede a divulgação de quaisquer informações.  
  
```  
When using randomized encryption: IV = Generate cryptographicaly random 128bits  
```  
  
 Caso haja criptografia determinística, o IV não é gerado aleatoriamente, mas, em vez disso, ele é derivado do valor de texto não criptografado usando o seguinte algoritmo:  
  
```  
When using deterministic encryption: IV = HMAC-SHA-256( iv_key, cell_data ) truncated to 128 bits.  
```  
  
 Onde iv_key é derivado da CEK da seguinte maneira:  
  
```  
iv_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell IV key" + algorithm + CEK_length)  
```  
  
 O truncamento do valor HMAC é executado para adequação de 1 bloco de dados conforme a necessidade do IV.
Como resultado, a criptografia determinística sempre produz o mesmo texto cifrado para um determinado valor de texto não criptografado, o que permite inferir se dois valores de texto não criptografado são iguais comparando seus valores de texto cifrado correspondentes. Essa divulgação limitada de informações permite que o sistema de banco de dados ofereça suporte à comparação de igualdade em valores de coluna criptografados.  
  
 A criptografia determinística é mais eficaz em ocultar padrões, em comparação com as alternativas, como usar um valor predefinido de IV.  
  
### <a name="step-2-computing-aes256cbc-ciphertext"></a>Etapa 2: Computando o texto cifrado AES_256_CBC  
 Depois de computar o IV, o texto cifrado **AES_256_CBC** é gerado:  
  
```  
aes_256_cbc_ciphertext = AES-CBC-256(enc_key, IV, cell_data) with PKCS7 padding.  
```  
  
 Onde a chave de criptografia (enc_key) é derivada da CEK como se segue.  
  
```  
enc_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell encryption key" + algorithm + CEK_length )  
```  
  
### <a name="step-3-computing-mac"></a>Etapa 3: Computando o MAC  
 Subsequentemente, o MAC é computado usando o seguinte algoritmo:  
  
```  
MAC = HMAC-SHA-256(mac_key, versionbyte + IV + Ciphertext + versionbyte_length)  
```  
  
 Onde:  
  
```  
versionbyte = 0x01 and versionbyte_length = 1
mac_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell MAC key" + algorithm + CEK_length)  
```  
  
### <a name="step-4-concatenation"></a>Etapa 4: Concatenation  
 Por fim, o valor criptografado é produzido com a concatenação do byte da versão do algoritmo, do MAC, do IV e do texto cifrado AES_256_CBC:  
  
```  
aead_aes_256_cbc_hmac_sha_256 = versionbyte + MAC + IV + aes_256_cbc_ciphertext  
```  
  
## <a name="ciphertext-length"></a>Comprimento do texto cifrado  
 Os tamanhos (em bytes) de componentes específicos do texto cifrado **AEAD_AES_256_CBC_HMAC_SHA_256** são:  
  
-   versionbyte: 1  
  
-   MAC: 32  
  
-   IV: 16  
  
-   aes_256_cbc_ciphertext: `(FLOOR (DATALENGTH(cell_data)/ block_size) + 1)* block_size`, em que:  
  
    -   block_size é 16 bytes  
  
    -   cell_data é um valor de texto não criptografado  
  
     Portanto, o tamanho mínimo de aes_256_cbc_ciphertext é 1 bloco, que são 16 bytes.  
  
 Portanto, o comprimento do texto cifrado, resultante da criptografia de determinados valores de texto não criptografado (cell_data) pode ser calculado usando a fórmula a seguir:  
  
```  
1 + 32 + 16 + (FLOOR(DATALENGTH(cell_data)/16) + 1) * 16  
```  
  
 Por exemplo:  
  
-   Um valor de texto não criptografado **int** longo de 4 bytes torna-se um valor binário longo de 65 bytes após a criptografia.  
  
-   Um valor de texto não criptografado **nchar(1000)** longo de 2.000 bytes torna-se um valor binário longo de 2.065 bytes após a criptografia.  
  
 A tabela a seguir contém uma lista completa de tipos de dados e o comprimento do texto cifrado para cada tipo.  
  
|Tipo de Dados|Comprimento do texto cifrado [bytes]|  
|---------------|---------------------------------|  
|**bigint**|65|  
|**binary**|Varia. Use a fórmula acima.|  
|**bit**|65|  
|**char**|Varia. Use a fórmula acima.|  
|**date**|65|  
|**datetime**|65|  
|**datetime2**|65|  
|**datetimeoffset**|65|  
|**decimal**|81|  
|**float**|65|  
|**geografia**|N/D (sem suporte)|  
|**geometria**|N/D (sem suporte)|  
|**hierarchyid**|N/D (sem suporte)|  
|**imagem**|N/D (sem suporte)|  
|**int**|65|  
|**money**|65|  
|**nchar**|Varia. Use a fórmula acima.|  
|**ntext**|N/D (sem suporte)|  
|**numeric**|81|  
|**nvarchar**|Varia. Use a fórmula acima.|  
|**real**|65|  
|**smalldatetime**|65|  
|**smallint**|65|  
|**smallmoney**|65|  
|**sql_variant**|N/D (sem suporte)|  
|**sysname**|N/D (sem suporte)|  
|**text**|N/D (sem suporte)|  
|**time**|65|  
|**timestamp**<br /><br /> (**rowversion**)|N/D (sem suporte)|  
|**tinyint**|65|  
|**uniqueidentifier**|81|  
|**varbinary**|Varia. Use a fórmula acima.|  
|**varchar**|Varia. Use a fórmula acima.|  
|**xml**|N/D (sem suporte)|  
  
## <a name="net-reference"></a>Referência do .NET  
 Para obter detalhes sobre os algoritmos abordados neste documento, confira os arquivos **SqlAeadAes256CbcHmac256Algorithm.cs** e **SqlColumnEncryptionCertificateStoreProvider.cs** na [Referência do .NET](https://referencesource.microsoft.com/).  
  
## <a name="see-also"></a>Consulte Também  
 [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted &#40;desenvolvimento de cliente&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
