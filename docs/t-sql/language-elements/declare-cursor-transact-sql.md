---
title: DECLARE CURSOR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECLARE_CURSOR_TSQL
- CURSOR_TSQL
- DECLARE CURSOR
- CURSOR
dev_langs: TSQL
helpviewer_keywords:
- DECLARE CURSOR statement
- cursors [SQL Server], attributes
- local cursors [SQL Server]
- nesting cursors
- Transact-SQL cursors, attributes
- global cursors [SQL Server]
ms.assetid: 5a3a27aa-03e8-4c98-a27e-809282379b21
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 79bf3115ef4e1d929e3e4a1b3ff731a1977ba28e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="declare-cursor-transact-sql"></a>DECLARE CURSOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Define os atributos de um cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)], como seu comportamento de rolagem e a consulta usada para construir o conjunto de resultados no qual o cursor funciona. DECLARE CURSOR aceita uma sintaxe fundada no padrão ISO e uma sintaxe que usa um conjunto de extensões [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ISO Syntax  
DECLARE cursor_name [ INSENSITIVE ] [ SCROLL ] CURSOR   
     FOR select_statement   
     [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]  
[;]  
Transact-SQL Extended Syntax  
DECLARE cursor_name CURSOR [ LOCAL | GLOBAL ]   
     [ FORWARD_ONLY | SCROLL ]   
     [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
     [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
     [ TYPE_WARNING ]   
     FOR select_statement   
     [ FOR UPDATE [ OF column_name [ ,...n ] ] ]  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor_name*  
 É o nome do [!INCLUDE[tsql](../../includes/tsql-md.md)] cursor de servidor definido. *cursor_name* devem estar em conformidade com as regras para identificadores.  
  
 INSENSITIVE  
 Define um cursor que faz uma cópia temporária dos dados a serem usados por ele. Todas as solicitações para o cursor são respondidas a partir dessa tabela temporária em **tempdb**; portanto, as modificações feitas na tabelas base não são refletidas nos dados retornados pelas buscas feitas nesse cursor, e esse cursor não permitir modificações. Quando a sintaxe de ISO é usada, se INSENSITIVE for omitido, exclusões e atualizações confirmadas nestas tabelas subjacentes (por qualquer usuário) são refletidas em buscas subsequentes.  
  
 SCROLL  
 Especifica que todas as opções de busca (FIRST, LAST, PRIOR, NEXT, RELATIVE, ABSOLUTE) estão disponíveis. Se SCROLL não for especificado em um ISO DECLARE CURSOR, NEXT será a única opção de busca com suporte. SCROLL não poderá ser especificado se FAST_FORWARD também for especificado.  
  
 *select_statement*  
 É uma instrução SELECT padrão que define o conjunto de resultados de um cursor. As palavras-chave FOR BROWSE e INTO não são permitidas em *select_statement* de uma declaração de cursor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Converte o cursor implicitamente a outro tipo se as cláusulas em *select_statement* conflito com a funcionalidade do tipo de cursor solicitado.  
  
 READ ONLY  
 Previne atualizações feitas por este cursor. O cursor não pode ser referenciado em uma cláusula WHERE CURRENT OF em uma instrução UPDATE ou DELETE. Essa opção anula a funcionalidade padrão de um cursor para ser atualizado.  
  
 UPDATE [OF *column_name* [**,**...*n*]]  
 Define colunas atualizáveis em um cursor. Se OF *column_name* [**,**... *n*] for especificado, somente as colunas listadas permitirão modificações. Se a UPDATE for especificada sem uma lista de colunas, todas as colunas poderão ser atualizadas.  
  
 *cursor_name*  
 É o nome do [!INCLUDE[tsql](../../includes/tsql-md.md)] cursor de servidor definido. *cursor_name* devem estar em conformidade com as regras para identificadores.  
  
 LOCAL  
 Especifica que o escopo do cursor é local para o lote, procedimento armazenado ou gatilho no qual o cursor foi criado. O nome de cursor só é válido dentro desse escopo. O cursor pode ser referenciado por meio de variáveis de cursor local no lote, no procedimento armazenado ou no gatilho, ou em um parâmetro OUTPUT do procedimento armazenado. Um parâmetro OUTPUT é usado para devolver o cursor local ao lote procedimento armazenado ou acionador de chamada, que pode nomear o parâmetro a uma variável de cursor para referenciar o cursor, depois que o procedimento armazenado terminar. O cursor é implicitamente desalocado quando o lote, procedimento armazenado ou acionador é encerrado, a menos que o cursor tenha sido repassado como um parâmetro OUTPUT. Se for repassado em um parâmetro OUTPUT, o cursor será desalocado quando a última variável que referenciada for desalocada ou extrapolar o escopo.  
  
 GLOBAL  
 Especifica que o escopo do cursor é global para a conexão. O nome do cursor pode ser referenciado em qualquer procedimento armazenado ou lote executado pela conexão. O cursor só é desalocado implicitamente na desconexão.  
  
> [!NOTE]  
>  Se nem GLOBAL nem LOCAL for especificado, o padrão é controlado pela configuração do **padronizar para cursor local** opção de banco de dados.  
  
 FORWARD_ONLY  
 Especifica se o cursor só pode ser rolado da primeira à última linha. FETCH NEXT é a única opção de busca com suporte. Se FORWARD_ONLY for especificado sem as palavras-chave STATIC, KEYSET ou DYNAMIC, o cursor operará como um cursor DYNAMIC. Quando FORWARD_ONLY ou SCROLL não estiverem especificados, FORWARD_ONLY será o padrão; a não ser que as palavras-chave STATIC, KEYSET ou DYNAMIC estejam especificadas. Os cursores STATIC, KEYSET e DYNAMIC seguem o padrão SCROLL. Diferentemente das APIs de banco de dados, como ODBC e ADO, os cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] STATIC, KEYSET e DYNAMIC oferecem suporte para FORWARD_ONLY  
  
 STATIC  
 Define um cursor que faz uma cópia temporária dos dados a serem usados por ele. Todas as solicitações para o cursor são respondidas a partir dessa tabela temporária em **tempdb**; portanto, as modificações feitas na tabelas base não são refletidas nos dados retornados pelas buscas feitas nesse cursor, e esse cursor não permitir modificações.  
  
 KEYSET  
 Especifica que a associação e a ordem de linhas no cursor são fixas, quando o cursor é aberto. O conjunto de chaves que identificam exclusivamente as linhas é criado em uma tabela no **tempdb** conhecido como o **keyset**.  
  
> [!NOTE]  
>  Se a consulta referencia ao menos uma tabela sem um índice exclusivo, o cursor controlado por conjunto de chaves é convertido a um cursor estático.  
  
 Alterações nos valores de chave nas tabelas base, feita pelo proprietário do cursor ou confirmadas por outros usuários, são visíveis como rolagens do proprietário ao redor do cursor. Inserções feitas por outros usuários não são visíveis (não é possível fazer inserções por um cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)]). Se uma linha for excluída, uma tentativa de buscar a linha retorna um @@FETCH_STATUS de -2. Atualização de valores de chave externos ao cursor lembram a exclusão de uma linha antiga, seguida de uma inserção de uma nova linha. A linha com os novos valores não estiver visível, e tenta buscar a linha com os valores antigos retorna um @@FETCH_STATUS de -2. Os novos valores ficarão visíveis se a atualização for feita através do cursor, especificando-se a cláusula WHERE CURRENT OF.   
  
 DYNAMIC  
 Define um cursor que reflete todas as mudanças de dados feitas às linhas no seu conjunto de resultados conforme você rola o cursor. Os valores de dados, a ordem e a associação das linhas podem ser alterados em cada busca. Cursores dinâmicos não oferecem suporte para a opção de busca ABSOLUTE.  
  
 FAST_FORWARD  
 Especifica um cursor FORWARD_ONLY, READ_ONLY, com otimizações de desempenho habilitadas. FAST_FORWARD não poderá ser especificado se SCROLL ou FOR_UPDATE também o for.  
  
