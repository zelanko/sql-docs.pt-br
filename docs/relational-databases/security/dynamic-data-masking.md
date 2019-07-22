---
title: Mascaramento de dados dinâmicos | Microsoft Docs
ms.date: 05/02/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: a62f4ff9-2953-42ca-b7d8-1f8f527c4d66
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c0f2a5d652b23efec6b4dd1c6d021f85e1155247
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997718"
---
# <a name="dynamic-data-masking"></a>Mascaramento de dados dinâmicos
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

![Mascaramento de dados dinâmicos](../../relational-databases/security/media/dynamic-data-masking.png)

O DDM (Máscara de Dados Dinâmicos) limita a exposição de dados confidenciais aplicando uma máscara para usuários sem privilégios. Ele pode ser usado para simplificar bastante o design e a codificação de segurança em seu aplicativo.  

A máscara de dados dinâmicos ajuda a impedir o acesso não autorizado a dados confidenciais, permitindo que os clientes especifiquem a quantidade de dados confidenciais a revelar, com impacto mínimo sobre a camada de aplicativo. O DDM pode ser configurado em campos de banco de dados designados para ocultar dados confidenciais nos conjuntos de resultados de consultas. Com DDM, os dados no banco de dados não são alterados. O mascaramento de dados dinâmicos é fácil de usar com aplicativos existentes, já que as regras de mascaramento são aplicadas nos resultados da consulta. Muitos aplicativos podem mascarar dados confidenciais sem modificar consultas existentes.

* Uma política de mascaramento de dados central atua diretamente nos campos confidenciais do banco de dados.
* Designe usuários ou funções com privilégios que tenham acesso aos dados confidenciais.
* O DDM apresenta funções de máscara completa e parcial e uma máscara aleatória para dados numéricos.
* Comandos simples do [!INCLUDE[tsql_md](../../includes/tsql-md.md)] definem e gerenciam máscaras.

Por exemplo, um profissional de suporte do call center pode identificar chamadores por vários dígitos do seu número do seguro social ou número de cartão de crédito.  Números do seguro social ou números de cartão de crédito não devem ser totalmente expostos para o profissional de suporte. Uma regra de mascaramento pode ser definida para mascarar todos exceto os quatro últimos dígitos de qualquer número do seguro social ou número de cartão de crédito no conjunto de resultado de qualquer consulta. Em outro exemplo, ao usar a máscara de dados apropriada para proteger dados de informações de identificação pessoal (PII), um desenvolvedor pode consultar os ambientes de produção para fins de solução de problemas sem violar os regulamentos de conformidade.

A finalidade do mascaramento de dados dinâmicos é limitar a exposição de dados confidenciais, impedindo que os usuários que não devem ter acesso a esses dados os visualizem. O mascaramento de dados dinâmicos não pretende impedir que usuários de banco de dados se conectem diretamente ao banco de dados e executem consultas abrangentes que exponham dados confidenciais. A Máscara de Dados Dinâmicos é complementar aos outros recursos de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (auditoria, criptografia, segurança em nível de linha...) e seu uso é altamente recomendável em conjunto com esses outros recursos, a fim de proteger melhor os dados confidenciais no banco de dados.  
  
O mascaramento de dados dinâmicos está disponível em [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)], e é configurado usando comandos do [!INCLUDE[tsql](../../includes/tsql-md.md)] . Para obter mais informações sobre como configurar a máscara de dados dinâmicos usando o portal do Azure, veja [Introdução à Máscara de Dados Dinâmicos do Banco de Dados SQL (portal do Azure)](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/).  
  
## <a name="defining-a-dynamic-data-mask"></a>Definir uma máscara de dados dinâmicos
 Uma regra de mascaramento pode ser definida em uma coluna de tabela para ocultar os dados dessa coluna. Há quatro tipos de máscaras disponíveis.  
  
