---
title: Pool de buffers híbrido | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: DBArgenis
ms.author: argenisf
manager: jroth
ms.openlocfilehash: ce63196cb8a5c8791eb6440f69cf06194591f422
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785293"
---
# <a name="hybrid-buffer-pool"></a>Pool de Buffers Híbrido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O Pool de Buffers Híbrido permite que o mecanismo de banco de dados acesse diretamente as páginas de dados em arquivos de banco de dados armazenados em dispositivos PMEM (memória persistente). Esse recurso foi introduzido no [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)].

Em um sistema tradicional sem PMEM, o SQL Server armazena as páginas de dados em cache no pool de buffers baseados em DRAM. Com o pool de buffers híbrido, o SQL Server ignora a execução de uma cópia da página para a parte do pool de buffers baseada em DRAM. Em vez disso, ele acessa a página diretamente no arquivo de banco de dados que residem no dispositivo PMEM. O acesso aos arquivos de dados em dispositivos PMEM para o pool de buffers híbrido é realizado usando o MMIO (E/S mapeada em memória), também conhecido como *capacitação* dos arquivos de dados no SQL Server.

Somente páginas limpas podem ser acessadas diretamente em um dispositivo PMEM. Quando uma página é marcada como suja, ela é copiada para o pool de buffers baseados em DRAM antes de ser finalmente gravada mais uma vez no dispositivo PMEM e marcada como limpa de novo. Esse processo acontece durante as operações de ponto de verificação regulares.

O recurso de pool de buffers híbrido está disponível para o Windows e o Linux. O dispositivo PMEM precisa ser formatado com um sistema de arquivos que dá suporte ao DAX (DirectAccess). Os sistemas de arquivos XFS, EXT4 e NTFS têm suporte para o DAX. O SQL Server detectará automaticamente se os arquivos de dados residirem em um dispositivo PMEM adequadamente formatado e realizará o mapeamento de memória no espaço do usuário. Esse mapeamento acontece na inicialização, quando um novo banco de dados é anexado, restaurado ou criado ou quando o recurso de pool de buffers híbrido é habilitado para um banco de dados.

Para obter mais informações sobre o suporte do Windows Server para PMEM, veja [Implantar memória persistente no Windows Server](/windows-server/storage/storage-spaces/deploy-pmem/).

Para saber mais sobre como configurar o SQL Server em Linux para dispositivos PMEM, veja [Implantar a memória persistente](../../linux/sql-server-linux-configure-pmem.md).

## <a name="enable-hybrid-buffer-pool"></a>Habilitar o pool de buffers híbrido

O [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] introduz a DDL (Dynamic Data Language) para controlar o pool de buffers híbrido.

O seguinte exemplo habilita o pool de buffers híbrido em uma instância do SQL Server:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

Por padrão, o pool de buffers híbrido é definido como desabilitado no escopo da instância. Observe que, para a alteração de configuração entrem em vigor, a instância do SQL Server deve ser reiniciada. Uma reinicialização é necessária para facilitar a alocação de páginas suficientes de hash para levar em conta a capacidade total de PMEM no servidor.

O exemplo a seguir habilita o pool de buffers híbrido em um banco de dados específico.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

Por padrão, o pool de buffers híbrido é definido como habilitado no escopo do banco de dados.

## <a name="disable-hybrid-buffer-pool"></a>Desabilitar o pool de buffers híbrido

O seguinte exemplo desabilita o pool de buffers híbrido em uma instância do SQL Server:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

Por padrão, o pool de buffers híbrido é definido como desabilitado no escopo da instância. Observe que, para a alteração de configuração entrem em vigor, a instância do SQL Server deve ser reiniciada. A reinicialização é necessária para evitar a alocação de páginas de hash, uma vez que a capacidade PMEM no servidor não precisa ser considerada.

O exemplo a seguir desabilita o pool de buffers híbrido em um banco de dados específico.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

Por padrão, o pool de buffers híbrido é definido como habilitado no escopo do banco de dados.

## <a name="view-hybrid-buffer-pool-configuration"></a>Exibir a configuração do pool de buffers híbrido

O exemplo a seguir retorna o status atual da configuração do sistema do pool de buffers híbrido para uma instância do SQL Server.

```sql
SELECT *
FROM sys.configurations
WHERE
    name = 'hybrid_buffer_pool';
```

O seguinte exemplo retorna duas tabelas:

- A primeira mostra o status atual da configuração do sistema do pool de buffers híbrido para uma instância do SQL Server.
- A segunda lista os bancos de dados e a configuração no nível de banco de dados para o pool de buffers híbrido (`is_memory_optimized_enabled`).

```sql
SELECT * FROM sys.configurations WHERE name = 'hybrid_buffer_pool';

SELECT name, is_memory_optimized_enabled FROM sys.databases;
```

## <a name="best-practices-for-hybrid-buffer-pool"></a>Melhores práticas para o pool de buffers híbrido

Não é recomendável habilitar o pool de buffers híbrido em instâncias com menos de 16 GB de RAM.

Ao formatar seu dispositivo PMEM no Windows, use o maior tamanho de unidade de alocação disponível para NTFS (2 MB no Windows Server 2019) e verifique se o dispositivo foi formatado para o DAX (Direct Access).

Os tamanhos de arquivos devem ser um múltiplo de 2 MB (2 MB de módulo deve igual a zero).

Se a configuração no escopo do servidor para o pool de buffers híbrido for definida como desabilitada, o pool de buffers híbrido não será usado por nenhum banco de dados de usuário.

Se a configuração no escopo do servidor para o buffer híbrido estiver habilitada, você poderá desabilitar o uso do pool de buffers híbrido para bancos de dados de usuário individuais seguindo as etapas para desabilitar o pool de buffers híbrido no nível do escopo do banco de dados para esses bancos de dados de usuário.