> [!NOTE]  
>  FAST_FORWARD e FORWARD_ONLY podem ser usadas na mesma instrução DECLARE CURSOR.  
  
 READ_ONLY  
 Previne atualizações feitas por este cursor. O cursor não pode ser referenciado em uma cláusula WHERE CURRENT OF em uma instrução UPDATE ou DELETE. Essa opção anula a funcionalidade padrão de um cursor para ser atualizado.  
  
 SCROLL_LOCKS  
 Especifica se atualizações posicionadas ou exclusões feitas pelo cursor têm garantia de êxito. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloqueia as linhas à medida que são lidas no cursor para assegurar a disponibilidade para modificações posteriores. SCROLL_LOCKS não poderá ser especificado se FAST_FORWARD ou STATIC também o forem.  
  
 OPTIMISTIC  
 Especifica que as atualizações posicionadas e exclusões realizadas pelo cursor não terão êxito se a linha tiver sido atualizada desde que foi lida no cursor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não bloqueia linhas à medida que são lidas no cursor. Em vez disso, ele usa comparações de **timestamp** valores de coluna, ou um valor de soma de verificação se a tabela não tiver nenhuma **timestamp** coluna, para determinar se a linha foi modificada depois de lida no cursor. Se a linha tiver sido modificada, a tentativa de atualização ou exclusão posicionada falhará. OPTIMISTIC não poderá ser especificado se FAST_FORWARD também for especificado.  
  
 TYPE_WARNING  
 Especifica que uma mensagem de aviso é enviada ao cliente quando o cursor é convertido implicitamente em outro a partir do tipo solicitado.  
  
 *select_statement*  
 É uma instrução SELECT padrão que define o conjunto de resultados de um cursor. As palavras-chave COMPUTE, COMPUTE BY, FOR BROWSE e INTO não são permitidas em *select_statement* de uma declaração de cursor.  
  
