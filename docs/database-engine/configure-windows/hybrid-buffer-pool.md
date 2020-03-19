---
title: Pool de buffers híbrido | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: 1d1e595918b33ae4fcc11cd59bf0964b2e6d919c
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112285"
---
# <a name="hybrid-buffer-pool"></a>Pool de Buffers Híbrido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O pool de buffers híbrido permite que objetos do pool de buffers façam referência a páginas de dados em arquivos de banco de dados que residem em dispositivos de memória persistente (PMEM), em vez de cópias das páginas de dados armazenadas em cache na DRAM volátil. Esse recurso foi introduzido no [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)].

![Pool de Buffers Híbrido](./media/hybrid-buffer-pool.png)

Os dispositivos de memória persistente (PMEM) são endereçáveis por byte e se um sistema de arquivos com reconhecimento de memória persistente do DAX (acesso direto) (como XFS, EXT4 ou NTFS) for usado, os arquivos no sistema de arquivos poderão ser acessados usando as APIs de sistema de arquivos usuais no sistema de arquivos. Como alternativa, ele pode executar o que é conhecido como operações de carregamento e armazenamento em relação aos mapas de memória dos arquivos no dispositivo. Isso permite que aplicativos de reconhecimento de PMEM, como SQL Server, acessem arquivos no dispositivo sem atravessar a pilha de armazenamento tradicional.

O pool de buffers híbrido usa essa capacidade de executar operações de carregamento e armazenamento em arquivos mapeados de memória, para aproveitar o dispositivo PMEM como cache para o pool de buffers, bem como armazenar arquivos de banco de dados. Isso cria a situação única em que uma leitura lógica e uma leitura física são essencialmente a mesma operação. Os dispositivos de memória persistentes podem ser acessados por meio do barramento de memória, assim como a DRAM volátil normal.

Somente as páginas de dados limpas são armazenadas em cache no dispositivo para o pool de buffers híbrido. Quando uma página é marcada como suja, ela é copiada para o pool de buffers da DRAM antes de ser finalmente gravada mais uma vez no dispositivo PMEM e marcada como limpa de novo. Isso ocorrerá durante as operações de ponto de verificação regulares de maneira semelhante àquela executada em relação a um dispositivo de bloco padrão.

O recurso de pool de buffers híbrido está disponível para o Windows e o Linux. O dispositivo PMEM precisa ser formatado com um sistema de arquivos que dá suporte ao DAX (DirectAccess). Os sistemas de arquivos XFS, EXT4 e NTFS têm suporte para o DAX. O SQL Server detectará automaticamente se os arquivos de dados residirem em um dispositivo PMEM formatado corretamente e executará o mapeamento de memória de arquivos de banco de dados durante a inicialização, quando um novo banco de dados for anexado, restaurado ou criado.

Para obter mais informações, consulte:

* [Entender e implantar a memória persistente (Windows)](/windows-server/storage/storage-spaces/deploy-pmem/)
* [Configurar a memória persistente (PMEM) para o SQL Server em Linux](../../linux/sql-server-linux-configure-pmem.md)


## <a name="enable-hybrid-buffer-pool"></a>Habilitar o pool de buffers híbrido

O [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] introduz a DDL (Dynamic Data Language) para controlar o pool de buffers híbrido.

O seguinte exemplo habilita o pool de buffers híbrido em uma instância do SQL Server:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

Por padrão, o pool de buffers híbrido é desabilitado no escopo da instância. Observe que, para a alteração de configuração entrem em vigor, a instância do SQL Server deve ser reiniciada. Uma reinicialização é necessária para facilitar a alocação de páginas suficientes de hash para levar em conta a capacidade total de PMEM no servidor.

O exemplo a seguir habilita o pool de buffers híbrido em um banco de dados específico.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

Por padrão, o pool de buffers híbrido está habilitado no escopo do banco de dados.

## <a name="disable-hybrid-buffer-pool"></a>Desabilitar o pool de buffers híbrido

O exemplo seguinte desabilita o pool de buffers híbrido no nível da instância:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

Por padrão, o pool de buffers híbrido é desabilitado no nível da instância. Para que essa alteração entre em vigor, a instância deve ser reiniciada. Isso garante que páginas de hash suficientes sejam alocadas para o pool de buffers, já que a capacidade da PMEM no servidor agora precisa ser considerada.

O exemplo a seguir desabilita o pool de buffers híbrido em um banco de dados específico.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

Por padrão, o pool de buffers híbrido está habilitado no escopo do banco de dados.

## <a name="view-hybrid-buffer-pool-configuration"></a>Exibir a configuração do pool de buffers híbrido

O exemplo a seguir retorna o status atual da configuração pool de buffers híbrido da instância.

```sql
SELECT * FROM
sys.server_memory_optimized_hybrid_buffer_pool_configuration;
```

O exemplo a seguir lista os bancos de dados e a configuração no nível de banco de dados para o pool de buffers híbrido (`is_memory_optimized_enabled`).

```sql
SELECT name, is_memory_optimized_enabled FROM sys.databases;
```

## <a name="best-practices-for-hybrid-buffer-pool"></a>Melhores práticas para o pool de buffers híbrido

Ao formatar seu dispositivo PMEM no Windows, use o maior tamanho de unidade de alocação disponível para NTFS (2 MB no Windows Server 2019) e verifique se o dispositivo foi formatado para o DAX (Direct Access).

Use o modelo de alocação de memória de página grande, que pode ser habilitado com o [sinalizador de rastreamento 834](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). O sinalizador de rastreamento 834 é um sinalizador de rastreamento de inicialização.

Usar o modelo de alocação de memória de página grande requer o uso de [páginas bloqueadas na memória](./enable-the-lock-pages-in-memory-option-windows.md) no Windows.

Os tamanhos de arquivos devem ser um múltiplo de 2 MB (2 MB de módulo deve igual a zero).

Se a configuração com escopo do servidor para o pool de buffers híbrido for desabilitada, o recurso não será usado por nenhum banco de dados de usuário.

Se a configuração com escopo do servidor para o pool de buffers híbrido estiver habilitada, você poderá usar a configuração com escopo do banco de dados para desabilitar o recurso para bancos de dados de usuário individuais.
