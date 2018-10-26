---
title: Always Encrypted com enclaves seguros (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 742c3dfb66add1a8e81fb9f530923b11e17bfea8
ms.sourcegitcommit: 0acd84d0b22a264b3901fa968726f53ad7be815c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49307110"
---
# <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted com enclaves seguros
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]


O Always Encrypted com enclaves seguros fornece funcionalidade adicional para o recurso [Always Encrypted](always-encrypted-database-engine.md).

Introduzido no SQL Server 2016, o Always Encrypted protege a confidencialidade dos dados confidenciais contra malwares e usuários com altos privilégios *não autorizados* do SQL Server. Usuários com altos privilégios não autorizados são DBAs, administradores de computador, administradores de nuvem ou qualquer outra pessoa que tenha acesso legítimo a instâncias do servidor, hardware, etc., mas que não poderia ter acesso à parte ou todos os dados reais. 

Até agora, o Always Encrypted protegia os dados criptografando-os no lado do cliente e nunca permitindo que os dados ou as chaves de criptografia correspondentes aparecessem em texto não criptografado dentro do Mecanismo do SQL Server. Como resultado, a funcionalidade em colunas criptografadas dentro do banco de dados ficava rigorosamente restrita. As únicas operações que o SQL Server podia executar nos dados criptografados eram as comparações de igualdade (que só estavam disponíveis com a criptografia determinística). Todas as outras operações, incluindo operações criptográficas (criptografia de dados inicial ou rotação de chave) ou cálculos avançados (por exemplo, correspondência de padrões) não eram compatíveis com o interior do banco de dados. Os usuários precisavam mover os dados para fora do banco de dados para executar essas operações no lado do cliente.

O Always Encrypted *com enclaves seguros* soluciona essas limitações, permitindo realizar cálculos em dados de texto não criptografado em um enclave seguro no lado do servidor. Um enclave seguro é uma região protegida de memória dentro do processo do SQL Server e atua como um ambiente de execução confiável para o processamento de dados confidenciais dentro do mecanismo do SQL Server. Um enclave seguro é exibido como uma caixa preta para o restante do SQL Server e outros processos no computador de hospedagem. Não há nenhuma maneira de exibir os dados ou o código dentro do enclave de fora, mesmo com um depurador.  


O Always Encrypted usa enclaves seguros, conforme ilustrado no diagrama a seguir:

![fluxo de dados](./media/always-encrypted-enclaves/ae-data-flow.png)



Durante a análise de uma consulta do aplicativo, o Mecanismo do SQL Server determina se a consulta contém alguma operação em dados criptografados que exige o uso do enclave seguro. Para consultas em que o enclave seguro precisa ser acessado:

- O driver do cliente envia as chaves de criptografia de coluna necessárias para as operações para o enclave seguro (por um canal seguro). 
- Em seguida, o driver do cliente envia a consulta para execução junto com os parâmetros da consulta criptografada.

Durante o processamento de consulta, os dados ou as chaves de criptografia de coluna não são expostos em texto não criptografado no Mecanismo do SQL Server fora do enclave seguro. O mecanismo do SQL Server delega operações criptográficas e cálculos em colunas criptografadas para o enclave seguro. Se necessário, o enclave seguro descriptografa os parâmetros de consulta e/ou os dados armazenados em colunas criptografadas e executa as operações solicitadas.

## <a name="why-use-always-encrypted-with-secure-enclaves"></a>Por que usar o Always Encrypted com enclaves seguros?

Com enclaves seguros, o Always Encrypted protege a confidencialidade dos dados confidenciais, fornecendo os seguintes benefícios:

- **Criptografia in-loco** – Operações criptográficas em dados confidenciais, por exemplo: criptografia de dados ou rotação de uma chave de criptografia de coluna são executadas dentro do enclave seguro e não exigem a movimentação dos dados para fora do banco de dados. Você pode emitir a criptografia in-loco usando a instrução Transact-SQL ALTER TABLE, e não será preciso usar ferramentas como o assistente de Always Encrypted no SSMS ou o cmdlet do PowerShell Set-SqlColumnEncryption.

- **Cálculos avançados (versão prévia)** – Operações em colunas criptografadas, incluindo a correspondência de padrões (o predicado LIKE) e comparações de intervalo são compatíveis dentro do enclave seguro, que desbloqueia o Always Encrypted para uma ampla gama de aplicativos e cenários que exigem que esses cálculos sejam executados dentro do sistema de banco de dados.

> [!IMPORTANT]
> Em [!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)], os cálculos avançados estão aguardando várias otimizações de desempenho, incluindo a funcionalidade limitada (sem indexação, etc) e estão desabilitados por padrão no momento. Para habilitar cálculos avançados, consulte [Habilitar cálculos avançados](configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

Em [!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)], o Always Encrypted com enclaves seguros usa enclaves de memória seguros com [VBS (Segurança baseada em Virtualização)](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) (também conhecido como enclaves VSM, ou Modo Seguro Virtual) no Windows.

## <a name="secure-enclave-attestation"></a>Atestado de enclave seguro

