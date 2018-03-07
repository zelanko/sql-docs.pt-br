---
title: CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: 
ms.prod_service: pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a44f5f46a60959b38b3e8121847e0c80c1ba82b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Seleciona os dados de um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] banco de dados e copia esses dados para uma nova tabela em um SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados em um servidor remoto. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]usa o dispositivo, com todos os benefícios MPP do processamento de consulta, para selecionar os dados para a cópia remota. Use isto para cenários que requerem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionalidade.  
  
 Para configurar o servidor remoto, consulte "Cópia de tabela remota" a [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE REMOTE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name     AT ('<connection_string>')  
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
 O banco de dados para criar a tabela remota. *Database_Name* é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. O padrão é o banco de dados padrão para o logon do usuário no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.  
  
 *schema_name*  
 O esquema para a nova tabela. O padrão é o esquema padrão para o logon do usuário no destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.  
  
 *table_name*  
 O nome da nova tabela. Para obter detalhes sobre permitidos nomes de tabela, consulte "Regras de nomenclatura de objeto" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 A tabela remota é criada como um heap. Ele não tem restrições de verificação ou disparadores. O agrupamento das colunas da tabela remota é o mesmo agrupamento das colunas da tabela de origem. Isso se aplica a colunas do tipo **char**, **nchar**, **varchar**, e **nvarchar**.  
  
 *connection_string*  
 Uma cadeia de caracteres que especifica o `Data Source`, `User ID`, e `Password` parâmetros para conexão com o servidor remoto e o banco de dados.  
  
 A cadeia de conexão é uma lista separada por ponto-e-vírgula de pares de chave e valor. Palavras-chave não diferenciam maiusculas de minúsculas. Espaços entre pares de chave e valor são ignorados. No entanto, os valores podem ser diferencia maiusculas de minúsculas, dependendo da fonte de dados.  
  
 *Fonte de dados*  
 O parâmetro que especifica o nome ou o endereço IP e o TCP número da porta para o SMP remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *nome do host* ou *endereço_IP*  
 Nome do computador do servidor remoto ou o endereço IPv4 do servidor remoto. Não há suporte para endereços IPv6. Você pode especificar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância no formato nomeada **nome_do_computador \ nome_da_instância** ou **IP_address\Instance_Name**. O servidor deve ser remoto e, portanto, não pode ser especificado como (local).  
  
 TCP *porta* número  
 O número da porta TCP para a conexão. Você pode especificar um número de porta TCP de 0 a 65535 para uma instância do SQL Server que não está escutando na porta padrão 1433. Por exemplo: **servidora, 1450** ou **10.192.14.27,1435**  
  
> [!NOTE]  
>  Recomendamos que você se conectar a um servidor remoto usando o endereço IP. Dependendo de sua configuração de rede, a conexão usando o nome do computador pode exigir etapas adicionais para usar o servidor DNS não seja de aplicação para resolver o nome para o servidor correto. Esta etapa não é necessária ao se conectar com um endereço IP. Para obter mais informações, consulte "Usar um encaminhador DNS para nomes DNS de dispositivo não Resolve (Analytics Platform System)" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 *user_name*  
 Uma opção válida [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de logon de autenticação. Número máximo de caracteres é 128.  
  
 *password*  
 A senha de logon. Número máximo de caracteres é 128.  
  
 *batch_size*  
 O número máximo de linhas por lote. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]envia linhas em lotes para o servidor de destino. *Batch_size* é um inteiro > = 0. O padrão é 0.  
  
 COM *common_table_expression*  
 Especifica um conjunto de resultados nomeado temporário, conhecido como uma CTE (expressão de tabela comum). Para obter mais informações, consulte [com common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Selecione \<select_criteria > o predicado de consulta que especifica quais dados serão preenchidas a nova tabela remota. Para obter informações sobre a instrução SELECT, consulte [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer:  
  
-   Selecione a permissão em cada objeto na cláusula SELECT.  
  
-   Requer a permissão CREATE TABLE no banco de dados SMP de destino.  
  
-   Requer ALTER, INSERT e SELECT permissões no esquema SMP de destino.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Se a cópia de dados para o banco de dados remoto falhar, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] anular a operação, registrará um erro e tentar excluir a tabela remota. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]não garante uma limpeza bem-sucedida da nova tabela.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 **Servidor de destino remoto**:  
  
-   O TCP é o padrão e só tem suporte protocolo para se conectar a um servidor remoto.  
  
-   O servidor de destino deve ser um servidor não seja de aplicação. Criar tabela remota não pode ser usada para copiar dados de um dispositivo para outro.  
  
-   A instrução CREATE REMOTE TABLE só cria novas tabelas. Portanto, a nova tabela não pode já existir. O banco de dados remoto e o esquema já devem existir.  
  
-   O servidor remoto deve ter espaço disponível para armazenar os dados que são transferidos do dispositivo para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados remoto.  
  
 **Instrução SELECT**:  
  
-   As cláusulas ORDER BY e TOP não têm suporte nos critérios de seleção.  
  
-   Criar tabela remota não pode ser executada dentro de uma transação ativa ou quando a configuração de confirmação automática desativado está ativa para a sessão.  
  
 [Número de linhas do conjunto de &#40; Transact-SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) não tem nenhum efeito nesta instrução. Para obter um comportamento semelhante, use [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 Depois de criar a tabela remota, a tabela de destino não está bloqueada até que a cópia seja iniciada. Portanto, é possível que outro processo excluir a tabela remota depois que ela é criada e antes de inicia a cópia. Quando isso ocorrer, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] irá gerar um erro e a cópia falhará.  
  
## <a name="metadata"></a>Metadados  
 Use [sys.dm_pdw_dms_workers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md) para exibir o progresso de copiar os dados selecionados para o servidor remoto do SMP. Linhas com tipo PARALLEL_COPY_READER contêm essas informações.  
  
## <a name="security"></a>Segurança  
 Criar tabela remota usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação para se conectar à instância remota [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância; ele não usa autenticação do Windows.  
  
 O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] rede externa deve ativar o firewall, com exceção de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] portas, portas administrativas e as portas de gerenciamento.  
  
 Para ajudar a evitar a perda acidental de dados ou corrupção, a conta de usuário que é usada para copiar do dispositivo para o banco de dados de destino deve ter as permissões mínimas necessárias no banco de dados de destino.  
  
 Configurações de Conexão permitem que você se conectar ao SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância com SSL para proteger os dados de nome e a senha do usuário, mas com dados reais que estão sendo enviados descriptografados em texto não criptografado. Quando isso ocorrer, um usuário mal-intencionado pode interceptar o texto da instrução CREATE REMOTE TABLE, que contém o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de usuário e senha para fazer logon no SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância. Para evitar esse risco, usar criptografia de dados na conexão para o SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.  
  
##  <a name="Examples"></a> Exemplos  
  
### <a name="a-creating-a-remote-table"></a>A. Criando uma tabela remota  
 Este exemplo cria um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela remota de SMP chamada `MyOrdersTable` no banco de dados `OrderReporting` e esquema `Orders`. O `OrderReporting` banco de dados está em um servidor chamado `SQLA` que escuta na porta padrão 1433. A conexão com o servidor usa as credenciais do usuário `David`, cuja senha é `e4n8@3`.  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdmpdwdmsworkers-dmv-for-remote-table-copy-status"></a>B. Consultando a DMV sys.dm_pdw_dms_workers para status de cópia da tabela remota  
 Esta consulta mostra como exibir o status da cópia de uma cópia da tabela remota.  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. Usando uma dica de consulta de junção com CREATE REMOTE TABLE  
 Esta consulta mostra a sintaxe básica para usar uma dica de consulta de junção com CREATE REMOTE TABLE. Depois que a consulta é enviada para o nó de controle, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em execução em nós de computação, serão aplicadas a estratégia de junção de hash ao gerar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] plano de consulta. Para obter mais informações sobre dicas de junção e como usar a cláusula OPTION, consulte [cláusula OPTION &#40; Transact-SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  