|Função|Descrição|Exemplos|  
|--------------|-----------------|--------------|  
|Padrão|Mascaramento completo de acordo com os tipos de dados dos campos designados.<br /><br /> Para os tipos de dados string, use XXXX ou menos Xs se o tamanho do campo for inferior a quatro caracteres (**char**, **nchar**,  **varchar**, **nvarchar**, **text**, **ntext**).  <br /><br /> Para os tipos de dados numeric, use um valor zero (**bigint**, **bit**, **decimal**, **int**, **money**, **numeric**, **smallint**, **smallmoney**, **tinyint**, **float**, **real**).<br /><br /> Para os tipos de dados data e hora, use 01.01.1900 00:00:00.0000000 (**date**, **datetime2**, **datetime**, **datetimeoffset**, **smalldatetime**, **time**).<br /><br />Para os tipos de dados binary, use um único byte de valor ASCII 0 (**binary**, **varbinary**, **image**).|Exemplo da sintaxe de definição de coluna: `Phone# varchar(12) MASKED WITH (FUNCTION = 'default()') NULL`<br /><br /> Exemplo de sintaxe de alteração: `ALTER COLUMN Gender ADD MASKED WITH (FUNCTION = 'default()')`|  
|Email|O método de mascaramento que expõe a primeira letra de um endereço de email e o sufixo constante ".com", na forma de um endereço de email. `aXXX@XXXX.com`.|Exemplo da sintaxe de definição: `Email varchar(100) MASKED WITH (FUNCTION = 'email()') NULL`<br /><br /> Exemplo de sintaxe de alteração: `ALTER COLUMN Email ADD MASKED WITH (FUNCTION = 'email()')`|  
|Random|Uma função de mascaramento aleatório para uso em qualquer tipo numérico para mascarar o valor original com um valor aleatório dentro de um intervalo especificado.|Exemplo da sintaxe de definição: `Account_Number bigint MASKED WITH (FUNCTION = 'random([start range], [end range])')`<br /><br /> Exemplo de sintaxe de alteração: `ALTER COLUMN [Month] ADD MASKED WITH (FUNCTION = 'random(1, 12)')`|  
|Cadeia de caracteres personalizada|O método de mascaramento que expõe as primeiras e últimas letras e adiciona uma cadeia de caracteres de preenchimento personalizada no meio. `prefix,[padding],suffix`<br /><br /> Observação: se o valor original for muito curto para completar a máscara inteira, parte do prefixo ou sufixo não será exposta.|Exemplo da sintaxe de definição: `FirstName varchar(100) MASKED WITH (FUNCTION = 'partial(prefix,[padding],suffix)') NULL`<br /><br /> Exemplo de sintaxe de alteração: `ALTER COLUMN [Phone Number] ADD MASKED WITH (FUNCTION = 'partial(1,"XXXXXXX",0)')`<br /><br /> Exemplos adicionais:<br /><br /> `ALTER COLUMN [Phone Number] ADD MASKED WITH (FUNCTION = 'partial(5,"XXXXXXX",0)')`<br /><br /> `ALTER COLUMN [Social Security Number] ADD MASKED WITH (FUNCTION = 'partial(0,"XXX-XX-",4)')`|  
  
## <a name="permissions"></a>Permissões  
 Não é necessário qualquer permissão especial para criar uma tabela com uma máscara de dados dinâmico, somente as permissões padrão de esquema **CREATE TABLE** e **ALTER** .  
  
 Para adicionar, substituir ou remover a máscara de uma coluna, a tabela deve ter as permissões **ALTER ANY MASK** e **ALTER** . É recomendável conceder **ALTER ANY MASK** para um analista de segurança.  
  
 Os usuários com a permissão **SELECT** em uma tabela podem exibir os dados da tabela. As colunas definidas como mascaradas exibirão os dados mascarados. Conceda a permissão **UNMASK** a um usuário para que ele possa recuperar dados não mascarados de colunas para as quais o mascaramento é definido.  
  
 A permissão **CONTROL** no banco de dados inclui as permissões **ALTER ANY MASK** e **UNMASK** .  
  
## <a name="best-practices-and-common-use-cases"></a>Práticas recomendadas e casos de uso comuns  
  
-   Criar uma máscara em uma coluna não impede que atualizações nessa coluna. Portanto, embora os usuários recebam dados mascarados ao consultar a coluna mascarada, os mesmos usuários podem atualizar os dados se tiverem permissões de gravação. Uma política de controle de acesso adequada ainda deve ser usada para limitar as permissões de atualização.  
  
