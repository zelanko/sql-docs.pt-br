---
title: Always Encrypted com enclaves seguros
description: Saiba mais sobre o Always Encrypted com o recurso de enclaves seguros do SQL Server.
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 3ad3743b35570ddb0f4644b909ca06339444143e
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87410932"
---
# <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted com enclaves seguros
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]
 
O Always Encrypted com enclaves seguros fornece funcionalidade adicional para o recurso [Always Encrypted](always-encrypted-database-engine.md).

Introduzido no SQL Server 2016, o Always Encrypted protege a confidencialidade dos dados confidenciais contra malwares e usuários com altos privilégios *não autorizados* do SQL Server. Usuários com altos privilégios não autorizados são DBAs, administradores de computador, administradores de nuvem ou qualquer outra pessoa que tenha acesso legítimo a instâncias do servidor, hardware, etc., mas que não poderia ter acesso à parte ou todos os dados reais.  

Sem os aprimoramentos discutidos neste artigo, o Always Encrypted protege os dados criptografando-os no lado do cliente e nunca permitindo que os dados ou as chaves de criptografia correspondentes aparecessem em texto não criptografado dentro do Mecanismo do SQL Server. Como resultado, a funcionalidade em colunas criptografadas dentro do banco de dados fica muito restrita. As únicas operações que o SQL Server pode executar em dados criptografados são comparações de igualdade (disponíveis somente com criptografia determinística). Todas as outras operações, incluindo operações criptográficas (criptografia de dados inicial ou rotação de chave) e/ou cálculos avançados (por exemplo, correspondência de padrões) não eram compatíveis com o interior do banco de dados. Os usuários precisam mover os dados para fora do banco de dados para executar essas operações no lado do cliente.

O Always Encrypted *com enclaves seguros* soluciona essas limitações, permitindo realizar cálculos em dados de texto não criptografado em um enclave seguro no lado do servidor. Um enclave seguro é uma região protegida de memória dentro do processo do SQL Server e atua como um ambiente de execução confiável para o processamento de dados confidenciais dentro do mecanismo do SQL Server. Um enclave seguro é exibido como uma caixa preta para o restante do SQL Server e outros processos no computador de hospedagem. Não há nenhuma maneira de exibir os dados ou o código dentro do enclave de fora, mesmo com um depurador.  


O Always Encrypted usa enclaves seguros, conforme ilustrado no diagrama a seguir:

![fluxo de dados](./media/always-encrypted-enclaves/ae-data-flow.png)



Durante a análise de uma consulta do aplicativo, o Mecanismo do SQL Server determina se a consulta contém alguma operação em dados criptografados que exige o uso do enclave seguro. Para consultas em que o enclave seguro precisa ser acessado:

- O driver do cliente envia as chaves de criptografia de coluna necessárias para as operações para o enclave seguro (por um canal seguro). 
- Em seguida, o driver do cliente envia a consulta para execução junto com os parâmetros da consulta criptografada.

Durante o processamento de consulta, os dados ou as chaves de criptografia de coluna não são expostos em texto não criptografado no Mecanismo do SQL Server fora do enclave seguro. O Mecanismo do SQL Server delega operações criptográficas e cálculos em colunas criptografadas para o enclave seguro. Se necessário, o enclave seguro descriptografa os parâmetros de consulta e/ou os dados armazenados em colunas criptografadas e executa as operações solicitadas.

Em [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], o Always Encrypted com enclaves seguros usa enclaves de memória seguros com [VBS (Segurança baseada em Virtualização)](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) (também conhecido como enclaves VSM ou Modo Seguro Virtual) no Windows.

## <a name="why-use-always-encrypted-with-secure-enclaves"></a>Por que usar o Always Encrypted com enclaves seguros?

Com enclaves seguros, o Always Encrypted protege a confidencialidade dos dados confidenciais, fornecendo os seguintes benefícios:

- **Criptografia in-loco** – operações criptográficas em dados confidenciais, por exemplo: criptografia de dados ou rotação de uma chave de criptografia de coluna são executadas dentro do enclave seguro e não exigem a movimentação dos dados para fora do banco de dados. Você pode emitir a criptografia in-loco usando a instrução Transact-SQL ALTER TABLE, e não será preciso usar ferramentas como o assistente de Always Encrypted no SSMS ou o cmdlet do PowerShell Set-SqlColumnEncryption.

