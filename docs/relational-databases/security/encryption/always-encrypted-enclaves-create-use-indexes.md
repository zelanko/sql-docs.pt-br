---
title: Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: e370af38481593404629fb3367deb3b9f54bb869
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73595671"
---
# <a name="create-and-use-indexes-on-columns-using-always-encrypted-with-secure-enclaves"></a>Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Este artigo descreve como criar e usar índices em colunas criptografadas usando chaves de criptografia de coluna habilitadas para enclave com o [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md). 

O Always Encrypted com enclaves seguros dá suporte a:
- Índices clusterizados e não clusterizados em colunas criptografadas usando a criptografia determinística e chaves habilitadas para enclave.
  - Esses índices são classificados com base no texto cifrado. Nenhuma consideração especial se aplica a esses índices. Você pode gerenciá-los e usá-los da mesma forma que os índices em colunas criptografadas usando a criptografia determinística e chaves que não são habilitadas para enclave (como ocorre com o Always Encrypted). 
- Índices não clusterizados em colunas criptografadas usando a criptografia aleatória e chaves habilitadas para enclave.
  - O processamento de consultas dentro de um enclave é útil e garante que não haja vazamento de dados confidenciais em um índice em uma coluna criptografada usando a criptografia aleatória. Os valores de chave na estrutura de dados do índice (árvore B) são criptografados e classificados com base nos valores de texto não criptografado. Para obter mais informações, confira [Índices em colunas habilitadas para enclave usando a criptografia aleatória](always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption).

> [!NOTE]
> O restante deste artigo aborda índices não clusterizados em colunas criptografadas usando a criptografia aleatória e chaves habilitadas para enclave.

Como um índice em uma coluna usando a criptografia aleatória e uma chave de criptografia de coluna habilitada para enclave contém dados criptografados (texto cifrado) classificados com base em um texto não criptografado, o Mecanismo do SQL Server precisa usar o enclave para as operações que envolvem a criação, a atualização ou a pesquisa de um índice, incluindo:

