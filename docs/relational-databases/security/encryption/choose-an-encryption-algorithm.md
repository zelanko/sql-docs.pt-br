---
title: Escolha um algoritmo de criptografia | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cryptography [SQL Server], algorithms
- encryption [SQL Server], algorithms
- security [SQL Server], encryption
- algorithms [SQL Server encryption]
ms.assetid: 8227028c-a9c9-489d-bd27-fbf8242634ae
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 66853b6453dae0c3855d23f390e3d1534b830859
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="choose-an-encryption-algorithm"></a>Escolher um algoritmo de criptografia
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  A criptografia é um dos muitos recursos de proteção que estão disponíveis para o administrador que deseja oferecer segurança a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Algoritmos de criptografia definem transformações de dados que não podem ser invertidas facilmente por usuários não autorizados. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite que administradores e desenvolvedores escolham entre diversos algoritmos, incluindo DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, RC4 de 128 bits, DESX, AES de 128 bits, AES de 192 bits e AES de 256 bits.  
  
> [!NOTE]  
>  A partir do [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], todos os algoritmos, exceto AES_128, AES_192 e AES_256, foram preteridos. Para usar algoritmos mais antigos (não recomendado) você deve definir o nível de compatibilidade do banco de dados para 120 ou inferior.  
  
 Nenhum algoritmo é ideal para todas as situações e informações sobre o benefício de cada um está além do escopo dos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Porém, os seguintes princípios gerais se aplicam:  
  
-   A criptografia segura geralmente consome mais recursos da CPU que criptografia menos segura.  
  
-   As chaves extensas geralmente produzem uma criptografia mais segura que as chaves mais curtas.  
  
-   A criptografia assimétrica é mais fraca que a criptografia simétrica, que usa o mesmo comprimento de chave mas é relativamente lenta.  
  
-   Codificações em bloco com chaves extensas são mais seguras que codificações em fluxo.  
  
-   Senhas longas e complexas são mais seguras que senhas curtas.  
  
-   Se você estiver criptografando muitos dados, deve criptografá-los usando uma chave simétrica e criptografar a chave simétrica com uma chave assimétrica.  
  
-   Dados criptografados não podem ser compactados, mas dados compactados podem ser criptografados. Se você usar compactação, deverá compactar os dados antes de criptografá-los.  
  
> [!IMPORTANT]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e versões posteriores, o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
>   
>  O uso repetido do mesmo RC4 ou RC4_128 KEY_GUID em blocos de dados diferentes resulta na mesma chave RC4 porque o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não fornece um salt automaticamente. O uso da mesma chave RC4 repetidamente é um erro bem conhecido que resulta em criptografia muito fraca. Portanto, preterimos as palavras-chave RC4 e RC4_128. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)]  
  
 Para obter mais informações sobre os algoritmos de criptografia e sobre a tecnologia de criptografia, consulte [Conceitos de segurança de chave](http://go.microsoft.com/fwlink/?LinkId=62082) no Guia do desenvolvedor do .NET Framework do MSDN.  
  
 **Esclarecimento em relação aos algoritmos DES:**  
  
-   O DESX foi nomeado incorretamente. As chaves simétricas criadas com ALGORITHM = DESX na verdade usam a cifra TRIPLE DES com uma chave de 192 bits. O algoritmo DESX não é fornecido. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   As chaves simétricas criadas com ALGORITHM = TRIPLE_DES_3KEY usam TRIPLE DES com uma chave de 192 bits.  
  
-   As chaves simétricas criadas com ALGORITHM = TRIPLE_DES usam TRIPLE DES com uma chave de 128 bits.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|Criptografando com o uso de uma chave simétrica.|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|Criptografando com o uso de uma chave assimétrica.|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|Criptografando com o uso de um certificado.|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)|  
|Criptografando arquivos de banco de dados com o uso de criptografia transparente de dados.|[TDE &#40;Transparent Data Encryption&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)|  
|Como criptografar uma coluna de uma tabela.|[Criptografar uma coluna de dados](../../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Criptografia do SQL Server](../../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Hierarquia de criptografia](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