-   Usar `SELECT INTO` ou `INSERT INTO` para copiar dados de uma coluna mascarada para outra tabela resulta em dados mascarados na tabela de destino.  
  
-   O mascaramento de dados dinâmicos é aplicado durante a execução de importações e exportações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Um banco de dados que contém colunas mascaradas resultará em um arquivo de dados exportado contendo dados mascarados (supondo que ele seja exportado por um usuário sem privilégios de **UNMASK**) e o banco de dados importado conterá dados estaticamente mascarados.  
  
## <a name="querying-for-masked-columns"></a>Consultar colunas mascaradas  
 Use a exibição **sys.masked_columns** para consultar colunas de tabela que tenham uma função de máscara aplicada. Essa exibição herda valores da exibição **sys.columns** . Ela retorna todas as colunas na exibição **sys.columns** , mais as colunas **is_masked** e **masking_function** , indicando se a coluna é mascarada e, em caso positivo, qual função de mascaramento foi definida. Essa exibição só mostra colunas com uma função de máscara aplicada.  
  
```sql 
SELECT c.name, tbl.name as table_name, c.is_masked, c.masking_function  
FROM sys.masked_columns AS c  
JOIN sys.tables AS tbl   
    ON c.[object_id] = tbl.[object_id]  
WHERE is_masked = 1;  
```  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 Não é possível definir uma regra de mascaramento para os seguintes tipos de coluna:  
  
-   Colunas criptografadas (Sempre Criptografadas)  
  
-   FILESTREAM  
  
-   COLUMN_SET ou uma coluna esparsa que faz parte de um conjunto de colunas.  
  
-   Uma máscara não pode ser configurada em uma coluna computada, mas se a coluna computada depender de uma coluna com uma MÁSCARA, ela retornará dados mascarados.  
  
-   Uma coluna com mascaramento de dados não pode ser uma chave para um índice FULLTEXT.  
  
 Para os usuários que não tenham a permissão **UNMASK** , as instruções **READTEXT**, **UPDATETEXT**e **WRITETEXT** preteridas não funcionarão corretamente em uma coluna configurada para mascaramento de dados dinâmicos. 
 
 A adição de uma máscara de dados dinâmicos é implementada como uma alteração de esquema na tabela subjacente e, portanto, não pode ser realizada em uma coluna com dependências. Para contornar essa restrição, você pode primeiro remover a dependência e adicionar a máscara de dados dinâmicos e, em seguida, recriar a dependência. Por exemplo, se a dependência ocorre devido a um índice dependente nessa coluna, você poderá remover o índice, adicionar a máscara e, em seguida, recriar o índice dependente.
 

## <a name="security-note-bypassing-masking-using-inference-or-brute-force-techniques"></a>Observação de segurança: ignorar a máscara usando técnicas de inferência ou força bruta

O Mascaramento de dados dinâmicos foi projetado para simplificar o desenvolvimento de aplicativos, limitando a exposição de dados em um conjunto de consultas predefinidas usadas pelo aplicativo. Embora o Mascaramento de dados dinâmicos também possa ser útil para evitar a exposição acidental de dados confidenciais ao acessar diretamente um banco de dados de produção, é importante observar que usuários sem privilégios com permissões de consulta ad hoc podem aplicar técnicas para acessar os dados reais. Se houver a necessidade de conceder esse acesso ad hoc, a Auditoria deve ser usada para monitorar todas as atividades do banco de dados e reduzir esse cenário.
 
Por exemplo, considere uma entidade de banco de dados principal que tem privilégios suficientes para executar consultas ad hoc no banco de dados e tenta "adivinhar" os dados subjacentes e inferir os valores reais. Suponha que tenhamos uma máscara definida na coluna `[Employee].[Salary]` e esse usuário se conecte diretamente ao banco de dados e comece a adivinhar valores, eventualmente inferindo o valor `[Salary]` de um conjunto de funcionários:
 

```sql
SELECT ID, Name, Salary FROM Employees
WHERE Salary > 99999 and Salary < 100001;
```

>    |  ID | Nome| Salário |   
>    | ----- | ---------- | ------ | 
>    |  62543 | Jane Doe | 0 | 
>    |  91245 | John Smith | 0 |  

