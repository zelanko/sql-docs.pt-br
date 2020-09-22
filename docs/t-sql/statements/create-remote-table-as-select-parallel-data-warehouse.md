---
description: CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse)
title: CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse)
ms.custom: seo-dt-2019
ms.date: 08/10/2017
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
author: ronortloff
ms.author: rortloff
ms.reviewer: jrasnick
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a45d59e3891e08f2ae5c5b5d64258b5ebcc371a8
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688323"
---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Seleciona os dados de um banco de dados do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] e copia esses dados para uma nova tabela em um banco de dados SMP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor remoto. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] usa o dispositivo, com todos os benefícios do processamento de consulta MPP, para selecionar os dados para a cópia remota. Use isto para cenários que exigem a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para configurar o servidor remoto, consulte "Cópia de tabela remota" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CREATE REMOTE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }  AT ('<connection_string>')  
    [ WITH ( BATCH_SIZE = batch_size ) ]  
    AS <select_statement>  
[;]  
  
<connection_string> ::=   
    Data Source = { IP_address | hostname } [, port ]; User ID = user_name ;Password = password;  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 O banco de dados no qual criar a tabela remota. *database_name* é um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Default é o banco de dados padrão para o logon de usuário na instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 *schema_name*  
 O esquema da nova tabela. Default é o esquema padrão para o logon de usuário na instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 *table_name*  
 O nome da nova tabela. Para obter detalhes sobre nomes de tabela permitidos, consulte "Regras de nomenclatura de objeto" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 A tabela remota é criada como um heap. Não tem restrições de verificação nem gatilhos. A ordenação das colunas de tabela remota é a mesma ordenação das colunas de tabela de origem. Isso se aplica a colunas do tipo **char**, **nchar**, **varchar** e **nvarchar**.  
  
 *connection_string*  
 Uma cadeia de caracteres que especifica os parâmetros `Data Source`, `User ID` e `Password` para conexão com o banco de dados e servidor remoto.  
  
 A cadeia de conexão é uma lista delimitada por ponto-e-vírgula de pares de chave e valor. As palavras-chave não diferenciam maiúsculas de minúsculas. Espaços entre pares de chave e valor são ignorados. No entanto, os valores podem diferenciar maiúsculas de minúsculas, dependendo da fonte de dados.  
  
 *Fonte de Dados*  
 O parâmetro que especifica o nome ou endereço IP e o número da porta TCP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP remoto.  
  
 *hostname* ou *IP_address*  
 Nome do computador do servidor remoto ou o endereço IPv4 do servidor remoto. Não há compatibilidade com endereços IPv6. Você pode especificar uma instância nomeada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no formato **Computer_Name\Instance_Name** ou **IP_address\Instance_Name**. O servidor deve ser remoto e, portanto, não pode ser especificado como (local).  
  
 Número da *porta* TCP  
 O número da porta TCP da conexão. Você pode especificar o número da porta TCP de 0 a 65535 para uma instância do SQL Server que não escuta na porta padrão 1433. Por exemplo:  **ServerA,1450** ou **10.192.14.27,1435**  
  
