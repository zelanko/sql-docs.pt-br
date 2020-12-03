---
description: Dados hierárquicos (SQL Server)
title: Dados hierárquicos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [SQL Server], tables to support
- hierarchyid [Database Engine], concepts
- hierarchical tables [Database Engine]
- SqlHierarchyId
- hierarchyid [Database Engine]
- hierarchical queries [SQL Server], using hierarchyid data type
ms.assetid: 19aefa9a-fbc2-4b22-92cf-67b8bb01671c
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 994adada7ecef047967b07d03cd2a9a129c8f227
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91869057"
---
# <a name="hierarchical-data-sql-server"></a>Dados hierárquicos (SQL Server)

[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]

  O tipo de dados interno **hierarchyid** facilita o armazenamento e a consulta de dados hierárquicos. **hierarchyid** foi otimizado para representar árvores, que são o tipo mais comum de dados hierárquicos.  
  
 Os dados hierárquicos são definidos como um conjunto de itens de dados mutuamente relacionados por relações hierárquicas. As relações hierárquicas existem onde um item de dados é o pai de outro item. Exemplos dos dados hierárquicos que geralmente são armazenados em bancos de dados incluem o seguinte:  
  
-   Uma estrutura organizacional  
  
-   Um sistema de arquivos  
  
-   Um conjunto de tarefas em um projeto  
  
-   Uma taxonomia de termos de linguagem  
  
-   Um gráfico de links entre páginas da Web  
  
 Use [hierarchyid](../t-sql/data-types/hierarchyid-data-type-method-reference.md) como o tipo de dados para criar tabelas com uma estrutura hierárquica ou para descrever a estrutura hierárquica dos dados armazenados em outro local. Use as [funções hierarchyid](../t-sql/data-types/hierarchyid-data-type-method-reference.md) no [!INCLUDE[tsql](../includes/tsql-md.md)] para consultar e gerenciar dados hierárquicos.  
  
##  <a name="key-properties-of-hierarchyid"></a><a name="keyprops"></a> Propriedades chave de hierarchyid  
 Um valor do tipo de dados **hierarchyid** representa uma posição em uma hierarquia de árvore. Os valores para **hierarchyid** têm as seguintes propriedades:  
  
-   Extremamente compacto  
  
     O número médio de bits necessários para representar um nó em uma árvore com *n* nós depende da média de fanout (o número médio de filhos de um nó). Para fanouts pequenos, o tamanho (0-7) é de aproximadamente 6\*logA *n* bits, em que A é o fanout médio. Um nó em uma hierarquia organizacional de 100.000 pessoas com um fanout médio de 6 níveis usa cerca de 38 bits. Isso é arredondado para 40 bits, ou 5 bytes, para armazenamento.  
  
-   A comparação está na ordem de profundidade  
  
     Dados dois valores de **hierarchyid****a** r **b**, **a<b** significa que a vem antes de b em uma passagem de profundidade da árvore. Índices em tipos de dados **hierarchyid** estão na ordem de profundidade e os nós próximos uns dos outros em uma passagem de profundidade são armazenados próximos um ao outro. Por exemplo, os filhos de um registro são armazenados adjacentes àquele registro.  
  
-   Suporte a inserções e exclusões arbitrárias  
  
     Usando o método [GetDescendant](../t-sql/data-types/getdescendant-database-engine.md) , é sempre possível gerar um irmão à direita de qualquer nó determinado, à esquerda de qualquer nó determinado ou entre dois irmãos. A propriedade de comparação é mantida quando um número arbitrário de nós é inserido ou excluído da hierarquia. A maioria das inserções e exclusões preserva a propriedade de densidade. Porém, inserções entre dois nós produzirão valores hierarchyid com uma representação ligeiramente menos compacta.  
  
  
##  <a name="limitations-of-hierarchyid"></a><a name="limits"></a> Limitações de hierarchyid  
 O tipo de dados **hierarchyid** tem as seguintes limitações:  
  
