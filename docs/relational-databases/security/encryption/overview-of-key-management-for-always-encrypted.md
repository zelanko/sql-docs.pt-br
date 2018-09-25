---
title: Visão geral do gerenciamento de chaves do Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2016
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 07a305b1-4110-42f0-b7aa-28a4e32e912a
caps.latest.revision: 32
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 60010a0d537b619dc3227efccc6d012e1456992b
ms.sourcegitcommit: 3762dd447ca4bb449eda8476e72f393db0851b38
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/18/2018
ms.locfileid: "46013891"
---
# <a name="overview-of-key-management-for-always-encrypted"></a>Overview of Key Management for Always Encrypted
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) usa dois tipos de chaves de criptografia para proteger seus dados, uma chave para criptografar os dados e outra para criptografar a chave que criptografa os dados. A chave de criptografia de coluna criptografa os dados, a chave mestra de coluna criptografa a chave de criptografia de coluna. Este artigo fornece uma visão geral detalhada para gerenciar essas chaves de criptografia.

Ao discutir chaves Always Encrypted e o gerenciamento de chaves, é importante compreender a diferença entre as chaves de criptografia reais e os objetos de metadados que *descrevem* as chaves. Usamos os termos **chave de criptografia de coluna** e **chave mestra de coluna** para referir-se às chaves de criptografia reais e usamos os **metadados de chave de criptografia de coluna** e **metadados de chave mestra de coluna** para referir-se às *descrições* da chave Always Encrypted no banco de dados.