> [!NOTE]  
>  Recomendamos que você se conecte a um servidor remoto usando o endereço IP. Dependendo da configuração da rede, a conexão com o nome do computador pode exigir etapas adicionais para usar o servidor DNS que não seja de dispositivo para resolver o nome para o servidor correto. Esta etapa não é necessária ao se conectar com um endereço IP. Para obter mais informações, consulte "Usar um encaminhador DNS para resolver nomes DNS que não são de dispositivo (Analytics Platform System)" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 *user_name*  
 Um nome de logon de autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. O número máximo de caracteres é 128.  
  
 *password*  
 A senha de logon. O número máximo de caracteres é 128.  
  
 *batch_size*  
 O número máximo de linhas por lote. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] envia linhas em lotes para o servidor de destino. *Batch_size* é um inteiro positivo >= 0. O padrão é 0.  
  
 WITH *common_table_expression*  
 Especifica um conjunto de resultados nomeado temporário, conhecido como uma CTE (expressão de tabela comum). Para obter mais informações, confira [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 SELECT \<select_criteria> O predicado de consulta que especifica quais dados serão populados na nova tabela remota. Para obter informações sobre a instrução SELECT, consulte [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Exige:  
  
-   Permissão SELECT em cada objeto na cláusula SELECT.  
  
-   Exige a permissão CREATE TABLE no banco de dados SMP de destino.  
  
-   Exige as permissões ALTER, INSERT e SELECT no esquema SMP de destino.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Se a cópia de dados para o banco de dados remoto falhar, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] anulará a operação, registrará um erro em log e tentará excluir a tabela remota. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não assegura uma limpeza bem-sucedida da nova tabela.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 **Servidor de destino remoto**:  
  
-   TCP é o padrão e é o único protocolo compatível com a conexão a um servidor remoto.  
  
-   O servidor de destino deve ser um servidor que não seja de dispositivo. CREATE REMOTE TABLE não pode ser usado para copiar dados de um dispositivo para outro.  
  
-   A instrução CREATE REMOTE TABLE apenas cria novas tabelas. Portanto, a nova tabela não pode já existir. O banco de dados remoto e o esquema já devem existir.  
  
-   O servidor remoto deve ter um espaço disponível para armazenar os dados que são transferidos do dispositivo para o banco de dados remoto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Instrução SELECT**:  
  
-   Não há compatibilidade com as cláusulas ORDER BY e TOP nos critérios de seleção.  
  
-   CREATE REMOTE TABLE não pode ser executado dentro de uma transação ativa ou quando a configuração de AUTOCOMMIT OFF está ativa para a sessão.  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) não tem nenhum efeito nessa instrução. Para obter um comportamento semelhante, use [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 Depois de criar a tabela remota, a tabela de destino não é bloqueada até que a cópia seja iniciada. Portanto, é possível que outro processo exclua a tabela remota depois que ela é criada e antes do início da cópia. Quando isso ocorrer, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] gerará um erro e a cópia falhará.  
  
## <a name="metadata"></a>Metadados  
 Use [sys.dm_pdw_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md) para exibir o progresso de copiar os dados selecionados para o servidor SMP remoto. Linhas com o tipo PARALLEL_COPY_READER contêm essas informações.  
  
## <a name="security"></a>Segurança  
 CREATE REMOTE TABLE usa a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para se conectar à instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; ele não usa a Autenticação do Windows.  
  
 A rede externa do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] deve ter o firewall ativado, com exceção de portas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], portas administrativas e portas de gerenciamento.  
  
 Para ajudar a prevenir a perda acidental de dados ou que os dados sejam corrompidos, a conta de usuário usada para a cópia por meio do dispositivo para o banco de dados de destino deve ter as permissões mínimas necessárias no banco de dados de destino.  
  
 As configurações de conexão permitem que você se conecte à instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do SMP com o SSL protegendo os dados de nome de usuário e senha, mas com os dados reais enviados descriptografados em texto sem formatação. Quando isso ocorrer, um usuário mal-intencionado poderá interceptar o texto da instrução CREATE REMOTE TABLE, que contém o nome de usuário e a senha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer logon na instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP. Para impedir esse risco, use a criptografia de dados na conexão com a instância SMP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="examples"></a><a name="Examples"></a> Exemplos  
  
### <a name="a-creating-a-remote-table"></a>a. Criando uma tabela remota  
 Este exemplo cria uma tabela remota SMP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamada `MyOrdersTable` no banco de dados `OrderReporting` e o esquema `Orders`. O banco de dados `OrderReporting` está em um servidor chamado `SQLA` que escuta na porta padrão 1433. A conexão com o servidor usa as credenciais do usuário `David`, cuja senha é `e4n8@3`.  
  
```sql  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdm_pdw_dms_workers-dmv-for-remote-table-copy-status"></a>B. Consultando a DMV sys.dm_pdw_dms_workers para obter o status da cópia de tabela remota  
 Esta consulta mostra como exibir o status da cópia de uma cópia de tabela remota.  
  
```sql  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. Usando uma dica de junção de consulta com CREATE REMOTE TABLE  
 Essa consulta mostra a sintaxe básica para uso de uma dica de consulta de junção com CREATE REMOTE TABLE. Depois que a consulta é enviada para o nó de Controle, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em execução nos nós de Computação, aplicará a estratégia de junção hash ao gerar o plano de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre dicas de junção e como usar a cláusula OPTION, consulte [Cláusula OPTION &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
```sql  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  