> [!NOTE]  
>  Você pode usar uma dica de consulta dentro de uma declaração de cursor; No entanto, se você também pode usar a cláusula FOR UPDATE OF, especifique a opção (*query_hint*) depois de atualização.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Converte o cursor implicitamente a outro tipo se as cláusulas em *select_statement* conflito com a funcionalidade do tipo de cursor solicitado. Para obter mais informações, consulte Conversões implícitas de cursor  
  
 ATUALIZAÇÃO [OF *column_name* [**,**... *n*]]  
 Define colunas atualizáveis em um cursor. Se OF *column_name* [**,**...  *n* ] for fornecido, somente as colunas listadas permitirão modificações. Se UPDATE for especificada sem uma lista de colunas, todas as colunas poderão ser atualizadas, a não ser que a opção de simultaneidade READ_ONLY seja especificada.  
  
## <a name="remarks"></a>Remarks  
 DECLARE CURSOR define os atributos de um cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)], como seu comportamento de rolagem e a consulta usada para construir o conjunto de resultados no qual o cursor funciona. A instrução OPEN popula o conjunto de resultados e FETCH retorna uma linha do conjunto de resultados. A instrução CLOSE libera o conjunto de resultados atual associado com o cursor. A instrução DEALLOCATE libera os recursos usados pelo cursor.  
  
 O primeiro formulário da instrução DECLARE CURSOR usa a sintaxe ISO para declarar comportamentos do cursor. O segundo formulário do DECLARE CURSOR usa extensões [!INCLUDE[tsql](../../includes/tsql-md.md)] que lhe permitem definir cursores com os mesmos tipos de cursor usados nas funções do cursor de API do banco de dados de ODBC ou ADO.  
  
 Você não pode misturar os dois formulários. Se você especificar a ROLAGEM ou palavras-chave não DIFERENCIA antes da palavra-chave CURSOR, você não pode usar as palavras-chave entre CURSOR e FOR *select_statement* palavras-chave. Se você especificar quaisquer palavras-chave entre CURSOR e FOR *select_statement* palavras-chave, você não pode especificar SCROLL ou INSENSITIVE antes da palavra-chave CURSOR.  
  
 Se uma instrução DECLARE CURSOR que usa sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] não especificar READ_ONLY, OPTIMISTIC ou SCROLL_LOCKS, o padrão é como se segue:  
  
-   Se a instrução SELECT não oferecer suporte a atualizações (permissões insuficientes, acesso a tabelas remotas que não oferecem suporte a atualizações, e assim por diante), o cursor será READ_ONLY.  
  
-   Os cursores STATIC e de FAST_FORWARD seguem o padrão READ_ONLY.  
  
