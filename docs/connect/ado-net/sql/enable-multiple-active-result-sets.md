---
title: Habilitando conjuntos de resultados ativos múltiplos
description: Discute como usar o MARS com o SQL Server.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d0c40df5ec7648b7073f9efa369428b8d88f6d11
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452221"
---
# <a name="enabling-multiple-active-result-sets"></a>Habilitando conjuntos de resultados ativos múltiplos

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

MARS (vários conjuntos de resultados ativos) é um recurso que funciona com SQL Server para permitir a execução de vários lotes em uma única conexão. Quando o MARS está habilitado para uso com SQL Server, cada objeto de comando usado adiciona uma sessão à conexão.  
  
> [!NOTE]
>  Uma única sessão MARS abre uma conexão lógica para o MARS usar e, em seguida, uma conexão lógica para cada comando ativo.  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>Habilitando e desabilitando MARS na cadeia de conexão  
  
> [!NOTE]
>  As cadeias de conexão a seguir usam o banco de dados de exemplo **AdventureWorks** incluído com o SQL Server. As cadeias de conexão fornecidas pressupõem que o banco de dados está instalado em um servidor chamado MSSQL1. Modifique a cadeia de conexão conforme necessário para o seu ambiente.  
  
O recurso MARS está desabilitado por padrão. Ele pode ser habilitado adicionando o par de palavras-chave "MultipleActiveResultSets = true" à sua cadeia de conexão. "True" é o único valor válido para habilitar MARS. O exemplo a seguir demonstra como se conectar a uma instância do SQL Server e como especificar que o MARS deve ser habilitado. 
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
Você pode desabilitar o MARS adicionando o par de palavras-chave "MultipleActiveResultSets = false" à sua cadeia de conexão. "False" é o único valor válido para desabilitar MARS. A cadeia de conexão a seguir demonstra como desabilitar o MARS.  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>Considerações especiais ao usar MARS  
Em geral, os aplicativos existentes não devem precisar de modificação para usar uma conexão habilitada para MARS. No entanto, se você quiser usar recursos de MARS em seus aplicativos, você deve entender as considerações especiais a seguir.  
  
### <a name="statement-interleaving"></a>Intercalação de instrução  
As operações de MARS são executadas de forma síncrona no servidor. É permitida a intercalação de instrução de instruções SELECT e BULK INSERT. No entanto, as instruções DML (linguagem de manipulação de dados) e DDL (linguagem de definição de dados) são executadas atomicamente. Todas as instruções que tentarem ser executadas enquanto um lote atômico estiver sendo executado serão bloqueadas. A execução paralela no servidor não é um recurso MARS.  
  
Se dois lotes forem enviados em uma conexão MARS, um deles contendo uma instrução SELECT, o outro contendo uma instrução DML, o DML poderá iniciar a execução na execução da instrução SELECT. No entanto, a instrução DML deve ser executada até a conclusão para que a instrução SELECT possa progredir. Se ambas as instruções estiverem em execução na mesma transação, todas as alterações feitas por uma instrução DML após a instrução SELECT começarem a execução não serão visíveis para a operação de leitura.  
  
Uma instrução WAITFOR dentro de uma instrução SELECT não produz a transação enquanto ela está aguardando, ou seja, até que a primeira linha seja produzida. Isso implica que nenhum outro lote pode ser executado na mesma conexão enquanto uma instrução WAITFOR está aguardando.  
  
### <a name="mars-session-cache"></a>Cache de sessão MARS  
Quando uma conexão é aberta com o MARS habilitado, uma sessão lógica é criada, o que adiciona sobrecarga adicional. Para reduzir a sobrecarga e melhorar o desempenho, o **SqlClient** armazena em cache a sessão de MARS dentro de uma conexão. O cache contém no máximo 10 sessões MARS. Este valor não é ajustável pelo usuário. Se o limite de sessão for atingido, uma nova sessão será criada — um erro não será gerado. O cache e as sessões contidas nele são por conexão; Eles não são compartilhados entre conexões. Quando uma sessão é liberada, ela é retornada ao pool, a menos que o limite superior do pool tenha sido atingido. Se o pool de cache estiver cheio, a sessão será fechada. As sessões MARS não expiram. Eles são limpos apenas quando o objeto de conexão é Descartado. O cache da sessão MARS não está pré-carregado. Ele é carregado, pois o aplicativo requer mais sessões.  
  