- ***Chaves de criptografia de coluna*** são chaves de criptografia de conteúdo usadas para criptografar dados. Como o nome implica, usamos chaves de criptografia de coluna para criptografar dados em colunas de banco de dados. Você pode criptografar uma ou mais colunas com a mesma chave de criptografia de coluna ou pode usar várias chaves de criptografia de coluna dependendo dos requisitos do aplicativo. As chaves de criptografia de coluna são criptografadas elas mesmas e apenas os valores criptografados das chaves de criptografia de coluna são armazenados no banco de dados (como parte dos metadados de chave de criptografia de coluna). Os metadados de chave de criptografia de coluna são armazenados nas exibições de catálogo [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) e [sys.column_encryption_key_values (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) . As chaves de criptografia de coluna usadas com o algoritmo AES-256 têm 256 bits.


- ***Chaves mestras de coluna*** são chaves de proteção usadas para criptografar as chaves de criptografia de coluna. Chaves mestras de coluna devem ser armazenadas em um repositório de chave confiável, como o Repositório de Certificados do Windows, o Cofre de Chaves do Azure ou um módulo de segurança de hardware. O banco de dados só contém metadados sobre chaves mestras de coluna (o tipo e local do repositório de chaves). Os metadados de chave mestra de coluna são armazenados na exibição de catálogo [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md) .  

É importante observar que os metadados de chave no sistema de banco de dados não contém chaves mestras de coluna de texto não criptografado ou chaves de criptografia de coluna de texto não criptografado. O banco de dados contém apenas informações sobre o tipo e o local das chaves mestras de coluna e valores criptografados das chaves de criptografia de coluna. Isso significa que chaves com texto não criptografado nunca são expostas no sistema de banco de dados, garantindo que os dados protegidos que usam o Always Encrypted estejam seguros, mesmo se o sistema de banco de dados for comprometido. Para garantir que o sistema de banco de dados não possa obter acesso às chaves de texto não criptografado, execute as ferramentas de gerenciamento de chaves em um computador diferente daquele que hospeda seu banco de dados. Leia a seção [Considerações de segurança para gerenciamento de chaves](#SecurityForKeyManagement) abaixo para ver os detalhes.

Como o banco de dados só contém dados criptografados (em colunas Always Encrypted protegidas) e não pode acessar as chaves de texto não criptografado, ele não pode descriptografar os dados. Isso significa que consultar colunas Always Encrypted simplesmente retornará valores criptografados, por isso aplicativos cliente que precisam criptografar ou descriptografar dados protegidos devem ser capazes de acessar a chave mestra de coluna e as chaves de criptografia de coluna relacionadas. Para ver os detalhes, consulte [Always Encrypted (desenvolvimento de cliente)](../../../relational-databases/security/encryption/always-encrypted-client-development.md).



## <a name="key-management-tasks"></a>Tarefas de Gerenciamento de Chaves

O processo de gerenciamento de chaves pode ser dividido nas seguintes tarefas de alto nível:

- **Provisionamento de chave** - Criar as chaves físicas em um repositório de chaves confiável (por exemplo, no Repositório de Certificados do Windows, o Cofre de Chaves do Azure ou um módulo de segurança de hardware), chaves de criptografia de coluna de criptografia com chaves mestras de coluna e criar metadados para os dois tipos de chaves no banco de dados.

- **Rotação de chaves** - Substituir periodicamente uma chave existente por uma nova chave. Pode ser necessário girar uma chave se ela tiver sido comprometida ou para manter a conformidade com políticas e regulamentos da sua organização que exigem que chaves criptográficas sejam giradas. 


## <a name="KeyManagementRoles"></a> Funções de Gerenciamento de Chaves

Existem duas funções distintas de usuários que gerencia chaves Always Encrypted: Administradores de Segurança e DBAs (Administradores de Banco de Dados):

- **Administrador de Segurança** - Gera chaves de criptografia de coluna e chaves mestras de coluna e gerencia repositórios de chaves que contém as chaves mestras de coluna. Para executar essas tarefas, um Administrador de Segurança deve ser capaz de acessar as chaves e o repositório de chaves, mas não precisam de acesso ao banco de dados.
- **DBA** – gerencia os metadados das chaves no banco de dados. Para executar tarefas de gerenciamento de chaves, um DBA precisa ser capaz de gerenciar metadados de chave no banco de dados, mas não precisam acessar as chaves ou repositório de chaves que contém as chaves mestras de coluna.

Considerando as funções acima, há duas maneiras de executar tarefas de gerenciamento de chaves para Always Encrypted: *com separação de função*e *sem separação de funções*. Dependendo das necessidades da sua organização, você pode selecionar o processo de gerenciamento de chaves que melhor atenda às suas necessidades.

## <a name="managing-keys-with-role-separation"></a>Gerenciamento de chaves com separação de funções
Quando chaves Always Encrypted forem gerenciadas com separação de funções, pessoas diferentes em uma organização assumem as funções de Administrador de Segurança e de DBA. Um processo de gerenciamento de chaves com separação de funções garante que DBAs não tenham acesso a chaves ou repositórios de chaves que contém chaves reais e os Administradores de Segurança não tenham acesso ao banco de dados que contêm dados confidenciais. É recomendável gerenciar as chaves com separação de funções se sua meta for garantir que os DBAs na sua organização não possam acessar dados confidenciais. 

**Observação:** Administradores de Segurança geram e trabalham com as chaves de texto não criptografado, por isso nunca devem executar suas tarefas nos mesmos computadores que hospedam um sistema de banco de dados ou computadores que podem ser acessados por DBAs ou outras pessoas que podem ser possíveis adversários. 

## <a name="managing-keys-without-role-separation"></a>Gerenciamento de chaves sem separação de funções
Quando chaves Always Encrypted são gerenciadas sem a separação de funções, uma única pessoa pode assumir ambas as funções de Administrador de Segurança e de DBA, o que significa que a pessoa precisa ser capaz de acessar e gerenciar tanto as chaves/repositório de chaves quanto os metadados de chaves. Gerenciar chaves sem separação de funções pode ser recomendado para organizações que usam o modelo de DevOps ou se o banco de dados estiver hospedado na nuvem e o principal objetivo for impedir que os administradores de nuvem (mas não os DBAs locais) acessem dados confidenciais.



## <a name="tools-for-managing-always-encrypted-keys"></a>Ferramentas para gerenciar chaves Always Encrypted

Chaves Always Encrypted podem ser gerenciadas usando o [SSMS (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms174173.aspx) e [PowerShell](../../scripting/sql-server-powershell.md):

- **SSMS (SQL Server Management Studio)** – fornece caixas de diálogo e assistentes que combinam tarefas que envolvem o acesso ao repositório de chaves e ao banco de dados, por isso o SSMS não dá suporte à separação de funções, mas facilita a configuração de suas chaves. Para obter mais informações sobre gerenciamento de chaves usando o SSMS, consulte:
    - [Provisionando chaves mestras de coluna](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#provisioncmk)
    - [Provisionando chaves de criptografia de coluna](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#provisioncek)
    - [Rotação de chaves mestras de coluna](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#rotatecmk)
    - [Girando chaves de criptografia de coluna](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#rotatecek)


- **SQL Server PowerShell** – inclui cmdlets para gerenciar chaves Always Encrypted com e sem separação de funções. Para obter mais informações, consulte:
    - [Configurar chaves do Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
    - [Girar chaves Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)


## <a name="SecurityForKeyManagement"></a> Considerações de segurança para gerenciamento de chaves

O principal objetivo do Always Encrypted é garantir que os dados confidenciais armazenados em um banco de dados estejam seguros, mesmo se o sistema de banco de dados ou seu ambiente de hospedagem for comprometido. Exemplos de ataques de segurança em que o Always Encrypted pode ajudar a impedir vazamentos de dados confidenciais:

- Um usuário de banco de dados de alto privilégio mal-intencionado, como um DBA, consultando colunas de dados confidenciais.
- Um administrador invasor de um computador que hospeda uma instância do SQL Server examinando a memória de um processo do SQL Server ou arquivos de despejo de memória do processo do SQL Server.
- Um operador do data center mal-intencionado consulta um banco de dados do cliente, examinando os arquivos de despejo do SQL Server ou examinando a memória de um computador que hospeda os dados do cliente na nuvem.
- Malware em execução em um computador que hospeda o banco de dados.

Para garantir que Always Encrypted seja eficaz na prevenção desses tipos de ataques, o processo de gerenciamento de chaves deve garantir que as chaves mestras de coluna e as chaves de criptografia de coluna, bem como as credenciais para um repositório de chaves que contém as chaves mestras de coluna, nunca sejam reveladas para um invasor em potencial. Aqui estão algumas diretrizes que você deve seguir:

- Nunca gere chaves mestras de coluna ou as chaves de criptografia de coluna em um computador que hospeda o banco de dados. Em vez disso, gere as chaves em um computador separado, dedicado para o gerenciamento de chaves ou que hospeda aplicativos que também precisarão de acesso às chaves. Isso significa que **você nunca deve executar ferramentas usadas para gerar as chaves no computador que hospeda o banco de dados** , pois se um invasor acessar um computador usado para provisionar ou manter as chaves Always Encrypted, ele poderá potencialmente obter suas chaves, mesmo se elas aparecerem somente na memória da ferramenta por um curto período.
- Para garantir que o processo de gerenciamento de chaves não revele inadvertidamente as chaves mestras de coluna ou as chaves de criptografia de coluna, é essencial identificar os possíveis adversários e ameaças de segurança antes de definir e implementar um processo de gerenciamento de chaves. Por exemplo, se sua meta é garantir que os DBAs não tenham acesso a dados confidenciais, um DBA não pode ser o responsável por gerar as chaves. Um DBA, no entanto, *pode* gerenciar metadados de chave no banco de dados, pois os metadados não contêm as chaves de texto não criptografado.

## <a name="next-steps"></a>Next Steps

- [Criar e armazenar chaves mestras de coluna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Configurar chaves do Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
- [Girar chaves Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Configurar o Always Encrypted usando o SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)

## <a name="additional-resources"></a>Recursos adicionais

- [Always Encrypted (mecanismo de banco de dados)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted (Client Development)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [Tutorial do assistente do Always Encrypted (Cofre de Chaves do Azure)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault/)
- [Tutorial do assistente do Always Encrypted (Repositório de Certificados do Windows)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)