Isso demonstra que Mascaramento de dados dinâmicos não deve ser usado como uma medida isolada para proteger dados confidenciais de usuários que executam consultas ad hoc no banco de dados. Ele é adequado para impedir a exposição acidental de dados confidenciais, mas não protege contra intenções mal-intencionadas de inferir os dados subjacentes.
 
É importante gerenciar corretamente as permissões no banco de dados e sempre seguir o princípio de mínimo de permissões necessárias. Além disso, lembre-se de ter a Auditoria habilitada para acompanhar todas as atividades que ocorrem no banco de dados.

  
## <a name="examples"></a>Exemplos  
  
### <a name="creating-a-dynamic-data-mask"></a>Criar uma máscara de dados dinâmicos  
 O exemplo a seguir cria uma tabela com três tipos diferentes de máscaras de dados dinâmicos. O exemplo preenche a tabela e faz seleções para mostrar o resultado.  
  
```sql
CREATE TABLE Membership  
  (MemberID int IDENTITY PRIMARY KEY,  
   FirstName varchar(100) MASKED WITH (FUNCTION = 'partial(1,"XXXXXXX",0)') NULL,  
   LastName varchar(100) NOT NULL,  
   Phone varchar(12) MASKED WITH (FUNCTION = 'default()') NULL,  
   Email varchar(100) MASKED WITH (FUNCTION = 'email()') NULL);  
  
INSERT Membership (FirstName, LastName, Phone, Email) VALUES   
('Roberto', 'Tamburello', '555.123.4567', 'RTamburello@contoso.com'),  
('Janice', 'Galvin', '555.123.4568', 'JGalvin@contoso.com.co'),  
('Zheng', 'Mu', '555.123.4569', 'ZMu@contoso.net');  
SELECT * FROM Membership;  
```  
  
 Um novo usuário é criado e recebe a permissão **SELECT** na tabela. As consultas executadas como o `TestUser` exibem os dados mascarados.  
  
```sql 
CREATE USER TestUser WITHOUT LOGIN;  
GRANT SELECT ON Membership TO TestUser;  
  
EXECUTE AS USER = 'TestUser';  
SELECT * FROM Membership;  
REVERT;  
```  
  
 O resultado demonstra as máscaras ao alterar os dados de  
  
 `1    Roberto     Tamburello    555.123.4567    RTamburello@contoso.com`  
  
 into  
  
 `1    RXXXXXXX    Tamburello    xxxx            RXXX@XXXX.com`  
  
### <a name="adding-or-editing-a-mask-on-an-existing-column"></a>Adicionar ou editar uma máscara em uma coluna existente  
 Use a instrução **ALTER TABLE** para adicionar uma máscara a uma coluna existente na tabela ou para editar a máscara nessa coluna.  
O exemplo a seguir adiciona uma função de mascaramento para a coluna `LastName` :  
  
```sql  
ALTER TABLE Membership  
ALTER COLUMN LastName ADD MASKED WITH (FUNCTION = 'partial(2,"XXX",0)');  
```  
  
 O exemplo a seguir altera uma função de mascaramento da coluna `LastName` :  

```sql  
ALTER TABLE Membership  
ALTER COLUMN LastName varchar(100) MASKED WITH (FUNCTION = 'default()');  
```  
  
### <a name="granting-permissions-to-view-unmasked-data"></a>Conceder permissões para exibir dados não mascarados  
 Conceder a permissão **UNMASK** permite que `TestUser` visualize os dados não mascarados.  
  
```sql
GRANT UNMASK TO TestUser;  
EXECUTE AS USER = 'TestUser';  
SELECT * FROM Membership;  
REVERT;   
  
-- Removing the UNMASK permission  
REVOKE UNMASK TO TestUser;  
```  
  
### <a name="dropping-a-dynamic-data-mask"></a>Eliminar uma máscara de dados dinâmicos  
 A instrução a seguir elimina a máscara da coluna `LastName` criada no exemplo anterior:  
  
```sql  
ALTER TABLE Membership   
ALTER COLUMN LastName DROP MASKED;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_definition &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-definition-transact-sql.md)   
 [sys.masked_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-masked-columns-transact-sql.md)   
 [Introdução à máscara de dados dinâmicos do Banco de Dados SQL (portal do Azure)](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)  
