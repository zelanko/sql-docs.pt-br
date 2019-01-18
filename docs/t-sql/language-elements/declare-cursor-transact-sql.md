---
title: DECLARE CURSOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECLARE_CURSOR_TSQL
- CURSOR_TSQL
- DECLARE CURSOR
- CURSOR
dev_langs:
- TSQL
helpviewer_keywords:
- DECLARE CURSOR statement
- cursors [SQL Server], attributes
- local cursors [SQL Server]
- nesting cursors
- Transact-SQL cursors, attributes
- global cursors [SQL Server]
ms.assetid: 5a3a27aa-03e8-4c98-a27e-809282379b21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: af3a010f835223a875da7df5028ac1406798c479
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54300093"
---
# <a name="declare-cursor-transact-sql"></a>DECLARE CURSOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  > [!div class="nextstepaction"]
  > [Compartilhe seus comentários sobre o Índice do SQL Docs!](https://aka.ms/sqldocsurvey)

  Define os atributos de um cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)], como seu comportamento de rolagem e a consulta usada para construir o conjunto de resultados no qual o cursor funciona. `DECLARE CURSOR` aceita uma sintaxe fundada no padrão ISO e uma sintaxe que usa um conjunto de extensões [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 É o nome do cursor de servidor do [!INCLUDE[tsql](../../includes/tsql-md.md)] definido. *cursor_name* deve estar em conformidade com as regras de identificadores.  
  
 INSENSITIVE  
 Define um cursor que faz uma cópia temporária dos dados a serem usados por ele. Todas as solicitações para o cursor são respondidas nessa tabela temporária em **tempdb**; portanto, as modificações feitas na tabelas base não são refletidas nos dados retornados pelas buscas feitas nesse cursor, que não permite modificações. Quando a sintaxe de ISO é usada, se `INSENSITIVE` for omitido, exclusões e atualizações confirmadas nestas tabelas subjacentes (por qualquer usuário) serão refletidas em buscas subsequentes.  
  
 SCROLL  
 Especifica que todas as opções de busca (`FIRST`, `LAST`, `PRIOR`, `NEXT`, `RELATIVE`, `ABSOLUTE`) estão disponíveis. Se `SCROLL` não for especificado em um ISO `DECLARE CURSOR`, `NEXT` será a única opção de busca compatível. Não será possível especificar `SCROLL` se `FAST_FORWARD` também estiver especificado. Se `SCROLL` não for especificado, apenas a opção de busca `NEXT` estará disponível e o cursor passará a ser `FORWARD_ONLY`.
  
 *select_statement*  
 É uma instrução `SELECT` padrão que define o conjunto de resultados de um cursor. As palavras-chave `FOR BROWSE` e `INTO` não são permitidas na *select_statement* de uma declaração de cursor.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte o cursor implicitamente em outro tipo se as cláusulas em *select_statement* entram em conflito com a funcionalidade do tipo de cursor solicitado.  
  
 READ ONLY  
 Previne atualizações feitas por este cursor. O cursor não pode ser referenciado em uma cláusula `WHERE CURRENT OF` em um instrução `UPDATE` ou `DELETE`. Essa opção anula a funcionalidade padrão de um cursor para ser atualizado.  
  
 UPDATE [OF *column_name* [**,**...*n*]]  
 Define colunas atualizáveis em um cursor. Se OF <column_name> [, <... n>] for especificada, somente as colunas listadas permitirão modificações. Se `UPDATE` for especificada sem uma lista de colunas, todas as colunas poderão ser atualizadas.  
  
*cursor_name*  
É o nome do cursor de servidor do [!INCLUDE[tsql](../../includes/tsql-md.md)] definido. *cursor_name* deve estar em conformidade com as regras de identificadores.  
  
LOCAL  
Especifica que o escopo do cursor é local para o lote, procedimento armazenado ou gatilho no qual o cursor foi criado. O nome de cursor só é válido dentro desse escopo. O cursor pode ser referenciado por meio de variáveis de cursor local no lote, no procedimento armazenado ou no gatilho ou em um parâmetro `OUTPUT` do procedimento armazenado. Um parâmetro `OUTPUT` é usado para repassar o cursor local para o lote de chamada, o procedimento armazenado ou o gatilho, que pode atribuir o parâmetro a uma variável do cursor para fazer referência ao cursor após o procedimento armazenado terminar. O cursor é implicitamente desalocado quando o lote, o procedimento armazenado ou o gatilho é encerrado, a menos que o cursor tenha sido repassado como um parâmetro `OUTPUT`. Se for repassado em um parâmetro `OUTPUT`, o cursor será desalocado quando a última variável que faz referência a ele for desalocada ou extrapolar o escopo.  
  
GLOBAL  
Especifica que o escopo do cursor é global para a conexão. O nome do cursor pode ser referenciado em qualquer procedimento armazenado ou lote executado pela conexão. O cursor só é desalocado implicitamente na desconexão.  
  
> [!NOTE]  
>  Se nem `GLOBAL` nem `LOCAL` forem especificados, o padrão será controlado pela definição da opção **padronizar para cursor local** do banco de dados.  
  
FORWARD_ONLY  
Especifica se o cursor só pode se mover para frente e ser rolado da primeira à última linha. `FETCH NEXT` é a única opção de busca compatível. Todas as instruções insert, update e delete feitas pelo usuário atual ou confirmadas por outros usuários que afetam as linhas no conjunto de resultados são visíveis como as linhas buscadas. Porém, como o cursor não podem ser revertido, as alterações feitas nas linhas no banco de dados depois que a linha foi buscada não são visíveis pelo cursor. Cursores somente de avanço são dinâmicos por padrão, o que significa que todas as alterações são detectadas conforme a linha atual é processada. Isso permite uma abertura do cursor mais rápida e que o conjunto de resultados exiba as atualizações feitas nas tabelas subjacentes. Embora os cursores somente de avanço não sejam compatíveis com rolagem para trás, os aplicativos podem retornar ao início do conjunto de resultados fechando e reabrindo o cursor. Se `FORWARD_ONLY` for especificado sem as palavras-chave `STATIC`, `KEYSET` ou `DYNAMIC`, o cursor operará como um cursor dinâmico. Quando nem `FORWARD_ONLY` nem `SCROLL` é especificado, `FORWARD_ONLY` é o padrão, a menos que as palavras-chave `STATIC`, `KEYSET` ou `DYNAMIC` sejam especificadas. Os cursores `STATIC`, `KEYSET` e `DYNAMIC` utilizam `SCROLL` como padrão. Ao contrário de APIs de banco de dados, como ODBC e ADO, `FORWARD_ONLY` dá suporte aos cursores `STATIC`, `KEYSET` e `DYNAMIC` [!INCLUDE[tsql](../../includes/tsql-md.md)].  
   
 STATIC  
Especifica que o cursor sempre exibe o conjunto de resultados como ele era quando o cursor foi aberto pela primeira vez e faz uma cópia temporária dos dados a serem usados pelo cursor. Todas as solicitações para o cursor são respondidas dessa tabela temporária em **tempdb**. Portanto, inserções, atualizações e exclusões feitas na tabelas base não são refletidas nos dados retornados pelas buscas feitas nesse cursor e esse cursor não detecta as alterações feitas à associação, à ordem ou aos valores do conjunto de resultados depois que o cursor é aberto. Cursores estáticos podem detectar as próprias atualizações, exclusões e inserções, embora não precisem fazer isso. Por exemplo, suponha que um cursor estático busque uma linha e outro aplicativo então atualize a linha. Se o aplicativo buscar novamente a linha do cursor estático, os valores que ele verá estarão inalterados, apesar das alterações feitas por outro aplicativo. Há suporte para todos os tipos de rolagem. 
  
KEYSET  
Especifica que a associação e a ordem de linhas no cursor são fixas, quando o cursor é aberto. O conjunto de chaves que identificam exclusivamente as linhas é construído em uma tabela no **tempdb**, conhecido como **keyset**. Esse cursor fornece funcionalidades entre um cursor dinâmico e um cursor estático em sua capacidade de detectar alterações. Como um cursor estático, ele nem sempre detecta alterações à associação e à ordem do conjunto de resultados. Como um cursor dinâmico, ele detecta alterações aos valores de linhas no conjunto de resultados. Os cursores controlados por conjuntos de chaves são controlados por um conjunto exclusivo de identificadores (chaves) conhecido como conjunto de chaves. As chaves são criadas a partir de um conjunto de colunas, que identificam exclusivamente as linhas no conjunto de resultados. O conjunto de chaves é o conjunto de valores de chave de todas as linhas retornadas pela instrução de consulta. Com cursores controlados por conjunto de chaves, uma chave é criada e salva para cada linha do cursor e armazenada na estação de trabalho cliente ou no servidor. Quando você acessa cada linha, a chave armazenada é usada para buscar os valores de dados atual da fonte de dados. Em um cursor controlado por conjunto de chaves, a associação do conjunto de resultados é congelada quando o conjunto de chaves está completamente preenchido. Depois disso, adições ou atualizações que afetem a associação não farão parte do resultado definido até que ele seja reaberto. Alterações nos valores de dados (feitas por outros processos ou pelo proprietário do conjunto de chaves) são visíveis conforme o usuário rola pelo conjunto de resultados:
-  Se uma linha for excluída, uma tentativa de buscar a linha retornará um `@@FETCH_STATUS` de -2 porque a linha excluída aparecerá como uma lacuna no conjunto de resultados. A chave para a linha existe no conjunto de chaves, mas a linha não existe mais no conjunto de resultados. 
-  Inserções feitas fora do cursor (por outros processos) serão visíveis apenas se o cursor for fechado e reaberto. Inserções feitas de dentro do cursor são visíveis no final do conjunto de resultados.
-  Atualização de valores de chave externos ao cursor lembram a exclusão de uma linha antiga, seguida de uma inserção de uma nova linha. A linha com os novos valores não é visível e as tentativas de buscar a linha com os valores antigos retornam um `@@FETCH_STATUS` igual a -2. Os novos valores ficarão visíveis se a atualização for feita por meio do cursor especificando a cláusula `WHERE CURRENT OF`. 

> [!NOTE]  
> Se a consulta referencia ao menos uma tabela sem um índice exclusivo, o cursor controlado por conjunto de chaves é convertido a um cursor estático.  
  
DYNAMIC  
Define um cursor que reflete todas as alterações de dados feitas às linhas em seu conjunto de resultados conforme você rola o cursor e busque um novo registro, não importa se as alterações ocorrem de dentro do cursor ou são feitas por outros usuários fora do cursor. Portanto, todas as instruções insert, update e delete feitas por todos os usuários são visíveis por meio do cursor. Os valores de dados, a ordem e a associação das linhas podem ser alterados em cada busca. Não há suporte para a opção de buscar `ABSOLUTE` com cursores dinâmicos. As atualizações feitas fora do cursor não são visíveis até serem confirmadas (a menos que o nível de isolamento da transação do cursor esteja definido como `UNCOMMITTED`). Por exemplo, suponha que um cursor dinâmico busque duas linhas e outro aplicativo então atualize uma dessas linhas e exclua a outra. Se o cursor dinâmico então buscar essas linhas, ele não localizará a linha excluída, mas exibirá os novos valores para a linha atualizada. 
  
FAST_FORWARD  
Especifica um cursor `FORWARD_ONLY`, `READ_ONLY` com otimizações de desempenho habilitadas. Não será possível especificar `FAST_FORWARD` se `SCROLL` ou `FOR_UPDATE` também estiver especificado. Esse tipo de cursor não permite modificações de dados de dentro do cursor.  
  
> [!NOTE]  
> `FAST_FORWARD` e `FORWARD_ONLY` podem ser usados na mesma instrução `DECLARE CURSOR`.  
  
READ_ONLY  
Previne atualizações feitas por este cursor. O cursor não pode ser referenciado em uma cláusula `WHERE CURRENT OF` em um instrução `UPDATE` ou `DELETE`. Essa opção anula a funcionalidade padrão de um cursor para ser atualizado.  
  
SCROLL_LOCKS  
Especifica se atualizações posicionadas ou exclusões feitas pelo cursor têm garantia de êxito. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloqueia as linhas à medida que são lidas no cursor para assegurar a disponibilidade para modificações posteriores. Não será possível especificar `SCROLL_LOCKS` se `FAST_FORWARD` ou `STATIC` também estiver especificado.  
  
OPTIMISTIC  
Especifica que as atualizações posicionadas e exclusões realizadas pelo cursor não terão êxito se a linha tiver sido atualizada desde que foi lida no cursor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não bloqueia linhas à medida que são lidas no cursor. Em vez disso, ele usa comparações de valores de coluna **timestamp** ou um valor de soma de verificação se a tabela não tem nenhuma coluna **timestamp**, para determinar se a linha foi modificada depois de ser lida no cursor. Se a linha tiver sido modificada, a tentativa de atualização ou exclusão posicionada falhará. Não será possível especificar `OPTIMISTIC` se `FAST_FORWARD` também estiver especificado.  
  
 TYPE_WARNING  
 Especifica que uma mensagem de aviso é enviada ao cliente quando o cursor é convertido implicitamente em outro a partir do tipo solicitado.  
  
 *select_statement*  
 É uma instrução SELECT padrão que define o conjunto de resultados de um cursor. As palavras-chave `COMPUTE`, `COMPUTE BY`, `FOR BROWSE` e `INTO` não são permitidas na *select_statement* de uma declaração de cursor.  
  
> [!NOTE]  
> Você pode usar uma dica de consulta dentro de uma declaração de cursor, porém, se você também usar a cláusula `FOR UPDATE OF`, especifique `OPTION (<query_hint>)` após de `FOR UPDATE OF`.  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte o cursor implicitamente em outro tipo se as cláusulas em *select_statement* entram em conflito com a funcionalidade do tipo de cursor solicitado. Para obter mais informações, consulte Conversões implícitas de cursor  
  
FOR UPDATE [OF *column_name* [**,**...*n*]]  
Define colunas atualizáveis em um cursor. Se `OF <column_name> [, <... n>]` for fornecido, somente as colunas listadas permitirão modificações. Se `UPDATE` for especificado sem uma lista de colunas, todas as colunas poderão ser atualizadas, a não ser que a opção de simultaneidade `READ_ONLY` seja especificada.  
  
## <a name="remarks"></a>Remarks  
`DECLARE CURSOR` define os atributos de um cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)], como seu comportamento de rolagem e a consulta usada para criar o conjunto de resultados no qual o cursor funciona. A instrução `OPEN` popula o conjunto de resultados e `FETCH` retorna uma linha do conjunto de resultados. A instrução `CLOSE` libera o conjunto de resultados atual associado ao cursor. A instrução `DEALLOCATE` libera os recursos usados pelo cursor.  
  