-   Uma coluna de tipo **hierarchyid** não representa automaticamente uma árvore. Depende do aplicativo gerar e atribuir valores **hierarchyid** de maneira que a relação desejada entre as linhas seja refletida nos valores. Alguns aplicativos podem ter uma coluna do tipo **hierarchyid** que indica o local em uma hierarquia definida em outra tabela.  
  
-   Depende de o aplicativo gerenciar a simultaneidade na geração e atribuição de valores **hierarchyid** . Não há nenhuma garantia de que os valores **hierarchyid** em uma coluna sejam exclusivos a menos que o aplicativo use uma restrição de chave exclusiva ou force sua exclusividade em sua própria lógica.  
  
-   Relações hierárquicas representadas por valores **hierarchyid** não são impostas como uma relação de chave estrangeira. É possível e, às vezes, apropriado ter uma relação hierárquica onde A tem um filho B e, depois, A é excluído deixando B com uma relação para um registro inexistente. Se esse comportamento for inaceitável, o aplicativo deverá fazer a consulta por descendentes antes de excluir os pais.  
  
  
##  <a name="when-to-use-alternatives-to-hierarchyid"></a><a name="alternatives"></a> Quando usar alternativas para hierarchyid  
 As duas alternativas para **hierarchyid** para representar dados hierárquicos são:  
  
-   Pai/filho  
  
-   XML  
  
 A **hierarchyid** é geralmente superior a essas alternativas. Porém, a seguir há situações específicas detalhadas em que as alternativas são provavelmente superiores.  
  
### <a name="parentchild"></a>Pai/filho  
 Ao usar a abordagem Pai/Filho, cada linha contém uma referência ao pai. A tabela a seguir define uma tabela típica usada para conter as linhas pai e filho em uma relação Pai/Filho:  
  
```sql
USE AdventureWorks2012 ;  
GO  
  
CREATE TABLE ParentChildOrg  
   (  
    BusinessEntityID int PRIMARY KEY,  
    ManagerId int REFERENCES ParentChildOrg(BusinessEntityID),  
    EmployeeName nvarchar(50)   
   ) ;  
GO  
```  
  
 Comparando pai/filho e **hierarchyid** em operações comuns  
  
-   Consultas de subárvore são significativamente mais rápidas com **hierarchyid**.  
  
-   Consultas de descendente direto são ligeiramente mais lentas com **hierarchyid**.  
  
-   A movimentação de nós não folha é mais lenta com **hierarchyid**.  
  
-   A inserção de nós não folha e a inserção ou a movimentação de nós folha têm a mesma complexidade com **hierarchyid**.  
  
 Pai/Filho pode ser superior quando existem as seguintes:  
  
-   O tamanho da chave é crítico. Para o mesmo número de nós, um valor **hierarchyid** é igual ou maior que um valor da família de inteiros (**smallint**, **int**, **bigint**). Essa é a única razão para usar Pai/Filho em casos raros, porque **hierarchyid** tem localidade significativamente melhor de E/S e complexidade de CPU que as expressões de tabela comuns exigidas quando você está usando uma estrutura Pai/Filho.  
  
-   Consultas raramente examinam por seções da hierarquia. Em outras palavras, as consultas normalmente se dirigem apenas a um único ponto na hierarquia. Nesses casos, a colocação não é importante. Por exemplo, Pai/Filho é superior quando a tabela de organização é usada somente para processar a folha de pagamento de funcionários individuais.  
  
-   Subárvores de não folha mudam frequentemente e o desempenho é muito importante. Em uma representação pai/filho, alterando o local de uma linha em uma hierarquia afeta uma linha única. Alterar o local de uma linha em um uso de **hierarchyid** afeta *n* linhas, em que *n* é número de nós na subárvore sendo movida.  
  
     Se as subárvores sem folha mudarem frequentemente e o desempenho for importante, mas a maioria das mudanças estiver em um nível bem definido da hierarquia, considere dividir os níveis superiores e inferiores em duas hierarquias. Isso faz todas as mudanças em níveis de folha da hierarquia mais alta. Por exemplo, considere uma hierarquia de sites hospedados por um serviço. Sites contêm muitas páginas organizadas de uma maneira hierárquica. Sites hospedados poderiam ser movidos a outros locais na hierarquia do site, mas as páginas subordinadas raramente seriam reorganizadas. Isso poderia ser representado por:  
  
    ```sql
    CREATE TABLE HostedSites   
       (  
        SiteId hierarchyid, PageId hierarchyid  
       ) ;  
    GO  
    ```  
  
  