- **Cálculos avançados** – Operações em colunas criptografadas, incluindo a correspondência de padrões (o predicado LIKE) e comparações de intervalo são compatíveis dentro do enclave seguro, que desbloqueia o Always Encrypted para uma ampla gama de aplicativos e cenários que exigem que esses cálculos sejam executados dentro do sistema de banco de dados.

## <a name="secure-enclave-attestation"></a>Atestado de enclave seguro

O enclave seguro dentro do Mecanismo do SQL Server pode acessar dados confidenciais armazenados em colunas de banco de dados criptografado e as chaves de criptografia de coluna correspondentes em texto não criptografado. Antes de enviar uma consulta que envolve cálculos de enclave para o SQL Server, o driver do cliente dentro do aplicativo precisa confirmar se o enclave seguro é um enclave genuíno com base em determinada tecnologia (por exemplo, VBS) e o código em execução dentro do enclave foi assinado para execução dentro do enclave. 

O processo de verificação do enclave é chamado de **atestado de enclave** e requer que um driver de cliente dentro do aplicativo e do SQL Server contate um serviço de atestado externo. As especificidades do processo de atestado dependem da tecnologia de enclave e do serviço de atestado.

O processo de atestado do SQL Server é compatível com enclaves seguros de VBS em [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] é o atestado de runtime de do Windows Defender System Guard, que usa o HGS (Serviço Guardião de Host) como um serviço de atestado. Você precisa configurar o HGS no seu ambiente e registrar o computador que hospeda a instância do SQL Server no HGS. Você também precisa configurar seus aplicativos cliente ou ferramentas (por exemplo, o SQL Server Management Studio) com um atestado de HGS.

## <a name="supported-client-drivers"></a>Drivers de cliente com suporte

Para usar o Always Encrypted com enclaves seguros, um aplicativo precisa usar um driver de cliente compatível com esse recurso. Você precisa configurar o aplicativo e o driver do cliente para habilitar computações enclave e atestado de enclave. Para obter detalhes, incluindo a lista de drivers de cliente com suporte, confira [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md).

## <a name="enclave-enabled-keys"></a>Chaves habilitadas para enclave

O Always Encrypted com enclaves seguros apresenta o conceito de chaves habilitadas para enclave:

- **Chave mestra de coluna habilitada para enclave** – uma chave mestra de coluna que tem a propriedade ENCLAVE_COMPUTATIONS especificada no objeto de metadados de chave mestra de coluna no banco de dados. O objeto de metadados de chave mestra de coluna também precisa conter uma assinatura válida das propriedades de metadados.
- **Chave de criptografia de coluna habilitada para enclave** – uma chave de criptografia de coluna que é criptografada com uma chave mestra de coluna habilitada para enclave.

Quando o Mecanismo do SQL Server determina as operações que, especificadas em uma consulta, precisam ser executadas dentro do enclave seguro, o Mecanismo do SQL Server solicita que o driver do cliente compartilhe as chaves de criptografia de coluna que são necessários para os cálculos com o enclave seguro. O driver de cliente compartilha as chaves de criptografia de coluna apenas quando as chaves estão habilitadas para enclave (ou seja, criptografadas com chaves mestras de coluna habilitada para enclave) e quando estão devidamente assinadas. Caso contrário, a consulta falhará.

Para obter mais informações, confira [Gerenciar chaves para Always Encrypted com enclaves seguros](always-encrypted-enclaves-manage-keys.md).

## <a name="enclave-enabled-columns"></a>Colunas habilitadas para enclave

Uma coluna habilitada para enclave é uma coluna de banco de dados criptografada com uma chave de criptografia de coluna habilitada para enclave. A funcionalidade disponível para uma coluna habilitada para enclave depende do tipo de criptografia que de coluna está usando.

- **Criptografia determinística** – Colunas habilitadas para enclave que usam criptografia determinística são compatíveis com criptografia in-loco, mas com nenhuma outra operação dentro do enclave seguro. A comparação de igualdade é compatível, mas é executada comparando o texto cifrado fora do enclave.  
- **Criptografia aleatória** – Colunas habilitadas para enclave que usam criptografia aleatória são compatíveis com criptografia in-loco, bem como com cálculos avançados dentro do enclave seguro. Os cálculos avançados compatíveis são a correspondência de padrões e os [operadores de comparação](../../../t-sql/language-elements/comparison-operators-transact-sql.md), incluindo a comparação de igualdade.

Para obter mais informações sobre os tipos de criptografia, consulte [Criptografia Always Encrypted](always-encrypted-cryptography.md).

A tabela a seguir resume a funcionalidade disponível para colunas criptografadas, dependendo se as colunas usam chaves de criptografia de coluna habilitadas para enclave e um tipo de criptografia.

