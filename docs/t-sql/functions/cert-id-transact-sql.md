---
description: CERT_ID (Transact-SQL)
title: CERT_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERT_ID
- CERT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], certificates
- CERT_ID function
- IDs [SQL Server], certificates
- certificates [SQL Server], IDs
ms.assetid: 59cc06f5-272e-4936-8afe-afba7aba8eea
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 70e1cb5ea77b6bd779d63cd349f1478cda31598f
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91114955"
---
# <a name="cert_id-transact-sql"></a>CERT_ID (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Essa função retorna o valor da ID de um certificado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
Cert_ID ( 'cert_name' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
**'** *cert_name* **'**  

O nome de um certificado no banco de dados.
  
## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="remarks"></a>Comentários  
A exibição de catálogo [sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) mostra nomes de certificado.
  
## <a name="permissions"></a>Permissões  
Exige permissões apropriadas no certificado e que a permissão VIEW DEFINITION não tenha sido negada ao chamador no certificado. Consulte [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md#permissions) para obter mais informações sobre permissões de certificado.
  
## <a name="examples"></a>Exemplos  
Esse exemplo retorna a ID de um certificado chamada `ABerglundCert3`.
  
```sql
SELECT Cert_ID('ABerglundCert3');  
GO  
```  
  
## <a name="see-also"></a>Confira também
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)
  
  