### <a name="xml"></a>XML  
 Um documento XML é uma árvore e, portanto, uma instância de tipo de dados XML única pode representar uma hierarquia completa. No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] quando um índice XML é criado, valores **hierarchyid** são usados internamente para representar a posição na hierarquia.  
  
 Usar um tipo de dados XML pode ser vantajoso quando todos os seguintes itens forem verdadeiros:  
  
-   A hierarquia completa é sempre armazenada e recuperada.  
  
-   Os dados são consumidos no formato XML pelo aplicativo.  
  
-   Pesquisas de predicado são extremamente limitadas e não têm de desempenho crítico.  
  
 Por exemplo, se um aplicativo controla várias organizações, ele sempre armazena e recupera a hierarquia organizacional completa, e não faz a consulta em uma organização única, uma tabela do formulário a seguir faria sentido:  
  
```sql
CREATE TABLE XMLOrg   
    (  
    Orgid int,  
    Orgdata xml  
    ) ;  
GO  
```  
  
  
##  <a name="indexing-strategies-for-hierarchical-data"></a><a name="indexing"></a> Estratégias de indexação para dados hierárquicos  
 Há duas estratégias para indexar dados hierárquicos:  
  
-   **Profundidade**  
  
     Um índice de profundidade armazena as linhas em uma subárvore próximas umas das outras. Por exemplo, todos os funcionários que se reportam a gerente são armazenados próximos do registro de seus gerentes.  
  
     Em um índice por profundidade, todos os nós na subárvore de um nó são colocados. Índices por profundidade são portanto eficientes para responder consultas sobre subárvores, como "Localizar todos os arquivos nesta pasta e subpastas""""""""".  
  
-   **Amplitude**  
  
     Uma amplitude armazena as linhas de cada nível da hierarquia juntas. Por exemplo, os registros de funcionários que se reportam diretamente ao mesmo gerente são armazenados próximos um do outro.  
  
     Em um índice por amplitude todos os filhos diretos de um nós são colocados. Índices por amplitude são, portanto, eficientes para responder consultas sobre filhos diretos, como "Localizar todos os empregados que se reportam diretamente a esse gerente".  
  
 Ter opções por profundidade, por amplitude, ou ambas, e qual delas tornar a chave de clustering (se houver), depende da importância relativa dos tipos de consultas anteriores e da importância relativa de operações SELECT versus DML. Para obter um exemplo detalhado de estratégias de indexação, consulte [Tutorial: Usando o tipo de dados HierarchyId](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md).  
  
  
### <a name="creating-indexes"></a>Criando índices  
 O método GetLevel() pode ser usado para criar uma ordem por amplitude. No exemplo seguinte, são criados índices por amplitude e por profundidade:  
  
```sql
USE AdventureWorks2012 ;   -- wmimof
GO  
  
CREATE TABLE Organization  
   (  
    BusinessEntityID hierarchyid,  
    OrgLevel as BusinessEntityID.GetLevel(),   
    EmployeeName nvarchar(50) NOT NULL  
   ) ;  
GO  
  
CREATE CLUSTERED INDEX Org_Breadth_First   
    ON Organization(OrgLevel,BusinessEntityID) ;  
GO  
  
CREATE UNIQUE INDEX Org_Depth_First   
    ON Organization(BusinessEntityID) ;  
GO  
```  
  
  
## <a name="examples"></a>Exemplos  
  
### <a name="simple-example"></a>Exemplo simples  
 O exemplo a seguir é intencionalmente simplificado para ajudá-lo a começar. Primeiro crie uma tabela para manter alguns dados geográficos.  
  