O enclave seguro dentro do Mecanismo do SQL Server pode acessar dados confidenciais armazenados em colunas de banco de dados criptografado e as chaves de criptografia de coluna correspondentes em texto não criptografado. Antes de enviar uma consulta que envolve cálculos de enclave para o SQL Server, o driver do cliente dentro do aplicativo precisa confirmar se o enclave seguro é um enclave genuíno com base em determinada tecnologia (por exemplo, VBS) e o código em execução dentro do enclave foi assinado para execução dentro do enclave. 

O processo de confirmação do enclave é chamado de **atestado de enclave**, e geralmente requer que um driver de cliente dentro do aplicativo (e, às vezes, também do SQL Server) entre em contato com um serviço de atestado externo. As especificidades do processo de atestado dependem da tecnologia de enclave e do serviço de atestado.

O processo de atestado do SQL Server é compatível com enclaves seguros de VBS em [!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)] é o atestado de tempo de execução de do Windows Defender System Guard, que usa o HGS (Serviço Guardião de Host) como um serviço de atestado. Você precisa configurar o HGS no seu ambiente e registrar o computador que hospeda a instância do SQL Server no HGS. Você também precisa configurar seus aplicativos cliente ou ferramentas (por exemplo, o SQL Server Management Studio) com um atestado de HGS.

## <a name="secure-enclave-providers"></a>Provedores de enclave seguro

Para usar o Always Encrypted com enclaves seguros, um aplicativo precisa usar um driver de cliente compatível com esse recurso. No [!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)], seus aplicativos precisam usar o .NET Framework 4.7.2 e o Provedor de Dados do .NET Framework para SQL Server. Além disso, os aplicativos .NET precisam ser configurados com um **provedor de enclave seguro** específico para o tipo de enclave (por exemplo, VBS) e o serviço de atestado (por exemplo, HGS) que você está usando. Os provedores de enclave compatíveis são fornecidos separadamente em um pacote NuGet, que você precisa integrar ao seu aplicativo. Um provedor de enclave implementa a lógica do lado do cliente para o protocolo de atestado e estabelece um canal seguro com um enclave seguro de um tipo determinado.

## <a name="enclave-enabled-keys"></a>Chaves habilitadas para enclave

O Always Encrypted com enclaves seguros apresenta o conceito de chaves habilitadas para enclave:

- **Chave mestra de coluna habilitada para enclave** – Uma chave mestra de coluna que tem a propriedade ENCLAVE_COMPUTATIONS especificada no objeto de metadados de chave mestra de coluna no banco de dados. O objeto de metadados de chave mestra de coluna também precisa conter uma assinatura válida das propriedades de metadados.
- **Chave de criptografia de coluna habilitada para enclave** – Uma chave de criptografia de coluna que é criptografada com uma chave mestra de coluna habilitada para enclave.

Quando o Mecanismo do SQL Server determina as operações que, especificadas em uma consulta, precisam ser executadas dentro do enclave seguro, o Mecanismo do SQL Server solicita que o driver do cliente compartilhe as chaves de criptografia de coluna que são necessários para os cálculos com o enclave seguro. O driver do cliente compartilha as chaves de criptografia de coluna apenas se as chaves estiverem habilitada para enclave (ou seja, criptografadas com chaves mestras de coluna habilitada para enclave) e se estiverem devidamente assinadas. Caso contrário, a consulta falhará.

## <a name="enclave-enabled-columns"></a>Colunas habilitadas para enclave

Uma coluna habilitada para enclave é uma coluna de banco de dados criptografada com uma chave de criptografia de coluna habilitada para enclave. A funcionalidade disponível para uma coluna habilitada para enclave depende do tipo de criptografia que de coluna está usando.