### <a name="thread-safety"></a>Acesso thread-safe  
As operações MARS não são thread-safe.  
  
### <a name="connection-pooling"></a>Pool de conexões  
Conexões habilitadas para MARS são agrupadas como qualquer outra conexão. Se um aplicativo abrir duas conexões, uma com o MARS habilitado e outra com o MARS desabilitado, as duas conexões estarão em pools separados.
  
### <a name="sql-server-batch-execution-environment"></a>Ambiente de execução de SQL Server lote  
Quando uma conexão é aberta, um ambiente padrão é definido. Esse ambiente é então copiado para uma sessão MARS lógica.  
  
O ambiente de execução em lotes inclui os seguintes componentes:  
  
- Definir opções (por exemplo, ANSI_NULLS, DATE_FORMAT, idioma, TEXTSIZE)  
  
- Contexto de segurança (função de usuário/aplicativo)  
  
- Contexto de banco de dados (banco de dados atual)  
  
- Variáveis de estado de execução (por exemplo, @ @ERROR, @ @ROWCOUNT, @ @FETCH_STATUS @ @IDENTITY)  
  
- Tabelas temporárias de alto nível  
  
Com o MARS, um ambiente de execução padrão é associado a uma conexão. Cada lote novo que inicia a execução sob uma determinada conexão recebe uma cópia do ambiente padrão. Sempre que o código é executado em um determinado lote, todas as alterações feitas no ambiente têm o escopo definido para o lote específico. Quando a execução termina, as configurações de execução são copiadas no ambiente padrão. No caso de um único lote que emite vários comandos a serem executados sequencialmente sob a mesma transação, a semântica é a mesma que aquelas expostas por conexões que envolvem clientes ou servidores anteriores.  
  
### <a name="parallel-execution"></a>Execução paralela  
O MARS não foi projetado para remover todos os requisitos de várias conexões em um aplicativo. Se um aplicativo precisar de execução paralela real de comandos em um servidor, várias conexões deverão ser usadas.  
  
Por exemplo, considere os seguintes cenários. Dois objetos de comando são criados, um para processamento de um conjunto de resultados e outro para a atualização de dados; Eles compartilham uma conexão comum via MARS. Neste cenário, a `Transaction`.`Commit` falha na atualização até que todos os resultados tenham sido lidos no primeiro objeto de comando, gerando a seguinte exceção:  
  
Mensagem: o contexto da transação está sendo usado por outra sessão.  
  
Fonte: Microsoft SqlClient Provedor de Dados  
  
Esperado: (nulo)  
  
Recebido: Microsoft. Data. SqlClient. SqlException  
  
Há três opções para lidar com este cenário:  
  
- Inicie a transação depois que o leitor for criado, para que ele não faça parte da transação. Cada atualização torna-se sua própria transação.  
  
- Confirmar todo o trabalho após o leitor ser fechado. Isso tem o potencial para um lote substancial de atualizações.  
  
- Não usar MARS; em vez disso, use uma conexão separada para cada objeto de comando como você teria antes de MARS.  
  
### <a name="detecting-mars-support"></a>Detectando suporte a MARS  
Um aplicativo pode verificar o suporte a MARS lendo o valor de `SqlConnection.ServerVersion`. O número principal deve ser 9 para SQL Server 2005 e 10 para SQL Server 2008.  
  
## <a name="next-steps"></a>Próximas etapas
- [MARS (conjunto de resultados ativos múltiplos)](multiple-active-result-sets-mars.md)
