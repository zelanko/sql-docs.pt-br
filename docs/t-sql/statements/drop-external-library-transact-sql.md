---
title: DROP EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: e39accbc9c4d3d45b5842e0431f14cd92908eb0f
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471138"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Exclui uma biblioteca de pacote existente. As bibliotecas de pacotes são usadas por tempos de execução externos com suporte, tais como do R, Python ou Java.

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
> [!NOTE]
> No SQL Server 2017, há compatibilidade apenas com a linguagem R e a plataforma Windows. Há suporte para R, Python e Java nas plataformas Windows e Linux no SQL Server 2019 CTP 2.4. 
::: moniker-end

## <a name="syntax"></a>Sintaxe

```sql
DROP EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ];
```

### <a name="arguments"></a>Argumentos

**library_name**

Especifica o nome de uma biblioteca de pacotes existente.

As bibliotecas estão no escopo do usuário. Os nomes de bibliotecas devem ser exclusivos no contexto de um usuário ou proprietário específico.

**owner_name**

Especifica o nome do usuário ou da função que é a proprietária da biblioteca externa.

Os proprietários de banco de dados podem excluir bibliotecas criadas por outros usuários.

## <a name="permissions"></a>Permissões

Para excluir uma biblioteca, é necessário ter o privilégio ALTER ANY EXTERNAL LIBRARY. Por padrão, todos os proprietários de bancos de dados ou do objeto também podem excluir uma biblioteca externa.

### <a name="return-values"></a>Valores retornados

Uma mensagem informativa é retornada se a instrução foi bem-sucedida.

## <a name="remarks"></a>Remarks

Ao contrário de outras instruções `DROP` no SQL Server, essa instrução dá suporte à especificação de uma cláusula de autorização opcional. Isso permite que o **dbo** ou os usuários na função **db_owner** removam uma biblioteca de pacote carregada por um usuário normal no banco de dados.

## <a name="examples"></a>Exemplos

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Adicione o pacote do R personalizado, chamado `customPackage`, a um banco de dados:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM (CONTENT = 'C:\temp\customPackage_v1.1.zip')
WITH (LANGUAGE = 'R');
GO
```
::: moniker-end

Exclua a biblioteca `customPackage`.

```sql
DROP EXTERNAL LIBRARY customPackage;
```

## <a name="see-also"></a>Confira também

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