```sql
CREATE TABLE SimpleDemo  
(
    Level hierarchyid NOT NULL,  
    Location nvarchar(30) NOT NULL,  
    LocationType nvarchar(9) NULL
);
```  
  
 Agora insira dados para alguns continentes, países, estados e cidades.  
  
```sql
INSERT SimpleDemo  
    VALUES   
('/1/', 'Europe', 'Continent'),  
('/2/', 'South America', 'Continent'),  
('/1/1/', 'France', 'Country'),  
('/1/1/1/', 'Paris', 'City'),  
('/1/2/1/', 'Madrid', 'City'),  
('/1/2/', 'Spain', 'Country'),  
('/3/', 'Antarctica', 'Continent'),  
('/2/1/', 'Brazil', 'Country'),  
('/2/1/1/', 'Brasilia', 'City'),  
('/2/1/2/', 'Bahia', 'State'),  
('/2/1/2/1/', 'Salvador', 'City'),  
('/3/1/', 'McMurdo Station', 'City');  
```  
  
 Selecione os dados, adicionando uma coluna que converta os dados de nível em um valor de texto de fácil compreensão. Essa consulta também ordena o resultado pelo tipo de dados **hierarchyid** .  
  
```sql
SELECT CAST(Level AS nvarchar(100)) AS [Converted Level], *   
    FROM SimpleDemo ORDER BY Level;  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```  
Converted Level  Level     Location         LocationType  
/1/              0x58      Europe           Continent  
/1/1/            0x5AC0    France           Country  
/1/1/1/          0x5AD6    Paris            City  
/1/2/            0x5B40    Spain            Country  
/1/2/1/          0x5B56    Madrid           City  
/2/              0x68      South America    Continent  
/2/1/            0x6AC0    Brazil           Country  
/2/1/1/          0x6AD6    Brasilia         City  
/2/1/2/          0x6ADA    Bahia            State  
/2/1/2/1/        0x6ADAB0  Salvador         City  
/3/              0x78      Antarctica       Continent  
/3/1/            0x7AC0    McMurdo Station  City  
```  
  
 Observe que a hierarquia tem uma estrutura válida, embora ela não seja consistente internamente. Bahia é o único estado. Ele aparece na hierarquia como um par da cidade de Brasília. Da mesma forma, a estação McMurdo não tem um país pai. Os usuários devem decidir se este tipo de hierarquia é apropriado para seu uso.  
  
 Adicione outra linha e selecione os resultados.  
  
```sql
INSERT SimpleDemo  
    VALUES ('/1/3/1/', 'Kyoto', 'City'), ('/1/3/1/', 'London', 'City');  
SELECT CAST(Level AS nvarchar(100)) AS [Converted Level], * FROM SimpleDemo ORDER BY Level;  
```  
  
 Isso demonstra mais problemas em potencial. Kyoto pode ser inserido como o nível `/1/3/1/` , embora não exista um nível pai `/1/3/`. Londres e Kyoto têm o mesmo valor para **hierarchyid**. Além disso, os usuários devem decidir se este tipo de hierarquia é apropriado para seu uso, e os valores do bloco que são inválidos para seu uso.  
  
 Além disso, essa tabela não usou a parte superior da hierarquia `'/'`. Ela foi omitida pois não há um pai comum de todos os continentes. Para adicionar um, adicione o planeta inteiro.  
  
```sql
INSERT SimpleDemo  
    VALUES ('/', 'Earth', 'Planet');  