- Criar ou recriar um índice.
- Inserir, atualizar ou excluir uma linha em uma tabela (contendo uma coluna indexada/criptografada), que dispara a inserção de uma chave de índice no índice e/ou a remoção de uma chave do índice.
- Executar comandos `DBCC` que envolvam a verificação da integridade dos índices, por exemplo, [DBCC CHECKDB (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ou [DBCC CHECKTABLE (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).
- Recuperação de banco de dados (por exemplo, após uma falha e uma reinicialização do SQL Server), caso o SQL Server precise desfazer qualquer alteração no índice (mais detalhes abaixo).

Todas as operações acima exigem que o enclave tenha a chave de criptografia de coluna para a coluna indexada. A chave é necessária para descriptografar as chaves de índice. Em geral, o enclave pode obter uma chave de criptografia de coluna de duas maneiras:
- Diretamente do aplicativo cliente.
- No cache das chaves de criptografia de coluna.

## <a name="invoke-indexing-operations-with-column-encryption-keys-provided-directly-by-the-client"></a>Invocar operações de indexação com chaves de criptografia de coluna fornecidas diretamente pelo cliente
Para que esse método de invocar operações de indexação funcione, o aplicativo (incluindo uma ferramenta, como o SSMS [SQL Server Management Studio]) emissor de uma consulta que dispara uma operação em um índice precisa:

- Conectar-se ao banco de dados com o Always Encrypted e os cálculos de enclave habilitados para a conexão de banco de dados.
- O aplicativo precisa ter acesso à chave mestra da coluna que protege a chave de criptografia da coluna indexada.

Depois que o Mecanismo do SQL Server analisa a consulta do aplicativo e determina a necessidade de atualizar um índice em uma coluna criptografada para executar a consulta, ele instrui o driver do cliente a fornecer a chave de criptografia de coluna necessária ao enclave por meio de um canal de segurança. Esse é exatamente o mesmo mecanismo usado para fornecer o enclave com chaves de criptografia de coluna para processamento de todas as outras consultas. Por exemplo, a criptografia in-loco ou consultas que usam a correspondência de padrões e comparações de intervalo.

Esse método é útil para garantir que a presença de índices em colunas criptografadas seja transparente para os aplicativos que já estão conectados ao banco de dados com o Always Encrypted e os cálculos de enclave habilitados. A conexão de aplicativo pode usar o enclave para o processamento de consulta. Depois de criar um índice em uma coluna, o driver dentro de seu aplicativo fornece de forma transparente as chaves de criptografia de coluna ao enclave para operações de indexação. Observe que a criação de índices pode aumentar o número de consultas que exigem que o aplicativo envie a as chaves de criptografia de coluna para o enclave.

Para usar esse método, siga as diretrizes gerais para executar consultas usando um enclave seguro em [Consultar colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-query-columns.md).

Para obter instruções passo a passo sobre como usar esse método, confira o [Tutorial: Criando e usando índices em colunas habilitadas para enclave com criptografia aleatória](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md).

## <a name="invoke-indexing-operations-using-cached-column-encryption-keys"></a>Invocar operações de indexação usando chaves de criptografia de coluna armazenadas em cache

Depois que um aplicativo cliente envia uma chave de criptografia de coluna para o enclave para processamento de qualquer consulta que exija cálculos de enclave, o enclave armazena a chave de criptografia de coluna em um cache interno. Esse cache está localizado dentro do enclave e é inacessível externamente.

Se o mesmo ou outro aplicativo cliente usado pelo mesmo ou por outro usuário disparar uma operação em um índice sem fornecer diretamente a criptografia de coluna necessária, o enclave pesquisará a chave de criptografia de coluna no cache. Como resultado, a operação de índice é bem-sucedida, embora o aplicativo cliente ainda não tenha fornecido a chave.

Para que esse método de invocação de operações de indexação funcione, o aplicativo deve se conectar ao banco de dados sem o Always Encrypted habilitado para a conexão e a chave de criptografia de coluna necessária deve estar disponível no cache dentro do enclave.

Só há suporte para esse método de invocação de operações em consultas que não exigem chaves de criptografia de coluna para outras operações, não relacionadas a índices. Por exemplo, um aplicativo que insere uma linha usando uma instrução `INSERT` em uma tabela que contém uma coluna criptografada precisa se conectar ao banco de dados com o Always Encrypted habilitado na cadeia de conexão e ter acesso às chaves, independentemente de a coluna criptografada ter um índice ou não.

Esse método é útil para:
 - Garantir que a presença de índices em colunas habilitadas para enclave usando criptografia aleatória seja transparente para aplicativos e usuários que não tenham acesso a chaves e aos dados em texto não criptografado. 
 - Isso garante que a criação de um índice em uma coluna criptografada não interrompa as consultas existentes. Se um aplicativo emite uma consulta em uma tabela que contém colunas criptografadas sem a necessidade de ter acesso às chaves, ele pode continuar sendo executado sem ter acesso às chaves depois que um DBA cria um índice. Por exemplo, considere um aplicativo que executa a consulta abaixo na tabela **Funcionários** que contém colunas criptografadas. O DBA não criou um índice em nenhuma coluna criptografada.

   ```sql
   DELETE FROM [dbo].[Employees] WHERE [EmployeeID] = 1;
   GO
   ```

   Se o aplicativo enviar a consulta em uma conexão sem o Always Encrypted e os cálculos de enclave habilitados, a consulta terá sucesso. A consulta não dispara nenhum cálculo em colunas criptografadas. Depois que um DBA cria um índice em uma coluna criptografada, a consulta dispara a remoção de chaves de índice dos índices. O enclave precisa das chaves de criptografia de coluna nessa situação. No entanto, o aplicativo poderá continuar a executar essa consulta na mesma conexão, desde que um proprietário de dados forneça as chaves de criptografia de coluna para o enclave.

 - Para obter a separação de funções ao gerenciar índices, pois ele permite que os DBAs criem e alterem índices em colunas criptografadas sem a necessidade de acesso a dados confidenciais. 

> [!TIP] 
> [sp_enclave_send_keys (Transact-SQL)](../../system-stored-procedures/sp-enclave-send-keys-sql.md) permite enviar com facilidade todas as chaves de criptografia de coluna habilitadas para enclave usadas para índices ao enclave e popular o cache de chaves.

Para obter instruções passo a passo sobre como usar esse método, confira o [Tutorial: Criando e usando índices em colunas habilitadas para enclave com criptografia aleatória](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md). 

## <a name="next-steps"></a>Próximas etapas
- [Consultar colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-query-columns.md).

## <a name="see-also"></a>Consulte Também  
- [Tutorial: Criando e usando índices em colunas habilitadas para enclave com criptografia aleatória](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md).
- [sp_enclave_send_keys (Transact-SQL)](../../system-stored-procedures/sp-enclave-send-keys-sql.md)