| **Operação**| **A coluna NÃO é habilitada para enclave** |**A coluna NÃO é habilitada para enclave**| **A coluna é habilitada para enclave**  |**A coluna é habilitada para enclave** |
|:---|:---|:---|:---|:---|
| | **Criptografia aleatória**  | **Criptografia determinística**     | **Criptografia aleatória**      | **Criptografia determinística**     |
| **Criptografia in-loco** | Sem suporte  | Sem suporte   | Com suporte         | Com suporte    |
| **Comparação de igualdade**   | Sem suporte | Compatível fora do enclave | Compatível (dentro do enclave) | Compatível fora do enclave |
| **Operadores de comparação além de igualdade** | Sem suporte  | Sem suporte   | Com suporte      | Sem suporte     |
| **LIKE**    | Sem suporte      | Sem suporte    | Com suporte     | Sem suporte    |

A criptografia in-loco é compatível com as seguintes operações dentro do enclave:

- A criptografia inicial dos dados armazenados em uma coluna existente.
- Criptografar novamente os dados existentes em uma coluna, por exemplo:
  
  - Girar a chave de criptografia de coluna (criptografar novamente a coluna com uma nova chave).
  - Alterar o tipo de criptografia.  

- Descriptografar dados armazenados em uma coluna criptografada (converter a coluna em uma coluna de texto não criptografado).

Para que a criptografia in-loco seja possível, a chave (ou chaves) de criptografia de coluna, envolvida nas operações criptográficas, precisa ser habilitada para enclave:

- Criptografia inicial: a chave de criptografia de coluna para a coluna que está sendo criptografada precisa ser habilitada para enclave.
- Nova criptografia: ambas as chave de criptografia de coluna atual e de destino (se forem diferentes da chave atual) precisam ser habilitadas para enclave.
- Descriptografia: a chave de criptografia de coluna atual da coluna precisa ser habilitada para enclave.

### <a name="indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>Índices em colunas habilitadas para enclave com criptografia aleatória
É possível criar índices não clusterizados em colunas habilitadas para enclave usando criptografia aleatória para que as consultas avançadas sejam executadas com mais rapidez. Para garantir que um índice em uma coluna criptografada com criptografia aleatória não vaze dados confidenciais e, ao mesmo tempo, que seja útil para processamento de consultas dentro do enclave, os valores da chave na árvore B (estrutura de dados do índice) são criptografados e classificados com base nos respectivos valores de texto não criptografado. Quando o executor de consultas usa um índice em uma coluna criptografada para cálculos dentro do enclave no Mecanismo do SQL Server, ele pesquisa o índice para localizar valores específicos armazenados na coluna. Cada pesquisa pode envolver várias comparações. O executor de consultas delega cada comparação ao enclave que descriptografa um valor armazenado na coluna e o valor da chave criptografada do índice a ser comparado, realiza a comparação em texto não criptografado e retorna o resultado da comparação ao executor. 

Ainda não há suporte para criação de índices em colunas que usam criptografia aleatória e que não são habilitadas para enclave.

Para obter mais informações, confira [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md). Para obter informações gerais, não específicas do recurso Always Encrypted, sobre como a indexação funciona no SQL Server, confira [Descrição de índices clusterizados e não clusterizados](../../indexes/clustered-and-nonclustered-indexes-described.md).

#### <a name="database-recovery"></a>Recuperação de banco de dados

