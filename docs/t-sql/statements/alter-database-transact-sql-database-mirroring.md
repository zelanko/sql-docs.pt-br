---
title: Alterar banco de dados do banco de dados de espelhamento (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- witness [SQL Server], establishing
- manual failover [SQL Server]
- ALTER DATABASE statement, database mirroring
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 27a032ef-1cf6-4959-8e67-03d28c4b3465
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54396925abb0e8eb2d6006ffdd4048551792d6db
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="alter-database-transact-sql-database-mirroring"></a>Banco de dados ALTER DATABASE (Transact-SQL) de espelhamento 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] em vez disso.  
  
 Controla o espelhamento de um banco de dados. Valores especificados com as opções de espelhamento de banco de dados aplicam-se a ambas as cópias do banco de dados e à sessão de espelhamento de banco de dados como um todo. Apenas um \<database_mirroring_option > é permitido por instrução ALTER DATABASE.  
  
> [!NOTE]  
>  Recomendamos configurar um espelhamento de banco de dados fora do período do pico de atividade, pois a configuração pode comprometer o desempenho.  
  
 Para opções ALTER DATABASE, consulte [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md). Para opções ALTER DATABASE SET, consulte [opções ALTER DATABASE SET &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER DATABASE database_name   
SET { <partner_option> | <witness_option> }  
  <partner_option> ::=  
    PARTNER { = 'partner_server'   
            | FAILOVER   
            | FORCE_SERVICE_ALLOW_DATA_LOSS  
            | OFF  
            | RESUME   
            | SAFETY { FULL | OFF }  
            | SUSPEND   
            | TIMEOUT integer  
            }  
  <witness_option> ::=  
    WITNESS { = 'witness_server'   
            | OFF   
            }  
  
```  
  
## <a name="arguments"></a>Argumentos  
  
> [!IMPORTANT]  
>  Um comando SET PARTNER ou SET WITNESS pode ser concluído com êxito quando digitado, mas falhar posteriormente.  
  
> [!NOTE]  
>  As opções de espelhamento de banco de dados ALTER DATABASE não estão disponíveis para um banco de dados independente.  
  
 *database_name*  
 É o nome do banco de dados a ser modificado.  
  
 PARTNER \<partner_option>  
 Controla as propriedades de banco de dados que definem os parceiros de failover de uma sessão de espelhamento de banco de dados e seu comportamento. Algumas opções de SET PARTNER podem ser definidas em qualquer parceiro; outros se restringem ao servidor principal ou ao servidor espelho. Para obter mais informações, consulte as opções individuais de PARTNER a seguir. Uma cláusula SET PARTNER afeta ambas as cópias do banco de dados, independentemente do parceiro no qual é especificada.  
  
 Para executar uma instrução SET PARTNER, o STATE dos pontos de extremidade de ambos os parceiros deve ser definido como STARTED. Note, também, que o ROLE do ponto de extremidade do espelhamento de banco de dados de cada instância de servidor parceiro deve ser definido como PARTNER ou ALL. Para obter informações sobre como especificar um ponto de extremidade, consulte [criar um banco de dados de espelhamento de ponto de extremidade para autenticação do Windows &#40; Transact-SQL &#41; ](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md). Para conhecer a função e o estado do ponto de extremidade do espelhamento de banco de dados de uma instância de servidor, naquela instância, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```  
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
```  
  
 **\<partner_option> ::=**  
  
> [!NOTE]  
>  Apenas um \<partner_option > é permitida por cláusula SET PARTNER.  
  
 **'** *partner_server* **'**  
 Especifica o endereço de rede de servidor de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atuar como um parceiro de failover em uma nova sessão de espelhamento de banco de dados. Cada sessão requer dois parceiros: um começa como servidor principal e o outro, como servidor espelho. Recomendamos que estes parceiros residam em computadores diferentes.  
  
 Esta opção é especificada uma vez por sessão em cada parceiro. Iniciar um sessão de espelhamento de banco de dados requer duas ALTER DATABASE *banco de dados* SET PARTNER **='***partner_server***'** instruções. A ordem delas é significativa. Primeiro, conecte-se ao servidor espelho e especifique a instância do servidor principal como *partner_server* (SET PARTNER **='***servidor_principal***'**). Segundo, conecte-se ao servidor principal e especifique a instância de servidor espelho como *partner_server* (SET PARTNER **='***servidor_espelho***'**); Isso inicia um banco de dados sessão entre esses dois parceiros de espelhamento. Para obter mais informações, consulte [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
 O valor de *partner_server* é um endereço de rede do servidor. Tem a seguinte sintaxe:  
  
 TCP**://***\<system-address>***:***\<port>*  
  
 onde  
  
-   *\<endereço do sistema >* é uma cadeia de caracteres, como um nome de sistema, um nome de domínio totalmente qualificado ou um endereço IP, que identifica inequivocamente o sistema de computador de destino.  
  
-   *\<porta >* é um número de porta que está associado com o ponto de extremidade de espelhamento da instância do servidor parceiro.  
  
 Para obter mais informações, consulte [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).  
  
 O exemplo a seguir ilustra a SET PARTNER **='***partner_server***'** cláusula:  
  
```  
'TCP://MYSERVER.mydomain.Adventure-Works.com:7777'  
```  
  
> [!IMPORTANT]  
>  Se uma sessão for configurada utilizando-se a instrução ALTER DATABASE, em vez de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], a sessão será definida com segurança de transação completa, por padrão (SAFETY é definido como FULL), e será executada em modo de alta segurança sem failover automático. Para permitir failover automático, configure uma testemunha; para executar em modo de alto desempenho, desative a segurança de transação (SAFETY OFF).  
  
 FAILOVER  
 Efetua failover do servidor principal manualmente para o servidor espelho. É possível especificar FAILOVER apenas no servidor principal. Esta opção só será válida quando a configuração SAFETY for FULL (o padrão).  
  
 A opção de FAILOVER requer **mestre** como o contexto do banco de dados.  
  
 FORCE_SERVICE_ALLOW_DATA_LOSS  
 Força o serviço de banco de dados no banco de dados espelho depois que o servidor principal falha com o banco de dados em estado não sincronizado ou sincronizado quando não ocorre failover automático.  
  
 É extremamente recomendável que você só force o serviço se o servidor principal não estiver mais em execução. Caso contrário, alguns clientes poderão continuar acessando o banco de dados principal original, em vez do novo banco de dados principal.  
  
 FORCE_SERVICE_ALLOW_DATA_LOSS só está disponível no servidor espelho e apenas sob as seguintes condições:  
  
-   O servidor principal está fora de operação.  
  
-   WITNESS está definido como OFF ou a testemunha está conectada ao servidor espelho.  
  
 Force o serviço apenas se você estiver disposto a arriscar perder alguns dados para restaurar imediatamente o serviço no banco de dados.  
  
 Forçar serviço suspende a sessão, preservando todos os dados temporariamente no banco de dados principal original. Uma vez que o banco de dados principal original estiver em serviço e conseguir se comunicar com o novo servidor principal, o administrador do banco de dados poderá retomar o serviço. Quando a sessão retomar, todos os registros de log não enviado e suas atualizações correspondentes serão perdidos.  
  
 OFF  
 Remove uma sessão de espelhamento de banco de dados e remove o espelhamento de banco de dados. Você pode especificar OFF em qualquer parceiro. Para obter informações, consulte sobre o impacto da remoção do espelhamento, consulte [removendo o espelhamento de banco de dados &#40; SQL Server &#41; ](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
 RESUME  
 Retoma uma sessão de espelhamento de banco de dados suspenso. É possível especificar RESUME apenas no servidor principal.  
  
 SAFETY { FULL | OFF }  
 Define o nível de segurança de transação. É possível especificar SAFETY apenas no servidor principal.  
  
 O padrão é FULL. Com a segurança completa, o sessão de espelhamento de banco de dados é executada síncrona (em *modo de alta segurança*). Se a segurança é definida como OFF, o sessão de espelhamento de banco de dados executa de modo assíncrono (em *modo de alto desempenho*).  
  
 O comportamento do modo de alta segurança depende, em parte, da testemunha, como segue:  
  
-   Quando a segurança é definida como FULL e uma testemunha é definida para a sessão, esta é executada em modo de alta segurança com failover automático. Quando o servidor principal for perdido, a sessão terá failover automaticamente se o banco de dados for sincronizado e a instância de servidor espelho e a testemunha ainda estiverem conectadas entre si (ou seja, tiverem quorum). Para obter mais informações, consulte [Quorum: como uma testemunha afeta a disponibilidade do banco de dados &#40;Espelhamento de Banco de Dados&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
     Se uma testemunha for definida para a sessão, mas estiver atualmente desconectada, a perda do servidor espelho fará com que o servidor principal caia.  
  
-   Quando a segurança está definida como FULL e a testemunha está definida como OFF, a sessão é executada em modo de alta segurança sem failover automático. Se a instância de servidor espelho cair, a instância de servidor principal não será afetada. Se a instância de servidor principal cair, você poderá forçar o serviço (com possível perda de dados) na instância de servidor espelho.  
  
 Se SAFETY estiver definido como OFF, a sessão será executada em modo de alto desempenho e não haverá suporte para failover automático ou manual. Porém, problemas no espelho não afetam o principal e, se a instância de servidor principal cair, você poderá, se necessário, forçar o serviço (com possível perda de dados) na instância de servidor espelho — se WITNESS estiver definido como OFF ou a testemunha estiver conectada atualmente ao espelho. Para obter mais informações sobre como forçar o serviço, consulte "FORCE_SERVICE_ALLOW_DATA_LOSS" anteriormente, nesta seção.  
  
> [!IMPORTANT]  
>  Não se pretende que o modo de alto desempenho use uma testemunha. Porém, sempre que definir SAFETY como OFF, é altamente recomendável que você verifique se WITNESS está definido como OFF.  
  
 SUSPEND  
 Pausa uma sessão de espelhamento de banco de dados.  
  
 Você pode especificar SUSPEND em qualquer parceiro.  
  
 Tempo limite *inteiro*  
 Especifica o tempo limite, em segundos. O tempo limite é o tempo máximo que uma instância de servidor espera para receber uma mensagem PING de outra instância na sessão de espelhamento antes de considerá-la desconectada.  
  
 Você só pode especificar a opção TIMEOUT no servidor principal. Se você não especificar essa opção, por padrão, o período de tempo será de 10 segundos. Se você especificar 5 ou mais, o tempo limite será definido como o número de segundos especificado. Se você especificar um valor de tempo limite de 0 a 4 segundos, o período será definido automaticamente como 5 segundos.  
  
> [!IMPORTANT]  
>  Recomendamos que você mantenha o tempo limite em 10 segundos ou mais. Definir o valor como menos de 10 segundos cria a possibilidade de um sistema extremamente carregado perdendo PINGs e declarando uma falsa falha.  
  
 Para obter mais informações, veja [Possíveis falhas durante o espelhamento de banco de dados](../../database-engine/database-mirroring/possible-failures-during-database-mirroring.md).  
  
 TESTEMUNHA \<witness_option >  
 Controla as propriedades de banco de dados que definem uma testemunha de espelhamento de banco de dados. Uma cláusula SET WITNESS afeta ambas as cópias do banco de dados, mas você só pode especificar SET WITNESS no servidor principal. Se uma testemunha é definida para uma sessão, o quorum é exigido para servir o banco de dados, independentemente da configuração de segurança; Para obter mais informações, consulte [Quorum: como uma testemunha afeta o banco de dados de disponibilidade &#40; espelhamento de banco de dados &#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
 Recomendamos que a testemunha e os parceiros de failover residam em computadores separados. Para obter informações sobre a testemunha, consulte [testemunha de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-witness.md).  
  
 Para executar uma instrução SET WITNESS, o STATE dos pontos de extremidade das instâncias do servidor testemunha e principal deve ser definido como STARTED. Observe, também, que o ROLE do ponto de extremidade do espelhamento de banco de dados de uma instância de servidor testemunha deve ser definido como WITNESS ou ALL. Para obter informações sobre como especificar um ponto de extremidade, consulte [a extremidade de espelhamento de banco de dados &#40; SQL Server &#41; ](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
 Para conhecer a função e o estado do ponto de extremidade do espelhamento de banco de dados de uma instância de servidor, naquela instância, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```  
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
```  
  
> [!NOTE]  
>  As propriedades do banco de dados não podem ser definidas na testemunha.  
  
 **\<witness_option> ::=**  
  
> [!NOTE]  
>  Apenas um \<witness_option > é permitida por cláusula SET WITNESS.  
  
 **'** *witness_server* **'**  
 Especifica uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para atuar como servidor testemunha de uma sessão de espelhamento de banco de dados. Você só pode especificar instruções SET WITNESS no servidor principal.  
  
 Em SET WITNESS **='***witness_server***'** instrução, a sintaxe de *witness_server* é o mesmo que a sintaxe de *partner_server*.  
  
 OFF  
 Remove a testemunha de uma sessão de espelhamento de banco de dados. Definir a testemunha como OFF desabilita o failover automático. Se o banco de dados estiver definido como FULL SAFETY e a testemunha como OFF, uma falha no servidor espelho fará com que o servidor principal torne o banco de dados indisponível.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-database-mirroring-session-with-a-witness"></a>A. Criando uma sessão de espelhamento de banco de dados com uma testemunha  
 A definição do espelhamento de banco de dados com testemunha requer a configuração da segurança e a preparação do banco de dados espelho, além do uso de ALTER DATABASE para definir os parceiros. Para obter um exemplo do processo de concluir a instalação, consulte [Configurando o espelhamento de banco de dados &#40; SQL Server &#41; ](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
### <a name="b-manually-failing-over-a-database-mirroring-session"></a>B. Efetuando manualmente o failover de uma sessão de espelhamento de banco de dados  
 O failover manual pode ser iniciado a partir de qualquer parceiro de espelhamento de banco de dados. Antes de efetuar o failover, você deve verificar se o servidor que se acredita ser o servidor principal atual o é de fato. Por exemplo, para o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], na instância de servidor que se acredita ser o servidor principal atual, execute a seguinte consulta:  
  
```  
SELECT db.name, m.mirroring_role_desc   
FROM sys.database_mirroring m   
JOIN sys.databases db  
ON db.database_id = m.database_id  
WHERE db.name = N'AdventureWorks2012';   
GO  
```  
  
 Se a instância do servidor for realmente a principal, o valor de `mirroring_role_desc` será `Principal`. Se essa instância de servidor fosse o servidor espelho, a instrução `SELECT` retornaria `Mirror`.  
  
 O exemplo a seguir presume que o servidor seja o principal atual.  
  
1.  Efetue manualmente o failover no parceiro de espelhamento de banco de dados:  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER FAILOVER;  
    GO  
    ```  
  
2.  Para verificar os resultados do failover no espelho novo, execute a seguinte consulta:  
  
    ```  
    SELECT db.name, m.mirroring_role_desc   
    FROM sys.database_mirroring m   
    JOIN sys.databases db  
    ON db.database_id = m.database_id  
    WHERE db.name = N'AdventureWorks2012';   
    GO  
    ```  
  
     O valor atual de `mirroring_role_desc` agora é `Mirror`.  
  
## <a name="see-also"></a>Consulte também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)  
  
  