- **Criptografia determinística** – Colunas habilitadas para enclave que usam criptografia determinística são compatíveis com criptografia in-loco, mas com nenhuma outra operação dentro do enclave seguro. A comparação de igualdade é compatível, mas ela é executada fora do enclave, comparando o texto cifrado (fora do enclave).  
- **Criptografia aleatória** – Colunas habilitadas para enclave que usam criptografia aleatória são compatíveis com criptografia in-loco, bem como com cálculos avançados dentro do enclave seguro. Os cálculos avançados compatíveis são a correspondência de padrões e os [operadores de comparação](https://docs.microsoft.com/sql/t-sql/language-elements/comparison-operators-transact-sql), incluindo a comparação de igualdade.

Para obter mais informações sobre os tipos de criptografia, consulte [Criptografia Always Encrypted](always-encrypted-cryptography.md).

A tabela a seguir resume a funcionalidade disponível para colunas criptografadas, dependendo se as colunas usam chaves de criptografia de coluna habilitadas para enclave e um tipo de criptografia.

| **Operação**| **A coluna NÃO é habilitada para enclave** |**A coluna NÃO é habilitada para enclave**| **A coluna é habilitada para enclave**  |**A coluna é habilitada para enclave** |
|:---|:---|:---|:---|:---|
| | **Criptografia aleatória**  | **Criptografia determinística**     | **Criptografia aleatória**      | **Criptografia determinística**     |
| **Criptografia in-loco** | Incompatível  | Incompatível   | Tem suporte         | Tem suporte    |
| **Comparação de igualdade**   | Incompatível | Compatível fora do enclave | Compatível (dentro do enclave) | Compatível fora do enclave |
| **Operadores de comparação além de igualdade** | Incompatível  | Incompatível   | Tem suporte      | Incompatível     |
| **LIKE**    | Incompatível      | Incompatível    | Tem suporte     | Incompatível    |

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

## <a name="known-limitations"></a>Limitações conhecidas

Limitações gerais: 

- Todas as limitações listadas para a versão atual do Always Encrypted nos [Detalhes do recurso](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine#feature-details) também se aplicam ao Always Encrypted com enclaves seguros (para colunas criptografadas com chaves habilitadas para enclave), exceto as restrições que são removidas ao adicionar a compatibilidade com criptografia in-loco e cálculos avançados.

- A comparação de igualdade continua sendo o único operador de Transact-SQL compatível com a criptografia determinística e as comparações de igualdade são executadas comparando valores de texto cifrado fora do enclave, independentemente se a chave de criptografia de colunas foi habilitada para enclave ou não. A única funcionalidade nova desbloqueada com chaves de criptografia de coluna habilitadas para enclave para criptografia determinística são as operações criptográficas in-loco. Se tiver uma coluna criptografada usando a criptografia determinística (e uma chave que não é habilitada para enclave), você precisará criptografar novamente a coluna usando criptografia aleatória para habilitar cálculos avançados (operações de comparação de correspondência de padrões).

- A restrição existente do uso de agrupamentos se aplica a colunas criptografadas com chaves de criptografia de coluna habilitada para enclave: as colunas de cadeia de caracteres (char, nchar, varchar, nvarchar) criptografadas usando criptografia determinística precisam usar agrupamentos com uma ordem de classificação binary2 (agrupamentos BIN2). Colunas de cadeias de caracteres que usam agrupamentos diferentes de BIN2 podem ser criptografadas usando a criptografia aleatória – no entanto, a única funcionalidade nova que está habilitada para essas colunas (se forem criptografadas com chaves de criptografia de coluna habilitadas para enclave) é a criptografia in-loco. **Para ser compatível com cálculos avançados (correspondência de padrões, operações de comparação) uma coluna precisa usar um agrupamento BIN2** (e a coluna precisa ser criptografada usando criptografia aleatória e uma chave de criptografia de coluna habilitada para enclave).

- O uso de chaves habilitadas para enclave para colunas em tabelas na memória não é compatível.

- Operações criptográficas in-loco não podem ser combinadas com outras alterações de metadados de coluna, exceto as alterações de agrupamento e de nulidade. Por exemplo, não é possível criptografar, recriptografar ou descriptografar uma coluna E alterar um tipo de dados da coluna em uma única instrução Transact-SQL ALTER TABLE ou ALTER COLUMN. Você precisará usar duas instruções separadas.

As seguintes limitações se aplicam à Versão prévia atual, mas estão em nossos planos para serem solucionadas:

- Colunas habilitadas para enclave que usam criptografia aleatória não podem ser indexadas, o que significa que as operações de comparação ou operações LIKE exigem verificações de tabela.

- O único driver de cliente compatível com Always Encrypted com enclaves seguros é o Provedor de Dados do .NET Framework para SQL Server (ADO.NET) no .NET Framework 4.7.2. Não há compatibilidade com o ODBC/JDBC.

- Os únicos repositórios de chaves compatíveis com o armazenamento de chaves mestras de coluna habilitadas para enclave são o Repositório de Certificados do Windows e o Azure Key Vault.

- A compatibilidade de ferramentas com o Always Encrypted com enclaves seguros está incompleta no momento. Para disparar uma operação criptográfica in-loco por meio de uma instrução Transact-SQL ALTER TABLE, é necessário emitir a instrução usando uma janela de consulta no SSMS ou então, você pode escrever seu próprio programa que emite a instrução. O cmdlet Set-SqlColumnEncryption no módulo SqlServer PowerShell e o assistente de Always Encrypted no SQL Server Management Studio ainda não são compatíveis com a criptografia in-loco – atualmente, ambas as ferramentas movem os dados para fora do banco de dados para operações criptográficas, mesmo se as chaves de criptografia de coluna usadas para as operações forem habilitadas para enclave. 

## <a name="known-issues"></a>Problemas conhecidos

- Cálculos avançados em colunas de cadeia de caracteres não UNICODE (char, varchar) exigem que um agrupamento BIN2 seja definido no nível do banco de dados. Consulte as Considerações especiais sobre colunas de cadeia de caracteres não UNICODE em [Gerenciar agrupamentos](configure-always-encrypted-enclaves.md#manage-collations).

## <a name="next-steps"></a>Next Steps

- Configure seu ambiente de teste e experimente a funcionalidade do Always Encrypted com enclaves seguros no SSMS – consulte [Tutorial: introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).