-   Os cursores DYNAMIC e KEYSET seguem o padrão OPTIMISTIC.  
  
 Nomes de cursor só podem ser referenciados através de outras instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Eles não podem ser referenciados através de funções da API do banco de dados. Por exemplo, depois de declarar um cursor, o nome de cursor não pode ser referenciado das funções ou métodos OLE DB, ODBC ou ADO. As linhas de cursor não podem ser pesquisadas com as funções ou métodos de busca das APIs; as linhas só podem ser buscadas através de instruções FETCH [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Depois que um cursor ter sido declarado, esses procedimentos armazenados do sistema podem ser usados para determinar as características do cursor.  
  
|Procedimentos armazenados do sistema|Description|  
|------------------------------|-----------------|  
|**sp_cursor_list**|Retorna uma lista de cursores atualmente visíveis na conexão e seus atributos.|  
|**sp_describe_cursor**|Descreve os atributos de um cursor, por exemplo, se ele é de somente avanço ou de rolagem.|  
|**sp_describe_cursor_columns**|Descreve os atributos das colunas no conjunto de resultados do cursor.|  
|**sp_describe_cursor_tables**|Descreve as tabelas base acessadas pelo cursor.|  
  
 Variáveis podem ser usadas como parte do *select_statement* que declara um cursor. Valores de variáveis de cursor não se alteram depois que um cursor é declarado.  
  
## <a name="permissions"></a>Permissões  
 Permissões de DECLARE CURSOR seguem o padrão para todo usuário que tem permissões SELECT para exibições, tabelas e colunas usadas no cursor.
 
## <a name="limitations-and-restrictions"></a>Limitações e restrições

Você não pode usar cursores ou gatilhos em uma tabela com um índice columnstore clusterizado. Essa restrição não se aplica a índices columnstore não clusterizado; Você pode usar cursores e gatilhos em uma tabela com um índice columnstore não clusterizado. 
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-simple-cursor-and-syntax"></a>A. Usando a sintaxe e o cursor simples  

O conjunto de resultados gerado na abertura deste cursor inclui todas as linhas e todas as colunas na tabela. Este cursor pode ser atualizado e todas as atualizações e exclusões são representadas em buscas feitas no cursor. `FETCH NEXT` é a única busca disponível porque a opção `SCROLL` não foi especificada.  

  
```  
DECLARE vend_cursor CURSOR  
    FOR SELECT * FROM Purchasing.Vendor  
OPEN vend_cursor  
FETCH NEXT FROM vend_cursor;  
```  
  
### <a name="b-using-nested-cursors-to-produce-report-output"></a>B. Usando cursores aninhados para produzir saída de relatório  
 O exemplo a seguir mostra como cursores podem ser aninhados para produzir relatórios complexos. O cursor interno é declarado para cada vendedor.  
  
```  
SET NOCOUNT ON;  
  
DECLARE @vendor_id int, @vendor_name nvarchar(50),  
    @message varchar(80), @product nvarchar(50);  
  
PRINT '-------- Vendor Products Report --------';  
  
DECLARE vendor_cursor CURSOR FOR   
SELECT VendorID, Name  
FROM Purchasing.Vendor  
WHERE PreferredVendorStatus = 1  
ORDER BY VendorID;  
  
OPEN vendor_cursor  
  
FETCH NEXT FROM vendor_cursor   
INTO @vendor_id, @vendor_name  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    PRINT ' '  
    SELECT @message = '----- Products From Vendor: ' +   
        @vendor_name  
  
    PRINT @message  
  
    -- Declare an inner cursor based     
    -- on vendor_id from the outer cursor.  
  
    DECLARE product_cursor CURSOR FOR   
    SELECT v.Name  
    FROM Purchasing.ProductVendor pv, Production.Product v  
    WHERE pv.ProductID = v.ProductID AND  
    pv.VendorID = @vendor_id  -- Variable value from the outer cursor  
  
    OPEN product_cursor  
    FETCH NEXT FROM product_cursor INTO @product  
  
    IF @@FETCH_STATUS <> 0   
        PRINT '         <<None>>'       
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
  
        SELECT @message = '         ' + @product  
        PRINT @message  
        FETCH NEXT FROM product_cursor INTO @product  
        END  
  
    CLOSE product_cursor  
    DEALLOCATE product_cursor  
        -- Get the next vendor.  
    FETCH NEXT FROM vendor_cursor   
    INTO @vendor_id, @vendor_name  
END   
CLOSE vendor_cursor;  
DEALLOCATE vendor_cursor;  
```  
  
## <a name="see-also"></a>Consulte também  
 [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursores &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