O primeiro formulário da instrução `DECLARE CURSOR` usa a sintaxe ISO para declarar comportamentos do cursor. O segundo formulário do `DECLARE CURSOR` usa extensões [!INCLUDE[tsql](../../includes/tsql-md.md)] que lhe permitem definir cursores com os mesmos tipos de cursor usados nas funções do cursor de API do banco de dados de ODBC ou ADO.  
  
Você não pode misturar os dois formulários. Se você especificar as palavras-chave `SCROLL` ou `INSENSITIVE` antes da palavra-chave `CURSOR`, não poderá usar nenhuma palavra-chave entre as palavras-chave `CURSOR` e `FOR <select_statement>`. Se você especificar quaisquer palavras-chave entre `CURSOR` e `FOR <select_statement>`, não poderá especificar `SCROLL` ou `INSENSITIVE` antes da palavra-chave `CURSOR`.  
  
Se um `DECLARE CURSOR` usando a sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] não especifica `READ_ONLY`, `OPTIMISTIC` ou `SCROLL_LOCKS`, o padrão é o seguinte:  
  
-   Se a instrução `SELECT` não der suporte para atualizações (permissões insuficientes, acesso a tabelas remotas que não dão suporte a atualizações e assim por diante), o cursor será `READ_ONLY`.  
  
