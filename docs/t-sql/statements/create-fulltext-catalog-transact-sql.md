---
title: "CRIAR o catálogo de texto completo (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CATALOG_TSQL
- CREATE_FULLTEXT_TSQL
- FULLTEXT_TSQL
- FULLTEXT CATALOG
- CREATE FULLTEXT CATALOG
- CREATE_FULLTEXT_CATALOG_TSQL
- CATALOG
- FULLTEXT_CATALOG_TSQL
- CREATE FULLTEXT
- FULLTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- CREATE FULLTEXT CATALOG statement
ms.assetid: d7a8bd93-e2d7-4a40-82ef-39069e65523b
caps.latest.revision: 60
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: f08bdaeaacb970c839ea1d7bb31c44f454daadf8
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="create-fulltext-catalog-transact-sql"></a>CREATE FULLTEXT CATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria um catálogo de texto completo para um banco de dados. Um catálogo de texto completo pode ter vários índices de texto completo, mas um índice de texto completo só pode fazer parte de um único catálogo de texto completo. Cada banco de dados pode conter zero ou mais catálogos de texto completo.  
  
 Não é possível criar catálogos de texto completo no **mestre**, **modelo**, ou **tempdb** bancos de dados.  
  
> [!IMPORTANT]  
>  A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], um catálogo de texto completo é um objeto virtual e não pertence a nenhum grupo de arquivos. Um catálogo de texto completo é um conceito lógico que faz referência a um grupo de índices de texto completo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE FULLTEXT CATALOG catalog_name  
     [ON FILEGROUP filegroup ]  
     [IN PATH 'rootpath']  
     [WITH <catalog_option>]  
     [AS DEFAULT]  
     [AUTHORIZATION owner_name ]  
  
<catalog_option>::=  
     ACCENT_SENSITIVITY = {ON|OFF}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *catalog_name*  
 É o nome do novo catálogo. O nome do catálogo deve ser exclusivo entre todos os nomes de catálogo no banco de dados atual. Além disso, o nome do arquivo que corresponde ao catálogo de texto completo (consulte ON FILEGROUP) deve ser exclusivo entre todos os arquivos no banco de dados. Se o nome do catálogo já for usado para outro catálogo no banco de dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro.  
  
 O comprimento do nome de catálogo não pode exceder 120 caracteres.  
  
 ON FILEGROUP *filegroup*  
 A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], esta cláusula não tem nenhum efeito.  
  
 NO caminho **'***rootpath***'**  
 > [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], esta cláusula não tem nenhum efeito.  
  
 ACCENT_SENSITIVITY = {ON|OFF}  
 Especifica se o catálogo a ser alterado diferencia ou não acentos para indexação de texto completo. Quando esta propriedade é alterada, o índice deve ser recriado. O padrão é usar a diferenciação de acentos especificada no agrupamento de banco de dados. Para exibir o agrupamento de banco de dados, use o **sys. Databases** exibição do catálogo.  
  
 Para determinar a configuração atual da propriedade sensibilidade de acentuação de um catálogo de texto completo, use a função FULLTEXTCATALOGPROPERTY com o **accentsensitivity** valor da propriedade contra *catalog_name*. Se o valor retornado é '1', o catálogo de texto completo diferencia acentuação; se o valor é '0', o catálogo não diferencia acentuação.  
  
 AS DEFAULT  
 Especifica que o catálogo é o padrão. Quando forem criados índices de texto completo sem um catálogo de texto completo explicitamente especificado, o catálogo padrão será usado. Se um catálogo de texto completo existente já estiver marcado como AS DEFAULT, a configuração AS DEFAULT tornará esse catálogo o padrão.  
  
 AUTORIZAÇÃO *owner_name*  
 Define o proprietário do catálogo de texto completo como o nome de um usuário ou uma função de banco de dados. Se *owner_name* é uma função, a função deve ser o nome de uma função que o usuário atual é membro ou o usuário que executa a instrução deve ser o proprietário do banco de dados ou o administrador do sistema.  
  
 Se *owner_name* é um nome de usuário, o nome de usuário deve ser um dos seguintes:  
  
-   O nome do usuário que executa a instrução.  
  
-   O nome de um usuário para o qual o usuário que executa o comando tem permissões de representação.  
  
-   O usuário que executa o comando deve ser o proprietário de banco de dados ou administrador do sistema.  
  
 *owner_name* também deve ser concedida a permissão TAKE OWNERSHIP no catálogo de texto completo especificado.  
  
## <a name="remarks"></a>Comentários  
 As IDs de catálogos de texto completo iniciam em 00005 e são incrementadas em um para cada catálogo novo criado.  
  
## <a name="permissions"></a>Permissões  
 Usuário deve ter permissão CREATE FULLTEXT CATALOG no banco de dados, ou ser um membro do **db_owner**, ou **db_ddladmin** funções de banco de dados fixas.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um catálogo de texto completo e também um índice de texto completo.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume) KEY INDEX PK_JobCandidate_JobCandidateID;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys. fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [REMOVER o catálogo de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)   
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)   
 
  
  