Quando uma instância do SQL Server falha, os respectivos bancos de dados podem ficar em um estado em que os arquivos de dados podem conter algumas modificações de transações incompletas. Quando a instância é iniciada, ela executa um processo chamado [recuperação de banco de dados](../../logs/the-transaction-log-sql-server.md#recovery-of-all-incomplete-transactions-when--is-started), que envolve a reversão de todas as transações incompletas encontradas no log de transações para garantir que a integridade do banco de dados seja preservada. Caso uma transação incompleta tenha feito alterações em um índice, essas alterações também precisam ser desfeitas. Por exemplo, talvez seja necessário remover ou reinserir alguns valores de chave no índice.

> [!IMPORTANT]
> A Microsoft recomenda habilitar a [ADR (Recuperação de Banco de dados Acelerada)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr) no banco de dados, **antes** de criar o primeiro índice em uma coluna habilitada para enclave com criptografia aleatória.

Para desfazer uma alteração feita em um índice com o [processo de recuperação de banco de dados tradicional](https://docs.microsoft.com/azure/sql-database/sql-database-accelerated-database-recovery#the-current-database-recovery-process) (que segue o modelo de recuperação [ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf)), o SQL Server precisa aguardar até que um aplicativo forneça a chave de criptografia da coluna para o enclave, o que pode levar muito tempo. A ADR reduz significativamente a quantidade de operações de desfazer que precisam ser adiadas devido a uma chave de criptografia de coluna que não está disponível no cache dentro do enclave. Consequentemente, esse recurso aumenta consideravelmente a disponibilidade do banco de dados, reduzindo a chance de uma nova transação ser bloqueada. Com a ADR habilitada, o SQL Server ainda pode precisar de uma chave de criptografia de coluna para concluir a limpeza de versões de dados anteriores, mas ele realiza esse processo como uma tarefa em segundo plano que não afeta a disponibilidade do banco de dados ou as transações do usuário. No entanto, talvez você receba mensagens de erro no log de erros, indicando falhas nas operações de limpeza devido à ausência de uma chave de criptografia da coluna.

### <a name="indexes-on-enclave-enabled-columns-using-deterministic-encryption"></a>Índices em colunas habilitadas para enclave com criptografia determinística

Um índice em uma coluna que usa criptografia determinística é classificado com base em texto cifrado (não em texto não criptografado), independentemente de a coluna ser habilitada ou não para enclave.

## <a name="security-considerations"></a>Considerações de segurança

As considerações a seguir sobre segurança se aplicam ao Always Encrypted com enclaves seguros.

- A segurança dos dados dentro do enclave depende de um protocolo e serviço de atestado. Portanto, é necessário garantir que o serviço e as políticas de atestado, bem como a aplicação do serviço de atestado, sejam gerenciados por um administrador confiável. Além disso, os serviços de atestado normalmente têm suporte para diversas políticas e protocolos de atestado, alguns dos quais realizam uma verificação mínima do enclave e do respectivo ambiente, e são projetados para fins de testes e desenvolvimento. Siga rigorosamente as diretrizes específicas do serviço de atestado para garantir que você esteja usando as configurações e políticas recomendadas para suas implantações de produção. 
- Criptografar uma coluna usando criptografia aleatória com um CEK habilitado para enclave pode resultar no vazamento da ordem dos dados armazenados na coluna, pois essas colunas têm suporte para comparações de intervalo. Por exemplo, se uma coluna criptografada contendo salários de funcionários tiver um índice, um administrador de banco de dados mal-intencionado poderá verificar o índice para encontrar o maior valor de salário criptografado e identificar uma pessoa que recebe esse salário (supondo que o nome dela não esteja criptografado). 
- Se usar o Always Encrypted para proteger dados confidenciais contra o acesso não autorizado por administradores de bancos de dados, não compartilhe as chaves mestras da coluna ou as chaves de criptografia da coluna com os administradores de bancos de dados. Um administrador de banco de dados pode gerenciar índices em colunas criptografadas sem ter acesso direto às chaves, aproveitando o cache de chaves de criptografia da coluna dentro do enclave.

## <a name="considerations-for-availability-groups-and-database-migration"></a><a name="anchorname-1-considerations-availability-groups-db-migration"></a> Considerações sobre grupos de disponibilidade e migração de banco de dados

Ao configurar um grupo de disponibilidade Always On necessário para o suporte de consultas com enclaves, você precisa garantir que todas as instâncias do SQL Server que hospedam os bancos de dados no grupo de disponibilidade tenham suporte para o recurso Always Encrypted com enclaves seguros e que tenham um enclave configurado. Se o banco de dados primário for compatível com enclaves (mas não uma réplica secundária), qualquer consulta que tente usar a funcionalidade do Always Encrypted com enclaves seguros falhará.

Quando você restaura um arquivo de backup de um banco de dados que usa a funcionalidade do Always Encrypted com enclaves seguros em uma instância do SQL Server que não tem o enclave configurado, a operação de restauração será bem-sucedida e todas as funcionalidades que não dependem do enclave ficarão disponíveis. No entanto, todas as consultas posteriores que usam a funcionalidade de enclave falharão, e os índices nas colunas habilitadas para enclave que usam criptografia aleatória ficarão inválidos. O mesmo se aplica quando você anexa um banco de dados usando o Always Encrypted com enclaves seguros na instância que não têm o enclave configurado.

Caso seu banco de dados inclua índices em colunas habilitadas para enclave com criptografia aleatória, habilite a [ADR (Recuperação de Banco de Dados Acelerada)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr) no banco de dados, antes de criar um backup. A ADR garantirá que o banco de dados, inclusive os índices, fique disponível imediatamente após a restauração. Para saber mais, confira [Recuperação de banco de dados](#database-recovery).

Quando migrar um banco de dados usando um arquivo bacpac, descarte todas as colunas de índices habilitadas para enclave com criptografia aleatória antes de criar o arquivo bacpac.

## <a name="known-limitations"></a>Limitações conhecidas
O Always Encrypted com enclaves seguros soluciona algumas limitações do Always Encrypted habilitando as seguintes operações:

- Operações criptográficas in-loco.
- Correspondência de padrões (LIKE) e operadores de comparação em colunas criptografadas com criptografia aleatória.
    > [!NOTE]
    > As operações acima são compatíveis com colunas de cadeia de caracteres que usam ordenações com classificação binário2 (ordenações BIN2). Colunas de cadeia de caracteres que usam ordenações não BIN2 podem ser criptografadas com criptografia aleatória e chaves de criptografia de coluna habilitadas para enclave. No entanto, a única nova funcionalidade habilitada para essas colunas é a criptografia no local.
- Criação de índices não clusterizados e estatísticas em colunas usando criptografia aleatória.

Todas as outras limitações do Always Encrypted listadas em [Detalhes do Recurso](always-encrypted-database-engine.md#feature-details) também se aplicam ao Always Encrypted com enclaves seguro.

As seguintes limitações são específicas do Always Encrypted com enclaves seguros:

- Não é possível criar índices clusterizados em colunas habilitadas para enclave com criptografia aleatória.
- Colunas habilitadas para enclave com criptografia aleatória não podem ser colunas de chave primária e não podem ser referenciadas por restrições de chaves estrangeiras nem por restrições de chaves exclusivas.
- Somente junções de loop aninhadas (usando índices, se disponíveis) têm suporte em colunas habilitadas para enclave usando criptografia aleatória. Não há suporte para junções hash nem para junções mescladas. 
- Operações criptográficas in-loco não podem ser combinadas com outras alterações de metadados de coluna, exceto as alterações de ordenação, na mesma página de código e nulidade. Por exemplo, não é possível criptografar, recriptografar ou descriptografar uma coluna E alterar um tipo de dados da coluna em uma única instrução `ALTER TABLE`/`ALTER COLUMN` do Transact-SQL. É necessário usar duas instruções separadas.
- Não há suporte para o uso de chaves habilitadas para enclave para colunas em tabelas na memória.
- Expressões que definem colunas computadas não podem executar cálculos em colunas habilitadas para enclave usando criptografia aleatória (mesmo que as computações forem comparações LIKE e de intervalo).
- Não há suporte para caracteres de escape em parâmetros do operador LIKE em colunas habilitadas para enclave usando criptografia aleatória.
- Consultas com o operador LIKE ou um operador de comparação que inclui um parâmetro de consulta com um dos seguintes tipos de dados (que se tornam objetos grandes após a criptografia) ignoram índices e executam verificações de tabela.
    - `nchar[n]` e `nvarchar[n]`, se n for maior que 3967.
    - `char[n]`, `varchar[n]`, `binary[n]`, `varbinary[n]`, se n for maior que 7935.
- Limitações de ferramentas:
  - Os únicos repositórios de chaves compatíveis com o armazenamento de chaves mestras de coluna habilitadas para enclave são o Repositório de Certificados do Windows e o Azure Key Vault.
  - Não há suporte para importar/exportar bancos de dados que contêm chaves habilitadas para enclave.
  - Para disparar uma operação criptográfica in-loco por meio de uma instrução `ALTER TABLE`/`ALTER COLUMN` do Transact-SQL, é necessário emitir a instrução usando uma janela de consulta no SSMS ou então, você pode escrever seu próprio programa que emite a instrução. No momento, o cmdlet Set-SqlColumnEncryption no módulo SqlServer PowerShell e o assistente de Always Encrypted no SQL Server Management Studio ainda não são compatíveis com a criptografia in-loco – eles movem os dados para fora do banco de dados para operações criptográficas, mesmo se as chaves de criptografia de coluna usadas para as operações estão habilitadas para enclave.

## <a name="next-steps"></a>Próximas etapas
- [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Configurar e usar o Always Encrypted com enclaves seguros](configure-always-encrypted-enclaves.md)

## <a name="see-also"></a>Confira também
- [Gerenciar chaves para Always Encrypted com enclaves seguros](always-encrypted-enclaves-manage-keys.md)
- [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md)
- [Consultar colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-query-columns.md)
- [Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)