```  
  
##  <a name="related-tasks"></a><a name="tasks"></a> Tarefas relacionadas  
  
###  <a name="migrating-from-parentchild-to-hierarchyid"></a><a name="migrating"></a> Migrando de Pai/Filho para hierarchyid  
 A maioria das árvores é representada usando Pai/Filho. O modo mais fácil de migrar de uma estrutura Pai/Filho para uma tabela usando **hierarchyid** é usar uma coluna ou uma tabela temporária para manter o controle do número de nós em cada nível da hierarquia. Para obter um exemplo de migração de uma tabela Pai/Filho, consulte a lição 1 do [Tutorial: Usando o tipo de dados HierarchyId](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md).  
  
  
###  <a name="managing-a-tree-using-hierarchyid"></a><a name="BKMK_ManagingTrees"></a> Gerenciando uma árvore com hierarchyid  
 Embora uma coluna **hierarchyid** não represente necessariamente uma árvore, um aplicativo pode garantir facilmente que essa representação ocorra.  
  
-   Para gerar novos valores, execute uma das ações abaixo:  
  
    -   Mantenha registro do último número filho da linha pai.  
  
    -   Compute o último filho. Para executar esse procedimento com eficácia, é necessário um índice de primeira amplitude.  
  
-   Imponha a exclusividade criando um índice exclusivo na coluna, talvez como parte de uma chave de clustering. Para assegurar a inserção de valores únicos, execute uma das ações a seguir:  
  
    -   Detecte as falhas de violação de chave exclusiva e tente novamente.  
  
    -   Determine a exclusividade de cada novo nó filho e insira-o como parte de uma transação serializável.  
  
  
#### <a name="example-using-error-detection"></a>Exemplo utilizando detecção de erro  
 No exemplo a seguir, o código de exemplo computa o novo valor filho de **EmployeeId** detectando depois quaisquer violações de chave para retorná-las ao marcador **INS_EMP** para computar novamente o valor de **EmployeeId** na nova linha:  
  
```sql
USE AdventureWorks ;  
GO  
  
CREATE TABLE Org_T1  
   (  
    EmployeeId hierarchyid PRIMARY KEY,  
    OrgLevel AS EmployeeId.GetLevel(),  
    EmployeeName nvarchar(50)   
   ) ;  
GO  
  
CREATE INDEX Org_BreadthFirst ON Org_T1(OrgLevel, EmployeeId);
GO  
  
CREATE PROCEDURE AddEmp(@mgrid hierarchyid, @EmpName nvarchar(50) )   
AS  
BEGIN  
    DECLARE @last_child hierarchyid;
INS_EMP:   
    SELECT @last_child = MAX(EmployeeId) FROM Org_T1   
        WHERE EmployeeId.GetAncestor(1) = @mgrid;
    INSERT INTO Org_T1 (EmployeeId, EmployeeName)  
        SELECT @mgrid.GetDescendant(@last_child, NULL), @EmpName;
-- On error, return to INS_EMP to recompute @last_child  
IF @@error <> 0 GOTO INS_EMP   
END ;  
GO  
```  
  
  
#### <a name="example-using-a-serializable-transaction"></a>Exemplo utilizando uma transação serializável  
 O índice **Org_BreadthFirst** verifica se a determinação de **\@last_child** usa uma busca de intervalo. Além de outros casos de erro que um aplicativo tenta verificar, uma violação da chave duplicada depois da inserção indica uma tentativa de adicionar vários funcionários com a mesma ID e, portanto, **\@last_child** deve ser novamente computado. O código a seguir computa o novo valor de nó dentro de uma transação serializável:  
  
```sql
CREATE TABLE Org_T2  
    (  
    EmployeeId hierarchyid PRIMARY KEY,  
    LastChild hierarchyid,   
    EmployeeName nvarchar(50)   
    ) ;  
GO  
  
CREATE PROCEDURE AddEmp(@mgrid hierarchyid, @EmpName nvarchar(50))   
AS  
BEGIN  
DECLARE @last_child hierarchyid  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
BEGIN TRANSACTION   
  
SELECT @last_child  =  EmployeeId.GetDescendant(LastChild,NULL)
FROM Org_T2
WHERE EmployeeId = @mgrid

UPDATE Org_T2 SET LastChild = @last_child  WHERE EmployeeId = @mgrid

INSERT Org_T2 (EmployeeId, EmployeeName)   
    VALUES(@last_child, @EmpName)  
