---
title: '@@VERSION (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@VERSION'
- '@@VERSION_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@VERSION function'
- current SQL Server installation information
- versions [SQL Server], @@VERSION
- processors [SQL Server], types
ms.assetid: 385ba80e-7c28-41a5-9cdb-5648f3785983
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1894f0e4aa31e8b80255fb49f30c7cfe1c1a146b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67927539"
---
# <a name="x40x40version---transact-sql-configuration-functions"></a>&#x40;&#x40;Versão – funções de configuração do Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações de compilação e sistema para a instalação atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@VERSION  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar**  
  
## <a name="remarks"></a>Comentários  
 Os resultados de @@VERSION são apresentados como uma cadeia de caracteres nvarchar. Use a função [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md) para recuperar os valores de propriedade individuais.  
  
 Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as informações a seguir são retornadas.  
  
-   Versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Arquitetura do processador  
  
-   Data de compilação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Instrução de direitos autorais  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edição  
  
-   Versão do sistema operacional  
  
 Para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as informações a seguir são retornadas.  
  
-   Edição- "Microsoft SQL Azure"  
  
-   Nível do produto- "(RTM)"  
  
-   Versão do produto  
  
-   Data de compilação  
  
-   Instrução de direitos autorais  

> [!NOTE]  
> Estamos cientes de um problema em que a versão de produto relatada por @@VERSION está incorreta para o Banco de Dados SQL do Azure. A versão do mecanismo de banco de dados do SQL Server executada pelo Banco de Dados SQL do Azure sempre está à frente da versão local do SQL Server e inclui as correções de segurança mais recentes. Isso significa que o nível de patch está sempre pareado com a versão local do SQL Server ou à frente dela e que os recursos mais recentes disponíveis no SQL Server estão disponíveis no Banco de Dados SQL do Azure.
>
> Para determinar programaticamente a edição do mecanismo, use SELECT SERVERPROPERTY('EngineEdition'). Essa consulta retornará “5” para bancos de dados individuais/pools elásticos e “8” para instâncias gerenciadas no Banco de Dados SQL do Azure. 
>
> A documentação será atualizada depois que esse problema for resolvido.

  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-the-current-version-of-ssnoversion"></a>A: Retornar a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O exemplo a seguir mostra o retorno das informações de versão da instalação atual.  
  
```  
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-return-the-current-version-of-ssdw"></a>B. Retornar a versão atual do [!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
  
```  
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  

