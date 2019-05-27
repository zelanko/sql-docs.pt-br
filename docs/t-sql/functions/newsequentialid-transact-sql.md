---
title: NEWSEQUENTIALID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NEWSEQUENTIALID
- NEWSEQUENTIALID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEWSEQUENTIALID function
- GUIDs [SQL Server]
ms.assetid: e06d2cab-f1ff-42f1-8550-6aaec57be36f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 19c9caf543f7db84cbf71f76832176118d262f60
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65944179"
---
# <a name="newsequentialid-transact-sql"></a>NEWSEQUENTIALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria um GUID que é maior que qualquer GUID anteriormente gerado por esta função em um computador especificado desde o início do Windows. Após o reinício do Windows, o GUID poderá ser iniciado novamente a partir de um intervalo inferior, mas ainda será globalmente exclusivo. Quando uma coluna de GUID é usada como um identificador de linha, usar NEWSEQUENTIALID pode ser mais rápido do que usar a função NEWID. Isso ocorre porque a função NEWID provoca atividade aleatória e usa menos páginas de dados do cache. O uso de NEWSEQUENTIALID também ajuda a preencher completamente as páginas de dados e índice.  
  
> [!IMPORTANT]  
>  Se a privacidade for uma preocupação, não use esta função. É possível adivinhar o valor do próximo GUID gerado e, assim, acessar os dados associados ao GUID.  
  
 NEWSEQUENTIALID é um wrapper na função [UuidCreateSequential](https://go.microsoft.com/fwlink/?LinkId=164027) do Windows, com [embaralhamento de bytes aplicado](https://blogs.msdn.microsoft.com/dbrowne/2012/07/03/how-to-generate-sequential-guids-for-sql-server-in-net/).
  
> [!WARNING]  
>  A função UuidCreateSequential tem dependências de hardware. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clusters de valores sequenciais podem se desenvolver quando os bancos de dados (como bancos de dados independentes) são movidos para outros computadores. Ao usar o Always On e no [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], clusters de valores sequenciais podem se desenvolver se o banco de dados faz failover para outro computador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NEWSEQUENTIALID ( )  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 **uniqueidentifier**  
  
## <a name="remarks"></a>Remarks  
 NEWSEQUENTIALID() apenas pode ser usado com restrições DEFAULT em colunas de tabela do tipo **uniqueidentifier**. Por exemplo:  
  
```  
CREATE TABLE myTable (ColumnA uniqueidentifier DEFAULT NEWSEQUENTIALID());   
```  
  
 Quando NEWSEQUENTIALID() for usada em expressões DEFAULT, não pode ser combinada com outros operadores escalares. Por exemplo, não é possível executar a seguinte consulta:  
  
```  
CREATE TABLE myTable (ColumnA uniqueidentifier DEFAULT dbo.myfunction(NEWSEQUENTIALID()));  
```  
  
 No exemplo anterior, `myfunction()` é uma função escalar de escalar definida pelo usuário que aceita e retorna um valor `uniqueidentifier`.  
  
 NEWSEQUENTIALID() não pode ser referenciada em consultas.  
  
 Você pode usar NEWSEQUENTIALID para gerar GUIDs e reduzir a contenção da página no nível folha de índices.  
  
 Cada GUID gerado usando NEWSEQUENTIALID é exclusivo nesse computador. Os GUIDs gerados com NEWSEQUENTIALID serão exclusivos entre vários computadores somente se o computador de origem tiver uma placa de rede.  
  
## <a name="see-also"></a>Consulte Também  
 [NEWID &#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md)   
 [Operadores de comparação &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)  
  
  