COMMIT  
END ;  
```  
  
 O código a seguir popula a tabela com três linhas e retorna os resultados:  
  
```sql
INSERT Org_T2 (EmployeeId, EmployeeName)   
    VALUES(hierarchyid::GetRoot(), 'David') ;  
GO  
AddEmp 0x , 'Sariya'  
GO  
AddEmp 0x58 , 'Mary'  
GO  
SELECT * FROM Org_T2  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```  
EmployeeId LastChild EmployeeName  
---------- --------- ------------  
0x        0x58       David  
0x58      0x5AC0     Sariya  
0x5AC0    NULL       Mary  
```  
  
  
###  <a name="enforcing-a-tree"></a><a name="BKMK_EnforcingTrees"></a> Aplicando uma árvore  
 Os exemplos anteriores ilustram como um aplicativo pode assegurar a manutenção de uma árvore. Para impor uma árvore usando restrições, uma coluna computada que define o pai de cada nó pode ser criada com uma restrição de chave estrangeira na ID de chave primária.  
  
```sql
CREATE TABLE Org_T3  
(  
   EmployeeId hierarchyid PRIMARY KEY,  
   ParentId AS EmployeeId.GetAncestor(1) PERSISTED    
      REFERENCES Org_T3(EmployeeId),  
   LastChild hierarchyid,   
   EmployeeName nvarchar(50)  
)  
GO  
```  
  
 O método de impor uma relação é preferido quando o código que não é confiável para manter a árvore hierárquica tiver acesso DML direto à tabela. No entanto, esse método pode reduzir o desempenho porque a restrição deve ser verificada em todas as operações DML.  
  
  
###  <a name="finding-ancestors-by-using-the-clr"></a><a name="findclr"></a> Localizando ancestrais usando o CLR  
 Uma operação comum que envolve dois nós em uma hierarquia é encontrar o mais baixo ancestral comum. Isso pode ser escrito em [!INCLUDE[tsql](../includes/tsql-md.md)] ou CLR, porque o tipo **hierarchyid** está disponível em ambos. CLR é recomendado porque o desempenho será mais rápido.  
  
 Use o código CLR a seguir para listar os ancestrais e localizar o ancestral comum mais baixo:  
  
```csharp
using System;  
using System.Collections;  
using System.Text;  
using Microsoft.SqlServer.Server;  // SqlFunction Attribute
using Microsoft.SqlServer.Types;   // SqlHierarchyId
  
public partial class HierarchyId_Operations  
{  
    [SqlFunction(FillRowMethodName = "FillRow_ListAncestors")]
    public static IEnumerable ListAncestors(SqlHierarchyId h)
    {  
        while (!h.IsNull)  
        {  
            yield return (h);  
            h = h.GetAncestor(1);  
        }  
    }  
    public static void FillRow_ListAncestors(
        Object obj,
        out SqlHierarchyId ancestor
        )
    {  
        ancestor = (SqlHierarchyId)obj;  
    }  
  
    public static HierarchyId CommonAncestor(
        SqlHierarchyId h1,
        HierarchyId h2
        )  
    {  
        while (!h1.IsDescendantOf(h2))  
            h1 = h1.GetAncestor(1);  
  
        return h1;  
    }  
}  
```  
  
 Para usar os métodos **ListAncestor** e **CommonAncestor** nos exemplos [!INCLUDE[tsql](../includes/tsql-md.md)] a seguir, construa a DLL e crie o assembly **HierarchyId_Operations** em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] executando um código semelhante ao seguinte:  
  
```sql
CREATE ASSEMBLY HierarchyId_Operations   
    FROM '<path to DLL>\ListAncestors.dll';
GO  
```  
  
  
###  <a name="listing-ancestors"></a><a name="ancestors"></a> Listando os ancestrais  
 A criação de uma lista de ancestrais de um nó é uma operação comum; por exemplo, para mostrar a posição em uma organização. Uma das formas de fazer isso é usar uma função com valor de tabela usando a classe **HierarchyId_Operations** definida acima:  
  
 Usando [!INCLUDE[tsql](../includes/tsql-md.md)]:  
  