-   Os cursores `STATIC` e `FAST_FORWARD` utilizam `READ_ONLY` como padrão.  
  
-   Os cursores `DYNAMIC` e `KEYSET` utilizam `OPTIMISTIC` como padrão.  
  
Nomes de cursor só podem ser referenciados através de outras instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Eles não podem ser referenciados através de funções da API do banco de dados. Por exemplo, depois de declarar um cursor, o nome de cursor não pode ser referenciado das funções ou métodos OLE DB, ODBC ou ADO. As linhas de cursor não podem ser pesquisadas com as funções ou métodos de busca das APIs; as linhas só podem ser buscadas através de instruções FETCH [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
Depois que um cursor ter sido declarado, esses procedimentos armazenados do sistema podem ser usados para determinar as características do cursor.  
  
|Procedimentos armazenados do sistema|Descrição|  
|------------------------------|-----------------|  
|**sp_cursor_list**|Retorna uma lista de cursores atualmente visíveis na conexão e seus atributos.|  
|**sp_describe_cursor**|Descreve os atributos de um cursor, por exemplo, se ele é de somente avanço ou de rolagem.|  
|**sp_describe_cursor_columns**|Descreve os atributos das colunas no conjunto de resultados do cursor.|  
|**sp_describe_cursor_tables**|Descreve as tabelas base acessadas pelo cursor.|  
  
 Variáveis podem ser usadas como parte da *select_statement* que declara um cursor. Valores de variáveis de cursor não se alteram depois que um cursor é declarado.  
  
## <a name="permissions"></a>Permissões  
 Permissões de `DECLARE CURSOR` seguem o padrão para todo usuário que tem permissões `SELECT` para exibições, tabelas e colunas usadas no cursor.
 
## <a name="limitations-and-restrictions"></a>Limitações e Restrições

Não é possível usar cursores nem gatilhos em uma tabela com um índice columnstore clusterizado. Essa restrição não se aplica a índices columnstore não clusterizados. É possível usar cursores e gatilhos em uma tabela com um índice columnstore não clusterizado. 
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-simple-cursor-and-syntax"></a>A. Usando a sintaxe e o cursor simples  

O conjunto de resultados gerado na abertura deste cursor inclui todas as linhas e todas as colunas na tabela. Este cursor pode ser atualizado e todas as atualizações e exclusões são representadas em buscas feitas no cursor. `FETCH NEXT` é a única busca disponível porque a opção `SCROLL` não foi especificada.  
 
```sql  
DECLARE vend_cursor CURSOR  
    FOR SELECT * FROM Purchasing.Vendor  
OPEN vend_cursor  
FETCH NEXT FROM vend_cursor;  
```  
  
### <a name="b-using-nested-cursors-to-produce-report-output"></a>b. Usando cursores aninhados para produzir saída de relatório  
 O exemplo a seguir mostra como cursores podem ser aninhados para produzir relatórios complexos. O cursor interno é declarado para cada vendedor.  
  
```sql  
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
  
## <a name="see-also"></a>Consulte Também  
 [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursores &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