```sql
CREATE FUNCTION ListAncestors (@node hierarchyid)  
RETURNS TABLE (node hierarchyid)  
AS  
EXTERNAL NAME HierarchyId_Operations.HierarchyId_Operations.ListAncestors  
GO  
```  
  
 Exemplo de uso:  
  
```sql
DECLARE @h hierarchyid  
SELECT @h = OrgNode   
FROM HumanResources.EmployeeDemo    
WHERE LoginID = 'adventure-works\janice0' -- /1/1/5/2/  
  
SELECT LoginID, OrgNode.ToString() AS LogicalNode  
FROM HumanResources.EmployeeDemo AS ED  
JOIN ListAncestors(@h) AS A   
   ON ED.OrgNode = A.Node  
GO  
```  
  
  
###  <a name="finding-the-lowest-common-ancestor"></a><a name="lowestcommon"></a> Localizando o mais baixo ancestral comum  
 Usando a classe **HierarchyId_Operations** definida acima, crie a seguinte função [!INCLUDE[tsql](../includes/tsql-md.md)] para localizar o mais baixo ancestral comum que envolva dois nós em uma hierarquia:  
  
```sql
CREATE FUNCTION CommonAncestor (@node1 hierarchyid, @node2 hierarchyid)  
RETURNS hierarchyid  
AS  
EXTERNAL NAME HierarchyId_Operations.HierarchyId_Operations.CommonAncestor  
GO  
```  
  
 Exemplo de uso:  
  
```sql
DECLARE @h1 hierarchyid, @h2 hierarchyid;
  
SELECT @h1 = OrgNode   
FROM  HumanResources.EmployeeDemo   
WHERE LoginID = 'adventure-works\jossef0'; -- Node is /1/1/3/  
  
SELECT @h2 = OrgNode   
FROM HumanResources.EmployeeDemo    
WHERE LoginID = 'adventure-works\janice0'; -- Node is /1/1/5/2/  
  
SELECT OrgNode.ToString() AS LogicalNode, LoginID   
FROM HumanResources.EmployeeDemo    
WHERE OrgNode = dbo.CommonAncestor(@h1, @h2) ;  
```  
  
 O nó resultante é /1/1/  
  
  
###  <a name="moving-subtrees"></a><a name="BKMK_MovingSubtrees"></a> Movendo subárvores  
 Outra operação comum é mover subárvores. O procedimento abaixo usa a subárvore de **\@oldMgr** e a torna (incluindo **\@oldMgr**) uma subárvore de **\@newMgr**.  
  
```sql
CREATE PROCEDURE MoveOrg(@oldMgr nvarchar(256), @newMgr nvarchar(256) )  
AS  
BEGIN  
DECLARE @nold hierarchyid, @nnew hierarchyid  
SELECT @nold = OrgNode FROM HumanResources.EmployeeDemo WHERE LoginID = @oldMgr ;  
  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
BEGIN TRANSACTION  
SELECT @nnew = OrgNode FROM HumanResources.EmployeeDemo WHERE LoginID = @newMgr ;  
  
SELECT @nnew = @nnew.GetDescendant(max(OrgNode), NULL)   
FROM HumanResources.EmployeeDemo WHERE OrgNode.GetAncestor(1)=@nnew ;  
  
UPDATE HumanResources.EmployeeDemo    
SET OrgNode = OrgNode.GetReparentedValue(@nold, @nnew)  
WHERE OrgNode.IsDescendantOf(@nold) = 1 ;  
  
COMMIT TRANSACTION;
END ;  
GO  
```  
  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de método de tipo de dados hierarchyid](../t-sql/data-types/hierarchyid-data-type-method-reference.md)   
 [Tutorial: Usar o tipo de dados HierarchyId](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md)   
 [hierarchyid &#40;Transact-SQL&#41;](../t-sql/data-types/hierarchyid-data-type-method-reference.md)  
  
